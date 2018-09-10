We are currently in the process of discussing Clippy 1.0 via the RFC process in https://github.com/rust-lang/rfcs/pull/2476 . The RFC's goal is to clarify policies around lint categorizations and the policy around which lints should be in the compiler and which lints should be in Clippy. Please leave your thoughts on the RFC PR.

# Clippy

[![Build Status](https://travis-ci.org/rust-lang-nursery/rust-clippy.svg?branch=master)](https://travis-ci.org/rust-lang-nursery/rust-clippy)
[![Windows Build status](https://ci.appveyor.com/api/projects/status/id677xpw1dguo7iw?svg=true)](https://ci.appveyor.com/project/rust-lang-libs/rust-clippy)
[![Current Version](https://meritbadge.herokuapp.com/clippy)](https://crates.io/crates/clippy)
[![License: MPL-2.0](https://img.shields.io/crates/l/clippy.svg)](#license)

A collection of lints to catch common mistakes and improve your [Rust](https://github.com/rust-lang/rust) code.

[There are 275 lints included in this crate!](https://rust-lang-nursery.github.io/rust-clippy/master/index.html)

We have a bunch of lint categories to allow you to choose how much Clippy is supposed to ~~annoy~~ help you:

* `clippy::all` (everything that has no false positives)
* `clippy::pedantic` (everything)
* `clippy::nursery` (new lints that aren't quite ready yet)
* `clippy::style` (code that should be written in a more idiomatic way)
* `clippy::complexity` (code that does something simple but in a complex way)
* `clippy::perf` (code that can be written in a faster way)
* `clippy::cargo` (checks against the cargo manifest)
* **`clippy::correctness`** (code that is just outright wrong or very very useless)

More to come, please [file an issue](https://github.com/rust-lang-nursery/rust-clippy/issues) if you have ideas!

Table of contents:

*   [Usage instructions](#usage)
*   [Configuration](#configuration)
*   [License](#license)

## Usage

Since this is a tool for helping the developer of a library or application
write better code, it is recommended not to include Clippy as a hard dependency.
Options include using it as an optional dependency, as a cargo subcommand, or
as an included feature during build. These options are detailed below.

### As a cargo subcommand (`cargo clippy`)

One way to use Clippy is by installing Clippy through rustup as a cargo
subcommand.

#### Step 1: Install rustup

You can install [rustup](http://rustup.rs/) on supported platforms. This will help
us install clippy and its dependencies.

If you already have rustup installed, update to ensure you have the latest
rustup and compiler:

```terminal
rustup update
```

#### Step 2: Install nightly toolchain

Rustup integration is still new, you will need a relatively new nightly (2018-07-15 or later).

To install Rust nightly with [rustup](https://rustup.rs/):

```terminal
rustup install nightly
```

#### Step 3: Install clippy

Once you have rustup and the nightly toolchain installed, run the following command:

```terminal
rustup component add clippy-preview --toolchain=nightly
```

Now you can run Clippy by invoking `cargo +nightly clippy`. If nightly is your
default toolchain in rustup, `cargo clippy` will work fine.

### Running Clippy from the command line without installing it

To have cargo compile your crate with Clippy without Clippy installation
in your code, you can use:

```terminal
cargo run --bin cargo-clippy --manifest-path=path_to_clippys_Cargo.toml
```

*[Note](https://github.com/rust-lang-nursery/rust-clippy/wiki#a-word-of-warning):*
Be sure that Clippy was compiled with the same version of rustc that cargo invokes here!

## Configuration

Some lints can be configured in a TOML file named `clippy.toml` or `.clippy.toml`. It contains a basic `variable = value` mapping eg.

```toml
blacklisted-names = ["toto", "tata", "titi"]
cyclomatic-complexity-threshold = 30
```

See the [list of lints](https://rust-lang-nursery.github.io/rust-clippy/master/index.html) for more information about which lints can be configured and the
meaning of the variables.

To deactivate the “for further information visit *lint-link*” message you can
define the `CLIPPY_DISABLE_DOCS_LINKS` environment variable.

### Allowing/denying lints

You can add options  to `allow`/`warn`/`deny`:

*   the whole set of `Warn` lints using the `clippy` lint group (`#![deny(clippy::all)]`)

*   all lints using both the `clippy` and `clippy::pedantic` lint groups (`#![deny(clippy::all)]`,
    `#![deny(clippy::pedantic)]`). Note that `clippy::pedantic` contains some very aggressive
    lints prone to false positives.

*   only some lints (`#![deny(clippy::single_match, clippy::box_vec)]`, etc)

*   `allow`/`warn`/`deny` can be limited to a single function or module using `#[allow(...)]`, etc

Note: `deny` produces errors instead of warnings.

## Updating rustc

Sometimes, rustc moves forward without Clippy catching up. Therefore updating
rustc may leave Clippy a non-functional state until we fix the resulting
breakage.

You can use the [rust-update](rust-update) script to update rustc only if
Clippy would also update correctly.

## License

Licensed under [MPL](https://www.mozilla.org/MPL/2.0/).
If you're having issues with the license, let me know and I'll try to change it to something more permissive.