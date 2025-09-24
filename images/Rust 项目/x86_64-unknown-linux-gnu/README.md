# x86_64-unknown-linux-gnu

| target | notes |
| ------ | ----- |
| x86_64-unknown-linux-gnu | 64-bit Linux (kernel 3.2+, glibc 2.17+) |

## 平台限制

**支持的系统最低版本**

无相关文档

**从源码构建 Rust 工具链要求主机工具链最低版本**

无相关文档

## 构建流程

构建流程依赖 bootstrap 及构建脚本，这里列举了构建该目标所设定的环境

参考链接 1.90.0 版本：https://github.com/rust-lang/rust/blob/1159e78c4747b02ef996e55082b704c09b970588/src/ci/github-actions/jobs.yml#L94-L100

```yml
CODEGEN_BACKENDS: llvm,cranelift
DOCKER_SCRIPT: dist.sh
```