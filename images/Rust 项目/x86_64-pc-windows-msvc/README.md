# x86_64-pc-windows-msvc

| target | notes |
| ------ | ----- |
| x86_64-pc-windows-msvc | 64-bit MSVC (Windows 10+, Windows Server 2016+) |

## 平台限制

**支持的系统最低版本**

- windows 10 或更高版本

**从源码构建 Rust 工具链要求主机工具链最低版本**

- 最小支持版本 `Visual Studio 2017`，推荐用 `Visual Studio 2022`。

## 构建流程

构建流程依赖 bootstrap 及构建脚本，这里列举了构建该目标所设定的环境

参考链接 1.90.0 版本：https://github.com/rust-lang/rust/blob/1159e78c4747b02ef996e55082b704c09b970588/src/ci/github-actions/jobs.yml#L629-L641

```yml
RUST_CONFIGURE_ARGS: >-
    --build=x86_64-pc-windows-msvc
    --host=x86_64-pc-windows-msvc
    --target=x86_64-pc-windows-msvc
    --enable-full-tools
    --enable-profiler
    --set rust.codegen-units=1
SCRIPT: python x.py build --set rust.debug=true opt-dist && PGO_HOST=x86_64-pc-windows-msvc ./build/x86_64-pc-windows-msvc/stage0-tools-bin/opt-dist windows-ci -- python x.py dist bootstrap --include-default-paths
DIST_REQUIRE_ALL_TOOLS: 1
CODEGEN_BACKENDS: llvm,cranelift
```