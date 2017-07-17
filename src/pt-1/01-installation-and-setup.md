# Installation and setup

## Install Rust

To install rust go to the [homepage](https://www.rust-lang.org), click the `install` button, and follow the instructions.

## Create the project

Go to wherever you keep your projects (e.g. `~/projects`) and tell `cargo` (Rust's package manager) that you'd like a new binary project:

```bash
$ cargo new --bin roguelike
$ cd roguelike
```

This does a few things; It creates a `git` repository along with a `.gitignore`, places a `Cargo.toml` in the root, and makes `src/main.rs` file.

## Hello, world!

If you run your program now:

```bash
$ cargo run --release
```

you'll get the output seen by nearly every programmer throughout the ages:

```
Compiling roguelike v0.1.0 (file:///Users/USERNAME/projects/roguelike)
  Finished release [optimized] target(s) in 0.21 secs
   Running `target/release/roguelike`

Hello, world!
```

When you run your program `cargo` (Rust's package manager) builds your library, and if no errors are found, places a binary in `target/release` named `roguelike` after your project's name, and then actually runs it on your behalf. That binary contains everything that is needed to run the program again on your platform (Windows, Mac, etc.).

If you were to open up `src/main.rs` in your favorite editor you'd see:

```rust
fn main() {
    println!("Hello, world!");
}
```

`main` is a special function name that is called on your behalf to start the program. After that is a call to a macro `println!` (macros are denoted by `!`, which is not particularly relevent atm) with the string literal `"Hello, world!"`.

`main` is where we will be putting our game, but first we'll need to add a library that we'll need to get the infamous `@` on the screen.

# Cargo.toml

You also have a `Cargo.toml` in your folder. [`toml`](https://github.com/toml-lang/toml) is a file format that is similar in spirit to `.ini`. Your program's metadata is written in `Cargo.toml`, along with any libraries you decide to pull in.

For now, we'll pull in 3 libraries: ("crates" in Rust/Cargo parlance) `gltile`, `pixset`, and `glium`. `gltile` is a terminal-like tile renderer that uses OpenGL behind the scenes. Don't worry, it presents a simple API that should hopefully be easy to pick up (and incidentally, is similar to `libtcod`). `pixset` is a toolkit for creating tilesets, and fonts and also has a default tileset that we'll be using. `glium` is a wrapper around OpenGL that `gltile` uses. You won't need to know OpenGL, and outside of some boilerplate, we won't be interacting with `glium` any.

Add the following 3 lines after the `[dependencies]` heading in `Cargo.toml`:

```toml
[dependencies]
glium = "0.17.0"
gltile = "0.0.5"
looper = "0.0.2"
pixset = "0.0.6
```

Now when you run your program again using `cargo run --release` you'll see it pull down the above crates, and their dependencies (and their dependencies dependencies...) and compile them all. It'll take a little bit, but you'll only need to do a full compilation when your dependencies change. That is all that is needed for setup. Easy, right?

Now on to getting an `@` showing! A "Hello, world!" of the Roguelike world, if you will.
