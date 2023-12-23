---
title: Cairo Hello World
date: 2023-10-01 15:49:25
tags:
---

现在你已经通过Scarb安装了Cairo，是时候编写你的第一个Cairo程序了。 在学习一门新语言时，传统的做法是写一个小程序 将文字Hello, world!打印到屏幕上，所以我们在这里也要这样做!

我们先创建一个工作区的目录
```bash
mkdir -p ~/workspace/cairo
cd ~/workspace/cairo
```

创建我们的第一个项目
```bash
scarb new hello_world
```
输出
```bash
Created `hello_world` package.
```

现在用我们的编辑器打开这个项目可以看到项目目录结构
<pre>
├── Scarb.toml
├── .gitignore
├── src
│   └── lib.cairo
</pre>

查看Scarb.toml的内容
```toml
[package]
name = "hello_world"
version = "0.1.0"
edition = "2023_10"

# See more keys and their definitions at https://docs.swmansion.com/scarb/docs/reference/manifest.html

[dependencies]
```

再看看lib.cairo的内容是个啥
```rust
fn main() -> felt252 {
    fib(16)
}

fn fib(mut n: felt252) -> felt252 {
    let mut a: felt252 = 0;
    let mut b: felt252 = 1;
    loop {
        if n == 0 {
            break a;
        }
        n = n - 1;
        let temp = b;
        b = a + b;
        a = temp;
    }
}

#[cfg(test)]
mod tests {
    use super::fib;

    #[test]
    fn it_works() {
        assert(fib(16) == 987, 'it works!');
    }
}
```

现在我们先编译试试看
```bash
scarb build
```
当然了，默认代码肯定是没有问题的，成功编译
不过还有一个问题没有解决，我们还没有语言提示，像是在notepad里面写代码一样，我们需要配置VSCode的Cairo插件，这样就可以有语言提示了

查看scarb的位置
```bash
find ~ -name scarb
```

可以看到输出了三个路径
```bash
~/.local/share/scarb-install/latest/bin/scarb
~/.local/bin/scarb
~/.cache/scarb
```
这里可以找到`~/.local/bin/scarb`
语言服务器也是他 直接填写就可以了
我们可以进行配置了
![](/Cairo-Hello-World/img_1.jpg)

配置完成后，我们可以看到语言提示了
![](/Cairo-Hello-World/img_2.jpg)

现在咱们开始下一步动作, 我们先删除lib.cairo里面的内容，然后写入以下内容
```rust
mod hello_world;
```
新建文件`src/hello_world.cairo`,并将以下代码放入其中
```rust
fn main() {
    println!("Hello, World!");
}
```
好了，现在我们可以编译了
```bash
scarb build
```
输出
```bash
Compiling hello_world v0.1.0 (file:///projects/Scarb.toml)
 Finished release target(s) in 4 seconds
```
说明编译没问题，让我们执行一下试试看呢
```bash
scarb cairo-run --available-gas=200000000
```
可以看到输出
```bash
   Compiling hello_world v0.1.0 (file:///projects/Scarb.toml)
    Finished release target(s) in 4 seconds
     Running hello_world
Run completed successfully, returning [987]
Remaining gas: 199953640
```
无论你的操作系统如何，终端里都应该打印出字符串Hello, world!。
如果 "Hello，world！"打印出来了，那么恭喜你！你已经正式写了一个Cairo程序！ 你已经成为了一名Cairo程序员--欢迎!