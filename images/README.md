# 容器镜像服务

用**容器镜像**开发属于比较贴近自动化构建的方案，既不会导致本身机器的环境被破坏，同时也更好的支持多并发。

这里存放两种 Rust 项目类型的容器镜像 `Cargo 项目` 和 `Rust 项目`。

## Cargo 项目

**搭建 Cargo 项目的容器镜像有两种方案**：

1. 基于 Rustup 搭建 Rust 环境，由于安装了 rustup, 此方案也便于后续直接在容器镜像内进行版本管理。

2. 基于 Rustup 中心仓提供的离线包进行搭建，此方案适用于版本固定的开发环境。

## Rust 项目

**在 Rust 官方项目中提供四个等级的目标产物**：

- Tier 1 with Host Tools（带有主机工具一级产物）
- Tier 2 with Host Tools（带有主机工具二级产物）
- Tier 2 without Host Tools（不带有主机工具二级产物、一般只有标准库）
- Tier 3（不带有主机工具三级产物、一般只有标准库）

根据[官方的申明](https://doc.rust-lang.org/nightly/rustc/platform-support.html#tier-1-with-host-tools)，其中 Rust 社区只对 Tier 1 的目标产物做质量保证，因此这里我们也重点介绍 tier 1 的目标产物环境搭建过程。

后续也会补充 tier 2 中 OHOS（鸿蒙）相关目标产物的构建环境搭建过程。
