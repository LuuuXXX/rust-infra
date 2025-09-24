# aarch64-unknown-linux-gnu

| target | notes |
| ------ | ----- |
| aarch64-pc-windows-msvc | ARM64 Windows MSVC |

## 平台限制

**支持的系统最低版本**

- windows 10 或更高版本

**从源码构建 Rust 工具链要求主机工具链最低版本**

- 最小支持版本 `Visual Studio 2017`，推荐用 `Visual Studio 2022`。

## 构建流程

构建流程依赖 bootstrap 及构建脚本，这里列举了构建该目标所设定的环境

参考链接 1.90.0 版本：https://github.com/rust-lang/rust/blob/1159e78c4747b02ef996e55082b704c09b970588/src/ci/github-actions/jobs.yml#L656-L666

```yml
RUST_CONFIGURE_ARGS: >-
    --build=aarch64-pc-windows-msvc
    --host=aarch64-pc-windows-msvc
    --target=aarch64-pc-windows-msvc,arm64ec-pc-windows-msvc
    --enable-full-tools
    --enable-profiler
SCRIPT: python x.py dist bootstrap --include-default-paths
DIST_REQUIRE_ALL_TOOLS: 1
```