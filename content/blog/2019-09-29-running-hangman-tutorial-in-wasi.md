---
title: "Running WASM Binaries in on your local system"
date: 2019-09-29T21:06:02+02:00

tags:

summary: New WASI runtimes are out. This article explains how to run a wasm binary on a local machine.

author: thinkrapido
---

# Running WASM in a WASI Rutime

WASI stands for [WebAssembly System Interface](https://github.com/CraneStation/wasmtime/blob/master/docs/WASI-overview.md).

In short, WASI allows you to run wasm binaries in a sandbox on any platform which has a WASI runtime. This technique might liberate polyglot architectures some day to share native modules and exchange functionality among these languages.

You can follow the latest articles about WebAssembly on the [moz://a HACKS](https://hacks.mozilla.org/category/webassembly/) blog. There you can look for the author Lin Clark to read more about what WASI.

In this article, I want to explain the necessary steps to run a Rust compiled wasm on your local machine.

## Prerequisites

### WebAssembly Runtime

At [wasmtime.dev](https://wasmtime.dev/) you can install the latest runtime for linux based systems.

For windows, you need to compile the executables by yourself, but this isn't a problem.

Just clone the repo from GitHub [https://github.com/CraneStation/wasmtime](https://github.com/CraneStation/wasmtime) and perform

```bash
> git clone --recurse-submodules https://github.com/CraneStation/wasmtime.git
> cd wasmtime
> cargo build --release
```

in the command line.

(Don't forget to ```rustup update``` first, if you encounter any problems)

When finished, make the executables available to the command line, if you want to, or you have to provide the whole path to the executable ```wasmtime``` later on in this tutorial.

### Check-Out a Rust Project

For simplicity, I suggest you clone the hangman tutorial of the Rust Community Stuttgart from GitHub [https://github.com/rusticus-io/hangman](https://github.com/rusticus-io/hangman).

### Install the WASI compilation target

```
> rustup target add wasm32-wasi
```

## How to Compile the Project

Switch to your Rust project folder and compile the source.

```
cargo build --target wasm32-wasi
```

You can find the wasm in the ```target/wasm32-wasi/debug``` folder.

### Run the WASM Binary in the Runtime

```
> wasmtime target/wasm32-wasi/debug/hangman.wasm
```

And play the game ;).

# Conclusion

As you see, it's pretty easy to run the WASM on your local machine.

The benefit of the WASI runtime is that all the programs run in a sandbox which, out of the box, only provides access to your folder structure downwards. This helps limit access to the system for security reasons. If you want more flexibility, lookup the wasmtime command line options and (obviously) wait for future releases.

This means that the development of WASI is not finished yet.

I want to see what the future brings.

## Usuful Links

- [WebAssembly System Interface](https://github.com/CraneStation/wasmtime/blob/master/docs/WASI-overview.md)
- [wasi.dev](https://wasi.dev/)
- [moz://a HACKS](https://hacks.mozilla.org/category/webassembly/) WebAssembly Category
- Follow [Lin Clark](https://twitter.com/linclark) on Twitter
- [wasmtime](https://github.com/CraneStation/wasmtime), Mozilla’s WebAssembly runtime
- [Lucet](https://www.fastly.com/blog/announcing-lucet-fastly-native-webassembly-compiler-runtime), Fastly’s WebAssembly runtime
- [a browser polyfill](https://wasi.dev/polyfill/)