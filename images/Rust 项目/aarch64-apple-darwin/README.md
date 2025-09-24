# aarch64-apple-darwin

| target | notes |
| ------ | ----- |
| aarch64-apple-darwin | ARM64 macOS (11.0+, Big Sur+) |

## 平台限制

**支持的系统最低版本**

- ARM64 macOS 11.0 Big Sur

**使用 Rust 工具链要求主机工具链最低版本**

- Xcode 9.2

**从源码构建 Rust 工具链要求主机工具链最低版本**
(for LLVM 19)
- macOS 10.13
- Xcode 10.0

**二进制格式**

- 默认格式为 `Mach-O`

## 构建流程

构建流程依赖 bootstrap 及构建脚本，这里列举了构建该目标所设定的环境

参考链接 1.90.0 版本：https://github.com/rust-lang/rust/blob/1159e78c4747b02ef996e55082b704c09b970588/src/ci/github-actions/jobs.yml#L477-L499

```yml
SCRIPT: ./x.py dist bootstrap --include-default-paths --host=aarch64-apple-darwin --target=aarch64-apple-darwin
RUST_CONFIGURE_ARGS: >-
    --enable-full-tools
    --enable-sanitizers
    --enable-profiler
    --set rust.jemalloc
    --set llvm.ninja=false
    --set rust.lto=thin
    --set rust.codegen-units=1
SELECT_XCODE: /Applications/Xcode_15.4.app
USE_XCODE_CLANG: 1
MACOSX_DEPLOYMENT_TARGET: 11.0
MACOSX_STD_DEPLOYMENT_TARGET: 11.0
NO_LLVM_ASSERTIONS: 1
NO_DEBUG_ASSERTIONS: 1
NO_OVERFLOW_CHECKS: 1
DIST_REQUIRE_ALL_TOOLS: 1
CODEGEN_BACKENDS: llvm,cranelift
```