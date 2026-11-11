# mtgpu-rust

A self-contained aarch64 Rust toolchain from Chromium's pinned Rust fork
(commit `1edd55dcfc`, 2026-09-09), including the pieces Chromium needs:
`rustc-dev` (for crubit), `bindgen`, `rustfmt`, `rust-src`, and the crubit
binaries `cc_bindings_from_rs` / `rs_bindings_from_cc`.

## Install

```sh
sudo apt install ./mtgpu-rust_1.100.0-nightly_arm64.deb
source /opt/mtgpu-toolchain/env.sh
rustc --version   # rustc 1.100.0-nightly (1edd55dcfc 2026-09-09)
```

## Guarantees

- Installs **only** under `/opt/mtgpu-toolchain/rust`.
- Declares **no dependencies**, no alternatives, no system path changes.
- The distribution's `rustc`/`cargo` are untouched.
- Removal: `dpkg -r mtgpu-rust`.

## Why a custom toolchain

Chromium ships prebuilt Rust/clang only for x86-64.  On aarch64 everything has
to be built, and the Rust bits must be coherent: `rustc`, `rust-std` and
`rustc-dev` have to come from the **same** `x.py dist` run, otherwise crubit
fails with `E0514`/`E0460`/`E0464`.  The recipe is in
`mtgpu-kde/tools/chromium-hdr/TOOLCHAIN.md`.
