# 文档

这里主要总结了目前用 Rust 进行开发所涉及的一些基础设施相关的文档方面的内容，其中比较特别的是 Rust 官方项目（一切 Rust 项目的起点，用于构建官方的 Rust 工具链），且会单独展开介绍其中的内容。

## 必要的知识点

### 中心仓

中心仓是 Rust 官方社区提供的为 Rust 开发者们提供的文件存储服务，对于绝大部分 Rust 开发者，在日常的使用过程中会涉及到两个中心仓：

#### 1. Rustup 中心仓

- **提供方**：Rust 官方社区。

- **提供服务**：供 Rust 开发者下载 Rust 官方工具链的存储仓。

- **官方地址**：`https://static.rust-lang.org/dist/<date>`

- **使用方式**：rustup 安装的时候自动会从该中心仓地址下载对应的包。

#### 2. Crates.io 中心仓

- **提供方**：Rust 官方社区。

- **提供服务**：供 Rust 开发者上传、下载三方库的存储仓，并提供接口文档。

- **官方地址**：`https://crates.io/`

- **使用方式**：在 Cargo 项目中通过依赖配置文件导入，Cargo 项目构建时会自动下载对应版本的三方库。

## Cargo 项目

Cargo 是官方的 Rust 项目包管理工具，其底层核心是通过调用 rustc 来进行编译，提供了重要的依赖管理能力。

详细的 Cargo 教程可以参考官方的文档。

- 官方：[cargo book](https://crates.io/)

- 中文：[cargo 手册](https://rustwiki.org/zh-CN/cargo/)

## Rust 项目

Rust 项目是官方开源的项目，每六周发布一个版本（如果有漏洞可能会提前发布补丁版本，如 1.72.1）。

Rust 项目是一个大的混合项目，包括一下几个组件（后续版本可能会更改）：
- **compiler**
    - rust 编译器前端代码，最终编译产物为 rustc。
- **library**
    - rust 提供的官方的标准库，测试库等。最终编译产物为：标准库，测试库的动态链接库。
- **src**
    - bootstrap - 版本构建核心工具
    - build-help - 辅助版本构建的工具
    - ci - 流水线相关的一下配置及脚本
    - doc - 官方文档的存储地址
    - etc - 一些杂项脚本及安装辅助工具
    - tools - 会集成到官方安装工具包的三方工具，如clippy、cargo、fmt。
    - gcc\llvm-projetc - 编译器后端代码的软连接，用于生成后端相关的库。
- **tests**
    - Rust 项目的集成测试套件，包括编译器、标准库、部分工具的测试（功能测试、性能测试）。

有关 Rust 特性的文档可以参考：

- 官方：[rustc book](https://doc.rust-lang.org/book/)

- 中文：[Rust 程序设计语言](https://rustwiki.org/zh-CN/book/)
