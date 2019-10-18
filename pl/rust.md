# rust

## 环境搭建

## 项目管理

rust自带非常好用的项目管理工具Cargo

- 新建项目

    ```shell
    cargo new rust-sample
    ```

项目的目录结构

    ```content
        
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
