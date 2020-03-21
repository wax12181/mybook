# rust

## 环境搭建

1. [rust安装指南](https://www.rust-lang.org/zh-CN/tools/install)

2. 使用USTC(中科大镜像源)，加速rust安装

    ```shell
    export RUSTUP_DIST_SERVER=https://mirrors.ustc.edu.cn/rust-static
    export RUSTUP_UPDATE_ROOT=https://mirrors.ustc.edu.cn/rust-static/rustup
    ```

3. rust发布版本，使用rustup进行管理

    - Nightly
    - Beta
    - Stable

    Nightly 版本指的是每天更新一次。每隔六周，Nightly 版本会晋升为 “Beta” 版。在这一点上，它只会收到补丁修复严重错误。六周后，Beta 版提升为 “Stable” 版，并成为下一个 1. x 版本。

    这个过程是平行地发生的。所以每隔六周的同一天，Nightly 变成 Beta，Beta 变成 Stable。当 1.x 版本发布时，与此同时，1.(x + 1)-beta 也被发布，Nightly 版本变成第一个 1.(x + 2)-nightly 版。

    一般来说，除非你有一个特别的原因，你应该使用stable 发行版。这些版本是针对大众的。

    然而，Rust 中那取决于你的兴趣，你可以选择使用nightly 版本。基本的权衡是这样的：在 nightly 通道中，您可以使用不稳定，新的 Rust 特性。然而，不稳定的特性易于改变，所以新的 nightly 版本发布时可能会破坏你的代码。如果你使用 stable 版本，你不能使用实验特性，但 Rust 的下一版本重大的变化不会造成严重的问题。

4. 使用USTC加速rust crates镜像

    - 在 $HOME/.cargo/config 中添加如下内容

    ```content
    [registry]
    index = "git://mirrors.ustc.edu.cn/crates.io-index"
    ```

    如果所处的环境中不允许使用 git 协议, 可以把上述地址改为

    ```content
    index = "http://mirrors.ustc.edu.cn/crates.io-index"
    ```

    同步频率为每两个小时更新一次.

    - 如果 cargo 版本为 0.13.0 或以上, 需要更改 $HOME/.cargo/config 为以下内容:

    ```content
    [source.crates-io]
    registry = "https://github.com/rust-lang/crates.io-index"
    replace-with = 'ustc'
    [source.ustc]
    registry = "git://mirrors.ustc.edu.cn/crates.io-index"
    ```

## 项目管理

rust自带非常好用的项目管理工具Cargo

- 新建项目

    ```shell
    cargo new rust-sample
    ```

- 项目的目录结构

    ```content
    ├── Cargo.toml
    ├── src
    |   └── main.rs
    └── tests
        └── test.rs
    ```

- 依赖管理

1. rust使用Cargo管理依赖，在Cargo.toml中设置

    ```toml
    [dependencies]
    #依赖本地，适用于依赖项在项目内
    hyper-utls = { path = "../hyper-utls" }
    # 依赖git仓库，适用于依赖项在项目外
    hyper-utls= { git = "${仓库URL地址}", branch = "master" }
    # 依赖crates-io库中二进制文件
    hyper-utls=1.0.0

    [patch.crates-io]
    #调试本地依赖项代码变更时使用，可以覆盖dependencies中的依赖
    hyper-utls = { path = "../hyper-utls" }
    # 调试非本地依赖项代码变更时使用，可以覆盖dependencies中的依赖
    hyper-utls= { git = "${仓库URL地址}", branch = "master" }
    ```

    注意事项

    - 使用SSH方式进行git仓库依赖设置，需要在本地开发环境下配置SSH

        1. 添加`~/.ssh/config`，并写入如下内容

        ```context
        Host *
            UseKeychain yes
            AddKeysToAgent yes
            IdentityFile ~/.ssh/id_rsa
        ```

        2. 指定私钥文件

        ```shell
        ssh-agent bash
        ssh-add -k ~/.ssh/id_rsa
        ```

## 测试

### 单元测试

一般在源代码文件内进行测试用例的编写，例子如下

```rust
#[cfg(test)]
mod tests {
    #[test]
    fn test_case_001() {
        assert_eq!(2 + 2, 4);
    }
}
```

### 集成测试

编写集成测试，需要在项目根目录创建一个`tests`目录，与`src`同级。Cargo知道如何去寻找这个目录中的集成测试文件。接着可以随意在这个目录中创建任意多的测试文件，Cargo会将每一个文件当作单独的crate来编译。

集成测试中某一个测试文件例子：

```rust
use adder;

#[test]
fn it_adds_two() {
    assert_eq!(4, adder::add_two(2));
}

```

## 变量和类型

### 指针

- `Box<T>` 指向类型T的、具有所有权的指针，有权释放内存
- `&T` 指向类型T的借用指针，也称为引用，无权释放内存，无权写数据
- `&mut T` 指向类型T的mut型借用指针，无权释放内存，有权写数据
- `*const T` 指向类型T的只读裸指针，没有生命周期信息，无权写数据
- `*mut T` 指向类型T的可读写裸指针，没有生命周期信息，有权写数据
- `Rc<T>` 指向类型T的引用计数指针，共享所有权，线程不安全
- `Arc<T>` 指向类型T的原子型引用计数指针，共享所有权，线程安全
- `Cow<'a, T>` Clone-on-write, 写时复制指针。可能是借用指针，也可能是具有所有权的指针

### 内存安全
