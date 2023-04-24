# Rust bindings to **nix** APIs

[![Cirrus Build Status](https://api.cirrus-ci.com/github/nix-rust/nix.svg)](https://cirrus-ci.com/github/nix-rust/nix)
[![crates.io](https://img.shields.io/crates/v/nix.svg)](https://crates.io/crates/nix)

[Documentation (Releases)](https://docs.rs/nix/)

Nix试图为各种*nix平台的API提供友好的绑定（Linux、Darwin、...)。对于许多系统API，Nix提供了一个安全的替代方案，以取代[libc crate](https://github.com/rust-lang/libc)所暴露的不安全API。 具体做法是用类型/抽象来包装libc的功能，强制执行合法、安全的使用。

Nix提供一个例子对比与libc系统调用的区别
[gethostname](https://man7.org/linux/man-pages/man2/gethostname.2.html)：

```rust,ignore
// libc api (unsafe, requires handling return code/errno)
pub unsafe extern fn gethostname(name: *mut c_char, len: size_t) -> c_int;

// nix api (returns a nix::Result<OsString>)
pub fn gethostname() -> Result<OsString>;
```
## 使用
在"BUILD.gn"中使用deps字段添加对num-traits的crates的依赖，例如：

```BUILD.gn
ohos_rust_shared_library("foo") {
  source = [ "src/lib.rs" ]
  deps = [ "//third_party/rust/crates/nix:lib" ]
}
```

## Minimum Supported Rust Version (MSRV)

nix在Rust 1.56.1及更高版本上得到支持。

## License

Nix使用MIT License。 更多细节见[LICENSE](LICENSE)。
