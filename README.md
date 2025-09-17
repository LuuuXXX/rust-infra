# Rust 基础设施介绍

项目介绍了一下 Rust 基础设施相关的知识点，包括当不限于，[Rust 基础设施知识文档](docs/README.md)、[Rust 构建镜像](images/README.md)以及[通用的流水线知识](pipeline/README.md)。

目录结构如下：
- docs
    - 基础储备
        - 1. Rust 中心仓概念及使用方法
    - Cargo 项目构建
        - 1. 搭建 Rust-Cargo 项目的版本构建镜像.md
        - 2. 结合已有的 CICD 搭建属于自己的 Rust-Cargo 项目构建环境
    - Rust 源码构建
        - 1. Rust 发布包的来历
        - 2. Rust 发布包的组成
        - 3. Rust 发布包的构建过程（构建系统 bootstrap）
        - 4. 搭建 Rust-Src 项目的版本构建镜像
        - 5. 结合已有的 CICD 搭建属于自己的 Rust-Src 项目构建环境
- images
    - Cargo 项目构建镜像
    - Rust 源码构建镜像
- pipeline
    - CodeArts
    - Github Action

**欢迎补充、纠错。**