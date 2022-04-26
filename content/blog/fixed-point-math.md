+++
title = "A little Fixed Point Math"
date = 2022-04-26
draft = false
in_search_index = true
template = "blog_post.html"
+++

Recently, I wanted to generate some sounds for [MnemOS](./mnemos-initial-release.md), and I wanted it to go fast.

This is a little mini-blog post describing how I did that.

<!-- more -->

I wanted to generate a sine wave to play out of a speaker on my small embedded device. My end goal was to generate 44.1kHz PCM samples, which meant I needed to generate 44100 `i16`s per second.

I also needed to generate stereo audio, but for now, I just play the same sine wave on both channels.

In embedded Rust, the core library doesn't actually link in routines for things like `sin` operations.

This means that typically you have two choices to "provide" these operations:

1. The [`libm`](https://docs.rs/libm) crate, which provides very accurate implementations of math operations like `sin`, but is often (relatively) slow, and the code size is (relatively) large, as these are fit for very low error rate calculations.
2. The [`micromath`](https://docs.rs/micromath/), which provides reasonable approximations of many operations like `sin`, to some respectable precision (but less precise than `libm`).

Since I knew I didn't need *crazy* accurate data, I didn't even try libm for this. My initial code using `micromath` looked like this, for generating my sine wave data:

```rust
// Generate N samples, interleaving left and right i16 PCM samples
for (i, dat) in idata.chunks_exact_mut(2).enumerate() {
    use micromath::F32Ext;
    let mut value = (i as f32);
    value *= (2.0 * core::f32::consts::PI * 441.0);
    value /= 44100.0;
    let ival = (value.sin() * (i16::MAX as f32)) as i16;
    dat.iter_mut().for_each(|i| *i = ival);
}
```

I profiled this on my 64MHz Cortex-M4F CPU, and found it took an acceptable, but not impressive, average of 114 CPU cycles per loop iteration.

**This meant that to generate 44100 samples per second, I would spend a total of 5.02M cycles/second generating the audio, out of a total of 64M cycles I had total, which was 7.9% of my entire CPU time.**

So instead, I decided to use a slightly different approach, using a phase accumulator, and fixed point math, and a pre-calculated 256-entry look up table.

Generating the sine table was pretty straightforward, I ran this on my desktop, and copy and pasted the output into an array:

```rust
// Generate a 256 point sine look up table
for i in 0..256 {
    let val = 2.0 * core::f32::consts::PI * ((i as f32) / 256.0);
    let val = (i16::MAX as f32) * val.sin();
    print!("{}, ", val.round() as i16);
}
println!();
```

That code looked like this:

```rust
// A pre-calculated Sine Look Up Table, or LUT.
use crate::SINE_TABLE; // : [i16; 256];

// We have a sample rate at 44.1kHz. Figure out how many samples it
// will take to play a single loop of our sine wave. For example,
// at 441hz, it will take 100 samples to "traverse" one
// whole sine wave.
let samp_per_cyc: f32 = 44100.0 / 441.0;

// The increment is (how many items are in our look up table)
// divided by (how long it takes to go through one look up table)
let fincr = 256.0 / samp_per_cyc;

// Convert this number to an i32, which we use as a fixed point
// decimal, basically 8bits.24bits, where the 8 bits are which LUT
// position we are currently in, and the 24 bits are like a "decimal"
// describing where we are between the LUT positions
let incr: i32 = (((1 << 24) as f32) * fincr) as i32;

// This calculation is based on the current "phase angle" of the sine
// table. This works because we increment our progress through the
// 256 value in our 8.24 fixed point number, and it will wrap around
// correctly whenever we "overflow" (this is a good thing! our sine
// table is the same loop over and over and over and...)
let mut cur_offset = 0i32;

// generate the next N samples...
idata.chunks_exact_mut(2).for_each(|i| {
    let val = cur_offset as u32;

    // Mask off the top 8 bits. This tells us which LUT position
    // we are in
    let idx_now = ((val >> 24) & 0xFF) as u8;
    // Add one (wrapping), to tell us what the NEXT LUT position is.
    let idx_nxt = idx_now.wrapping_add(1);

    // Get the i16 value of the two LUT data points
    let base_val = SINE_TABLE[idx_now as usize] as i32;
    let next_val = SINE_TABLE[idx_nxt as usize] as i32;

    // Distance to next value - perform 256 slot linear interpolation

    // Here, I take the top 8 bits of the 24 bit "decimal" part of
    // the number. This will be used to interpolate one of
    // 256 positions between the two LUT positions.
    //
    // This is to reduce error between the "steps" of each LUT
    // value in our table
    let off = ((val >> 16) & 0xFF) as i32; // 0..=255

    // Here, we "weight" each sample based on how close we are at. We
    // multiply this to a total of 256x larger than our original
    // sample, split between how close we are between the two samples.
    // We multiply each, then add them back together
    let cur_weight = base_val.wrapping_mul(256i32.wrapping_sub(off));
    let nxt_weight = next_val.wrapping_mul(off);
    let ttl_weight = cur_weight.wrapping_add(nxt_weight);

    // Our number is now the weighted average of the two LUT samples,
    // but 256x too big. Reduce it down with a right shift operation.
    let ttl_val = ttl_weight >> 8; // div 256

    // Un-sign-extend this back to an i16, to use as a sample
    let ttl_val = ttl_val as i16;

    // Set the linearly interpolated value to the left and
    // right channel
    i.iter_mut().for_each(|i| *i = ttl_val);

    // Adjust our phase angle by the "increment" we calculated earlier
    cur_offset = cur_offset.wrapping_add(incr);
});
```

**When profiling this approach, My average loop time was now down to 22 cycles per iteration, meaning it would now only take me 970.2k CPU cycles per second, or 1.5% of my total CPU time!**

I also checked my approximation against the "real" floating point sine operation, and found a maximum error of 0.012% for any `i16` value, which is more than close enough for my ears!

There's no long term lesson here, I just wanted to share the technique I used, and explain it a little bit. These approaches are widely used in high performance audio equipment, but I hadn't found too many clear examples to use when writing my code.
