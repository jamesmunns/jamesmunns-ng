+++
title = "James' password recovery plan"
date = 2020-04-10
draft = false
in_search_index = true
template = "blog_post.html"
+++

**Last updated: 2020-04-10**

In case of an emergency, I would like to have the people I trust to be able to access my list of accounts and passwords. This is intended for cases where I am incapacitated in some way, temporarily or permanently.

Rather than sharing my password(s) with any one emergency contact, this is a process that requires multiple people to work together to gain access, preventing any one person from gaining access to my information on-demand.

Your threat model may vary. This is meant only to share what I did, not necessarily be a specific guide for all use cases.

<!-- more -->

## Glossary

* [Shamir's Secret Sharing] - This is the technique that allows a secret to be split into multiple shares. To recover the secret, N (of a total of M) shares must be combined.
* Secret - In this case, the secret is the root password for my password database
* Share - The component held by each person on my contact list
* Share holder - the person holding one of the Shares
* "password" database - the Keepass database containing all of my passwords and accounts
* "share" database - the Keepass database containing the Share for each Share holder.

## Tools

* [KeePass] - This is the open source tool that I use to store my passwords under. There are clients for Windows, Mac, Linux, and mobile devices.
* [ssss] - Shamir's Secret Sharing Scheme - this is the linux command line tool I used to split the secrets into shares. The source code [is available here]. The tool is widely available on Linux, and appears to be available on Brew for OSX. There also appears to be an [updated fork] with some fixes and enhancements.

[Shamir's Secret Sharing]: https://en.wikipedia.org/wiki/Shamir's_Secret_Sharing
[KeePass]: https://keepass.info/
[ssss]: https://linux.die.net/man/1/ssss
[is available here]: http://point-at-infinity.org/ssss/index.html
[updated fork]: https://github.com/MrJoy/ssss

## Setup steps: for the person sharing the data

In this case, the person sharing the data is me, James. The data is the password to my encrypted password database.

All passwords should be tracked within a secure password database, where all passwords are stored in an encrypted fashion. It should be possible to unlock this database with a strong password. You should include all passwords here, including:

* Phone passwords - including full disk encryption and SIM passwords
* PC/Server passwords - including any user or root accounts, as well as full disk encryption passwords
* Online accounts - particularly for primary email accounts
* Backup
* SSH keys/root GPG keys

If necessary, you may want to include instructions for access of some devices, such as hostnames, ports, and other settings. Or, instructions on how to unlock full disk encyption of devices. This can be done in an INSTRUCTIONS category of the database.

You should collect a list of trusted friends who can work together to gain access to your password if necessary. Your threat model may vary.

For my purposes, I have selected 8 contacts in different countries (physically distant, meaning it is unlikely they will be incapcitated at the same time), and require 5 people to work together to unlock the secrets. In my case, this requires people in different countries to work together.

### Splitting the password

You will need to install the [ssss] tool on a suitable platform. I used the [AUR package] on Arch linux.

[AUR package]: https://aur.archlinux.org/packages/ssss/

Run this command, and enter in your password. This will take a while, and the tool gives no graphical feedback. I had to wait about a minute or so. Eventually it will spit out a list of secrets

Command:

```shell
ssss-split -t 5 -n 8 -w james-test-0000 -s 512
```

Example output:

```shell
# password used was "thisisatestoftheemergencybroadcastsystem"
ssss-split -t 5 -n 8 -w james-test-0000 -s 512
Generating shares using a (5,8) scheme with a 512 bit security level.
Enter the secret, at most 64 ASCII characters:
james-test-0000-1-7aa8787ba5b297ea2cb7763befd574e0d42a32efe6136e8a34c84adf15a315a0e717c0540215ee21d8c0e29dfb33f2426e17a8e2ee254a9fa9b83196da4aab35
james-test-0000-2-518824115bd445a59cc99b7af3e61800312249a58a6202cc387f31eaad4d6d0fb81e35cb05b064abb5332d31c80d112131579d562080553426c5ed71359aa03d
james-test-0000-3-06603131ab745291b861ac50531c80c2aeb1675ce92d58c94b49ee41ec93b0b05676e26b56ea1da879602f1a65d24bb12585804a44ee635d14529334a28cba4e
james-test-0000-4-3b5dae33fe554cade712a9701fd1a7225ce59f1bba78b58f23748e23765744ccd59846f31be41b6a621b04b85d414bafe153b3455d92cae3d8c5d4ee226e40ae
james-test-0000-5-0567cc4a81c01c0ba796c49e3412efe069a73ad08d5f27f460d154ff6869dcb544d0838aee29c5a621834a62933fe82355aefb29975e058a2389999becd1755b
james-test-0000-6-fde37e9361cc4160dfb09c563e522301d90c57fe49ffdb4e0d4025246f472f96e59953a6a4a300b353e61c2c6742f9794ab0647c04bee8203f42231cb0532037
james-test-0000-7-bb9f0df49c3e0b9be5e0ef9420992d18b90871e5b9a067fc280e255fb5ef7618d06afd41dd84898b923d900b64077f2aa89986b62c49b449ea90080fbb0f1a37
james-test-0000-8-e811818f88ccc3450cfe4285e937fa94b746551f63dd515fa1f6e33352079c276c7181360bf86742c9a9d9824bc8446896eb31582abcca8484476d2c732897e9
```

### Encrypting the parts

In order to store these secrets, a keepass database should be created for each share holder. You should use a separate password for each share holder.

Keepass was re-used for this in order to keep the total number of tools low, as well as the decryption step portable and simple. You could use a number of command line tools to encrypt the secret as text or as a file, but users on Windows (or even OSX) may have difficulty extracting the secrets.

### Distributing the parts

Once the keepass databases have been created, send the databases to each share holder. Email works for this.

Each share holder should receive:

* The "share" database - containing their portion of the secret
* The "password" database - containing all of your passwords
* This instruction document

You should provide the "share" database password to each shareholder through a separate medium, such as a video/voice call, or by mail. Sharing this in written form (text message, email), is not recommended.

### Verifying it worked

## Verification instructions

The share holder should verify that they are able to access the contents of the keepass database. The database should include one entry, with the entry looking something like `5-0567cc4a81c01c0ba796c49e3412efe069a73ad08d5f27f460d154ff6869dcb544d0838aee29c5a621834a62933fe82355aefb29975e058a2389999becd1755b`.

## Storage instructions

The share holder should store the password for the "share" database somewhere secure, such as in their own separate password database, or on paper in a secure location, such as a safe.

The share holder should store the "password" database somewhere secure, such as on an offline drive if possible.

## Combination instructions

### When to share information

In general, all share holders should be very cautious before sharing their component of the secret. This process should only be activated if:

* I am deceased
* I am incapacitated for an unknown amount of time, at least 1 week or more.
* I have lost access to my accounts and backups, e.g. in a fire or other natural disaster

Effort should be made, particularly for those that are physically capable of doing so, to verify that I am indeed deceased or incapacitated, or that I have lost my accounts/backups.

I leave it up to each of the share holder's best judgement when to share their component or not. In general, it should not ever be necessary to do this in a rush. Consider waiting a day or two after being contacted before sharing, and attempt to reach out to me or multiple share holders through multiple mediums (email, voice call, or even a video call if possible) to ensure that information SHOULD be shared, and that I or one of the share holders has not been comprimised though a phishing attack or other means. This includes any requests from me directly.

All share holders have the complete contact list, and should use it when necessary.

### How to share information

Once it has been decided that the share holders should unlock my password database, one shareholder should be chosen as the one to receive the shares. If possible, this should be my wife Laura. This person will do the final "assembly".

Each of the share holders should send their "share" keepass database to the person doing the assembly. This can be done through email after confirmation through other mediums has been completed.

The password for these parts should be provided through a separate medium, such as a phone call or by mail. This password should never be sent through email, text message, etc.

The receiver should be capable of performing the instructions in the next section.

### Once the pieces have been assembled

Run this command, and enter in the required number of shares. When entering the shares, do NOT enter in the prefix tag.

Command:

```shell
ssss-combine -t 5
```

Example output

```shell
ssss-combine -t 5
Enter 5 shares separated by newlines:
Share [1/5]: 2-518824115bd445a59cc99b7af3e61800312249a58a6202cc387f31eaad4d6d0fb81e35cb05b064abb5332d31c80d112131579d562080553426c5ed71359aa03d
Share [2/5]: 3-06603131ab745291b861ac50531c80c2aeb1675ce92d58c94b49ee41ec93b0b05676e26b56ea1da879602f1a65d24bb12585804a44ee635d14529334a28cba4e
Share [3/5]: 4-3b5dae33fe554cade712a9701fd1a7225ce59f1bba78b58f23748e23765744ccd59846f31be41b6a621b04b85d414bafe153b3455d92cae3d8c5d4ee226e40ae
Share [4/5]: 5-0567cc4a81c01c0ba796c49e3412efe069a73ad08d5f27f460d154ff6869dcb544d0838aee29c5a621834a62933fe82355aefb29975e058a2389999becd1755b
Share [5/5]: 7-bb9f0df49c3e0b9be5e0ef9420992d18b90871e5b9a067fc280e255fb5ef7618d06afd41dd84898b923d900b64077f2aa89986b62c49b449ea90080fbb0f1a37
Resulting secret: thisisatestoftheemergencybroadcastsystem
```

The "Resulting secret" is the password to my Keepass database. This can be used to unlock my password storage file. Even after unlocking, this password should be kept secret only by the assember, as anyone with my password database and this password will have access to all of my accounts.

Once you have unlocked this storage, please change the password for each account.
