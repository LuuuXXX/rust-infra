# Cargo 项目交叉编译

Cargo 常常涉及构建不同平台目标产物，也就是交叉编译常见。

Rust 实现交叉编译，需要准备两个内容：

1. Rust 侧：提供交叉编译目标平台的标准库。

2. 平台侧：提供交叉编译目标平台链接器，用于链接生成对应平台的二进制。

## 基本流程如下

此处举例为：
Host 机器架构为 x86_64 的环境交叉编译 arm64 OHOS 版本目标产物。

[参考文档](https://doc.rust-lang.org/rustc/platform-support/openharmony.html)

### 前期环境准备

1. 添加目标平台标准库

    **在线安装**

    ```shell
    rustup target add aarch64-unknown-linux-ohos
    ```

    **离线安装（需要 rust 工具链也是离线安装）**

    ```shell
    wget https://static.rust-lang.org/dist/2025-08-07/rust-std-1.89.0-aarch64-unknown-linux-ohos.tar.gz
    tar zxvf rust-std-1.89.0-aarch64-unknown-linux-ohos.tar.gz
    cd rust-std-1.89.0-aarch64-unknown-linux-ohos
    sh install.sh --prefix=/path/to/install
    ```

2. 添加对应平台链接器

    **下载`ohos-sdk`**

    ```shell
    curl https://repo.huaweicloud.com/openharmony/os/5.0.0-Release/ohos-sdk
    mkdir /opt/ohos-sdk
    cd /opt/ohos-sdk
    unzip -qq /tmp/linux/native-linux-x64-5.0.0.71-Release.zip
    rm /tmp/linux/native-linux-x64-5.0.0.71-Release.zip
    ```

    **添加链接器`aarch64-unknown-linux-ohos-clang.sh`到`usr/local/bin`目录**

    ```shell
    #!/bin/sh
    exec /opt/ohos-sdk/linux/native/llvm/bin/clang \
      -target aarch64-linux-ohos \
      --sysroot=/opt/ohos-sdk/linux/native/sysroot \
      -D__MUSL__ \
      "$@"
    ```

### 交叉编译配置

**为项目的`config.toml`配置文件添加配置**

```toml
[target.aarch64-unknown-linux-ohos]
ar="/opt/ohos-sdk/native/llvm/bin/llvm-ar"
linker="/usr/local/bin/aarch64-unknown-linux-ohos.sh"
```

### 执行交叉编译

**执行构建**

```
cargo build --target aarch64-unknown-linux-ohos
```

**构建输出**

通过 file 执行进行初步检查
