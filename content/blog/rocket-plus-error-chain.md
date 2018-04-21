+++
title = "Rocket + error_chain"
date = 2017-07-22
draft = false
aliases = ["update/2017/07/22/rocket-plus-error-chain.html"]
in_search_index = true
template = "blog_post.html"

# TODO
# tags = []
# category = ""
+++

Recently I've gotten the chance to work in Rust a little more often, and I've been using the wonderful web framework [Rocket](https://rocket.rs). Primarily, I've been using it to develop a REST server, serving and receiving JSON data. I've also been using [error_chain](https://github.com/brson/error-chain), which is a great tool to avoid error handling boilerplate.

However, I was having difficulty getting them to work together the way that I wanted. In my mind, if my Rocket handler returned `Ok(Json(T))`, it would make sense to return the JSON in the body, and a return code of 200. If my Rocket handler returned `Err(Json(T))`, then the server should return `400` (or maybe `500`), with my error in the body.

<!-- more -->

Well, I came up with a bit of code that manages to get that behavior, while also using some convenient features from `error_chain`. Heres the whole example, then I'll explain a bit after:

```
#![feature(plugin)]
#![plugin(rocket_codegen)]

#[macro_use] extern crate error_chain;
#[macro_use] extern crate rocket_contrib;
extern crate rocket;

use rocket_contrib::{Json, Value};
use std::io::{Error, ErrorKind};

mod echain {
    use rocket::request::Request;
    use rocket::response::{Response, Responder};
    use std::io::Cursor;
    use rocket::http::{Status, ContentType};

    // This generates basic Error, Result, etc. types
    error_chain!{ }

    // Implement `Responder` for `error_chain`'s `Error` type
    // that we just generated
    impl<'r> Responder<'r> for Error {
        fn respond_to(self, _: &Request) -> ::std::result::Result<Response<'r>, Status> {
            // Render the whole error chain to a single string
            let mut rslt = String::new();
            rslt += &format!("Error: {}", self);
            self.iter().skip(1).map(|ce| rslt += &format!(", caused by: {}", ce)).collect::<Vec<_>>();

            // Create JSON response
            let resp = json!({
                "status": "failure",
                "message": rslt,
            }).to_string();

            // Respond. The `Ok` here is a bit of a misnomer. It means we
            // successfully created an error response
            Ok(Response::build()
                .status(Status::BadRequest)
                .header(ContentType::JSON)
                .sized_body(Cursor::new(resp))
                .finalize())
        }
    }
}

// Pull in our instance of `error_chain`'s ResultExt. This allows us to
// use `chain_err()` in this context. Don't pull in `Result`, because this
// will confuse Rocket which uses `std::result::Result`
use echain::ResultExt;

#[get("/<number>", format = "application/json")]
pub fn hello(number: u8) -> Result<Json<Value>, echain::Error>
{
    works_above_127(number)
        .chain_err(|| "curse your sudden but inevitable betrayal")?;

    Ok(Json(json!({
        "status": "it worked"
    })))
}

fn works_above_127(number: u8) -> std::io::Result<()> {
    if number < 128 {
        Err(Error::new(ErrorKind::Other, "Some sort of IO problem"))
    } else {
        Ok(())
    }
}

fn main() {
    rocket::ignite().mount("/hello", routes![hello]).launch();
}
```

The main trick here is implementing `Responder` for `Error`. When Rocket receives an `Error` back from a handler, it does one of two things:

1. If the `Error` doesn't implement `Responder`, then a generic 500 response is generated and returned to the client
2. If the `Error` does implement `Responder`, then:
    * If `error.respond_to()` returns an `Error`, then the generic 500 response is returned to the client
    * If `error.respond_to()` returns an `Ok(Response)`, that response is returned to the client

So, by implementing `Responder` for `error_chain`'s `Error`, we can control what the response is, and get our intended behavior. Additionally, we have access to all errors in the chain, which we can return to the user (if we like).

Heres what it looks like when I test it with a bit of Python code:

```
import requests as r

x = r.get("http://localhost:8000/hello/28", json={})
print(x.status_code) # "400"
print(x.json())
# "{'message': 'Error: curse your sudden but inevitable betrayal, caused by: Some sort of IO problem',
#   'status': 'failure'}"

x = r.get("http://localhost:8000/hello/128", json={})
print(x.status_code) # "200"
print(x.json()) # "{'status': 'it worked'}"
```

In the future, I will probably add some filtering on the `message` field, maybe showing the full chain in "development" mode, and just the top level error in "release" mode, depending on how sensitive the contents of the deeper errors are.