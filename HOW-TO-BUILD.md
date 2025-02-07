
# How To Build

## 1. Install Rust toolchain

#### 1.1 Under Ubuntu (Done this on 24.04.1)
```console
# Easiest way to install rustup under Ubuntu is:
$ sudo snap install rustup
```

#### 1.2 Under Windows
See [Rustup Installation](https://rustup.rs/)

#### 1.3 Under Mac
See [Rustup Installation](https://rustup.rs/)
See [Rust Other Installation Methods](https://forge.rust-lang.org/infra/other-installation-methods.html)


## 2. Once Rust is installed
```console
# For nightly builds: $ rustup toolchain install nightly
# automatically infers the platform
$ rustup toolchain install stable
$ rustup default stable
```

## 2.1 Install dependencies

#### 2.1.1 Under Ubuntu (Done this on 24.04.1)
´´´console
# On Ubuntu or Debian, install
$ sudo apt install libobs-dev
´´´

## 3. Build
```console
cargo build --release
```

## 4. Cross-Building
#### 4.1 Linux to Windows
```console
$ rustup toolchain install x86_64-pc-windows-gnu
$ cargo build --release --target x86_64-pc-windows-gnu
```

#### 4.2 Linux to MacOS
```console
$ docker run --rm -it -v $(pwd):/io -w /io ghcr.io/rust-cross/cargo-zigbuild   cargo zigbuild --release --target aarch64-apple-darwin
```

The docker container has everything installed, including the MacOS SDK, the cargo-zigbuild crate,
**except for the libobs.framework.**

You can get *a* libobs.framework from [https://github.com/obsproject/obs-studio/actions/runs](the OBS GitHub Actions),
map you have to map it into the container manually, copy it into the SDK/System/Library/Frameworks

Alternatively [https://github.com/tpoechtrager/osxcross](installing the SDK) also works,
but I have no idea how to get zigbuild to find the frameworks on the linux host
(don't forget to copy over the libobs.framework aswell)

#### Mentioned OSX Cross environments
- [Cargo-Zigbuild by Rust-Cross](https://github.com/rust-cross/cargo-zigbuild)
- [OSXCross by tpoechtrager](https://github.com/tpoechtrager/osxcross)

There's also this, which I didn't try
- [OSX Cross Docker Container](https://github.com/crazy-max/docker-osxcross)

#### Docker Links
- [Docker Linux Setup](https://docs.docker.com/desktop/setup/install/linux/)
- [Docker Engine Installation](https://docs.docker.com/engine/install/)
- [Docker Engine Installation Post-Install](https://docs.docker.com/engine/install/linux-postinstall/)