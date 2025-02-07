
# How To Build

## 1. Install Rust toolchain
```
# Easiest way to install rustup under Ubuntu
$ sudo snap install rustup
```

[https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)
[https://docs.docker.com/desktop/setup/install/linux/](https://docs.docker.com/desktop/setup/install/linux/)
[https://docs.docker.com/engine/install/linux-postinstall/](https://docs.docker.com/engine/install/linux-postinstall/)

```console
# For nightly builds: $ rustup toolchain install nightly
# automatically infers the platform
$ rustup toolchain install stable
$ rustup default stable
```

## 2. Install dependencies
´´´console
# On Ubuntu or Debian, install
$ sudo apt install libobs-dev
´´´

## 3. Build
```bash
cargo build --release
```

## 4. Cross-Building
Linux to Windows
```console
rustup toolchain install x86_64-pc-windows-gnu
cargo build --release --target x86_64-pc-windows-gnu
```

Linux to MacOS Crossbuilding
```bash
$ docker run --rm -it -v $(pwd):/io -w /io ghcr.io/rust-cross/cargo-zigbuild   cargo zigbuild --release --target aarch64-apple-darwin
```
The docker container has everything installed, including the MacOS SDK, the cargo-zigbuild crate,
**except for the libobs.framework**.
You can get *a* libobs.framework from [https://github.com/obsproject/obs-studio/actions/runs](OBS' GitHub Actions),
map you have to map it into the container manually, copy it into the SDK/System/Library/Frameworks
Alternatively [https://github.com/tpoechtrager/osxcross](installing the SDK on the Linux host) also works,
but I have no idea how to get zigbuild to find the frameworks on the linux host
(don't forget to copy over the libobs.framework aswell)