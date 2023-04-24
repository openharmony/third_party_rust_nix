# Rust bindings to **nix** APIs

[![Cirrus Build Status](https://api.cirrus-ci.com/github/nix-rust/nix.svg)](https://cirrus-ci.com/github/nix-rust/nix)
[![crates.io](https://img.shields.io/crates/v/nix.svg)](https://crates.io/crates/nix)

[Documentation (Releases)](https://docs.rs/nix/)

Nix试图为各种*nix平台的API提供友好的绑定（Linux、Darwin、
...). 我们的目标不是提供一个100%统一的接口，而是统一
同时仍然提供平台特定的API。

对于许多系统API，Nix提供了一个安全的替代方案，以取代[libc crate]暴露的不安全的API。
[libc crate](https://github.com/rust-lang/libc)所暴露的不安全API。 具体做法是
用类型/抽象来包装libc的功能，强制执行合法/安全的
使用。


作为Nix提供的一个例子，检查一下
的不同之处。
[gethostname](https://man7.org/linux/man-pages/man2/gethostname.2.html) 系统调用的区别
调用：

```rust,ignore
// libc api (unsafe, requires handling return code/errno)
pub unsafe extern fn gethostname(name: *mut c_char, len: size_t) -> c_int;

// nix api (returns a nix::Result<OsString>)
pub fn gethostname() -> Result<OsString>;
```

## 支持的平台

nix的目标支持由两层组成。虽然 nix 试图支持所有
[libc](https://github.com/rust-lang/libc)所支持的所有平台，但由于技术或人力原因，只有一些
由于技术或人力的限制，只有部分平台被积极支持。对平台的支持分为三个层级：

  * 第1层 - 该目标的构建和测试在CI中运行。如果其中任何一个失败
             阻止新代码的加入。
  * 第2层--该目标的构建在CI中运行。在构建过程中出现的故障
             阻止了新代码的加入。测试可以被运行，但测试中的失败
             但测试中的失败不会阻止新代码的加入。
  * 第3层 - 该目标的构建在CI中运行。构建过程中的失败
             *不*阻碍新代码的加入。测试可以被运行，但
             测试中的失败不会阻止新代码的加入。

以下目标由 "nix "支持：

第1层：
  * aarch64-apple-darwin
  * aarch64-unknown-linux-gnu
  * arm-unknown-linux-gnueabi
  * armv7-unknown-linux-gnueabihf
  * i686-unknown-freebsd
  * i686-unknown-linux-gnu
  * i686-unknown-linux-musl
  * mips-unknown-linux-gnu
  * mips64-unknown-linux-gnuabi64
  * mips64el-unknown-linux-gnuabi64
  * mipsel-unknown-linux-gnu
  * powerpc64le-unknown-linux-gnu
  * x86_64-unknown-freebsd
  * x86_64-unknown-linux-gnu
  * x86_64-unknown-linux-musl

第2层：
  * aarch64-apple-ios
  * aarch64-linux-android
  * arm-linux-androideabi
  * arm-unknown-linux-musleabi
  * armv7-linux-androideabi
  * i686-linux-android
  * powerpc-unknown-linux-gnu
  * s390x-unknown-linux-gnu
  * x86_64-apple-ios
  * x86_64-linux-android
  * x86_64-apple-darwin
  * x86_64-unknown-illumos
  * x86_64-unknown-netbsd

第3层：
  * armv7-unknown-linux-uclibceabihf
  * x86_64-fuchsia
  * x86_64-unknown-dragonfly
  * x86_64-unknown-haiku
  * x86_64-unknown-linux-gnux32
  * x86_64-unknown-openbsd
  * x86_64-unknown-redox

## 最低支持的Rust版本(MSRV)

nix在Rust 1.56.1及更高版本上得到支持。 它的MSRV将不会
它的MSRV在未来不会被改变而不需要增加主版本或次版本。

## 贡献

我们非常欢迎投稿。 请参见 [CONTRIBUTING](CONTRIBUTING.md) 了解更多细节。
更多细节。

欢迎加入我们在Gitter上的[nix-rust/nix](https://gitter.im/nix-rust/nix)频道，以便
讨论 "nix "开发。

## 许可

Nix在MIT许可下被授权。 更多细节见[LICENSE](LICENSE)。
