# Cargo 项目构建流程

详细的 Cargo 功能特性建议熟读 [Cargo 手册](https://rustwiki.org/zh-CN/cargo/)。

这里不介绍项目逻辑部分，只介绍常见的几个内容：
- 1. 创建 Cargo 项目（二进制，库）。
- 2. 依赖管理（单一项目，组合项目-workspace）。
- 3. 配置文件（config.toml）

## 1. 创建 Cargo 项目

- **创建二进制项目**

```shell
cargo new <crate-name>
```

- **创建库项目**，库项目最终的[生成格式可以通过 Cargo.toml 进行修改](https://doc.rust-lang.org/cargo/reference/cargo-targets.html?highlight=rlib#the-crate-type-field)。

```shell
cargo new <crate-name> --lib
```

## 2. 依赖管理

对于 Cargo 项目而言，依赖管理主要是基于项目根目录的 `Cargo.toml` 文件，内容可以参考：[Cargo 依赖管理](https://doc.rust-lang.org/cargo/guide/dependencies.html).

常见格式如下：

```toml
[dependencies]
time = "0.1.12"
```

## 3. 配置文件

对于 Cargo 项目而言，Cargo 会去逐层寻找 `config.toml` 文件作为构建当前项目的全局配置文件，顺序依次是：
1. 当前项目的 `.cargo/config.toml`
2. Cargo HOME目录的 `$CARGO_HOME/.cargo/config.toml`
3. 当前用户的 `$HOME/.cargo/config.toml`
4. root 用户的 `/root/.cargo/config.toml`
当有多个配置时，Cargo 项目会使用最上层的配置文件来作为当前项目的全局配置文件。

常见的配置如下，更多配置可以参考[官方文档](https://doc.rust-lang.org/cargo/reference/config.html)：

> 配置文件一般常用来指定 `crates.io` 镜像，编译链接器等全局配置。
> 对于国内用户，可以直接使用如下配置来加速获取三方库资源：

- 中国旋武社区
```toml
[source.crates-io]
replace-with = 'xuanwu-sparse'
[source.xuanwu]
registry = "https://mirror.xuanwu.openatom.cn/crates.io-index"
[source.xuanwu-sparse]
registry = "sparse+https://mirror.xuanwu.openatom.cn/index/"
[registries.xuanwu]
index = "https://mirror.xuanwu.openatom.cn/crates.io-index"
[net]
git-fetch-with-cli = true
```

- rsproxy - 字节镜像
```toml
[source.crates-io]
replace-with = 'rsproxy-sparse'
[source.rsproxy]
registry = "https://rsproxy.cn/crates.io-index"
[source.rsproxy-sparse]
registry = "sparse+https://rsproxy.cn/index/"
[registries.rsproxy]
index = "https://rsproxy.cn/crates.io-index"
[net]
git-fetch-with-cli = true
```