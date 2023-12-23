---
title: Cairo Lang Syntax
date: 2023-09-21 22:40:52
tags:
---

完成了hello world的编写, 接下来让我们从头了解一下`cairo`语法

## 变量

与大多数语言不同的是Cairo 分为了两种变量, 一种是可变变量, 一种是不可变变量
让我们新开一个项目试试看

```bash
scarb new variables 
```

修改`src/lib.cairo`文件
cairo使用let声明变量
例如

- let a = 1; 这里我们声明了一个不可变变量a, 值为1
- let b = 2;
- let mut c = 3; 这里我们声明了一个可变变量c, 值为3
- let mut d = 4;
  这些声明都是正确的, 且可以被正确运行的，让我们试试看

```rust
fn main() {
    let a = 1;
    let b = 2;
    let mut c = 3;
    let mut d = 4;
    println!("a = {}", a);
    println!("b = {}", b);
    println!("c = {}", c);
    println!("d = {}", d);
}
```

运行试试看会遇到什么不同的情况

```bash
scarb cairo-run --available-gas=200000000
```

那让我们尝试一下修改变量的值试试

```rust
fn main() {
    let a = 1;
    a = 2;
    println!("a = {}", a);
}
```

![](/Cairo-Hello-World/img_1.jpg)
运行会发现提示

```bash
   Compiling variables v0.1.0 (/home/0xstark/workspace/cairo/variables/Scarb.toml)
error: Cannot assign to an immutable variable.
 --> /home/0xstark/workspace/cairo/variables/src/lib.cairo:3:5
    a = 2;
    ^***^


error: could not compile `variables` due to previous error
Error: `scarb metadata` exited with error
```

这里提示我们不能修改不可变变量, 那我们修改一下代码, 只有用mut修饰的变量才可进行重新赋值
让我们修改一下

```rust
fn main() {
    let mut a = 1;
    a = 2;
    println!("a = {}", a);
}
```

加上mut的修饰，我们发现可以正常运行代码了，是的, cairo是使用Rust语法，所以在这里和其他的语言相差会比较大，需要多熟悉理解一下

### 常量

常量是不可变的变量，与变量不同的是，常量必须在声明时就赋值，且不能使用mut修饰
Cairo的常量命名规则是使用所有大写字母，单词之间使用下划线。

```rust
const ONE_HOUR_IN_SECONDS: u32 = 3600;
```

### 隐藏

```rust
fn main() {
    let x = 10;
    let x = x + 1;
    {
        let x = x * 2;
        println!("Inner scope x value is: {}", x);
    }
    println!("Outer scope x value is: {}", x);
}
```

运行可得到

```bash
   Compiling variables v0.1.0 (/home/0xstark/workspace/cairo/variables/Scarb.toml)
    Finished release target(s) in 4 seconds
   Compiling variables v0.1.0 (/home/0xstark/workspace/cairo/variables/Scarb.toml)
    Finished release target(s) in 4 seconds
     Running variables
Inner scope x value is: 22
Outer scope x value is: 11
Run completed successfully, returning []
Remaining gas: 199608300
```

由此可以看出，cairo是支持隐藏的，这里的x是不同的变量，不同的作用域，不同的值

# 数据类型

和solidity一样，cairo也是强类型语言，但是cairo的数据类型比solidity要严格很多

上述变量我们还未对数据类型进行说明，cairo有以下数据类型

### 标量类型

标量类型代表一个单独的值。Cairo 有三种基本的标量类型：

- felts
- 整数
- 布尔值

##### felts类型

是在你未指定类型，那么默认就是一个`felt252`

##### 整数类型

| Length  | 	Unsigned |
|---------|-----------|
| 8-bit   | 	u8       |
| 16-bit  | 	u16      |
| 32-bit  | 	u32      |
| 64-bit  | 	u64      |
| 128-bit | 	u128     |
| 256-bit | 	u256     |
| 32-bit  | 	usize    |

Cairo 的整数类型字面值

| Numeric literals | 	Example    |
|------------------|-------------|
| Decimal          | 	98222      |
| Hex              | 	0xff       |
| Octal            | 	0o77       |
| Binary           | 	0b11110000 |

数值运算
```rust
fn main() {
    let a = 1_u128 + 2_u128;
    let b = 1_u128 - 2_u128;
    let c = 1_u128 * 2_u128;
    let d = 1_u128 / 2_u128;
    let e = 1_u128 % 2_u128;
    println!("a = {}", a);
    println!("b = {}", b);
    println!("c = {}", c);
    println!("d = {}", d);
    println!("e = {}", e);
}
```
运行发现报错
```bash
Compiling variables v0.1.0 (/home/0xstark/workspace/cairo/variables/Scarb.toml)
Finished release target(s) in 4 seconds
Running variables
Run panicked with [39878429859763533771555484554338820190071 ('u128_sub Overflow'), ].
Remaining gas: 199368300
```
我们来找到原因因为`1_u128 - 2_u128`这里的值是负数，而cairo不支持负数，所以会报错，那我们修改一下代码
```rust
fn main() {
    let a = 1_u128 + 2_u128;
    let b = 1_u128 - 1_u128;
    let c = 1_u128 * 2_u128;
    let d = 1_u128 / 2_u128;
    let e = 1_u128 % 2_u128;
    println!("a = {}", a);
    println!("b = {}", b);
    println!("c = {}", c);
    println!("d = {}", d);
    println!("e = {}", e);
}
```
以下是结果输出
```bash
   Compiling variables v0.1.0 (/home/0xstark/workspace/cairo/variables/Scarb.toml)
    Finished release target(s) in 4 seconds
     Running variables
a = 3
b = 0
c = 2
d = 0
e = 1
Run completed successfully, returning []
Remaining gas: 199215600
```
##### 布尔类型
```rust
fn main() {
    let a = true;
    let b: bool = false; // with explicit type annotation
}
```
主要用于判断作用, 这个无需多讲解

>短字符串类型
>Cairo 没有字符串（String）的原生类型，但你可以在 felt252 中存储短字符，形成我们所说的 "短字符串"。一个短字符串的最大长度为 31 个字符。这是为了确保它能装入一个 felt （一个 felt 是252位，一个 ASCII 字符是 8 位）
```rust
fn main() {
    let the_char = 'C';
    let the_string = 'Hello world';
    println!("the_char = {}", the_char);
    println!("the_string = {}", the_string);
}
```
打印之后我们可以得到
```bash
   Compiling variables v0.1.0 (/home/0xstark/workspace/cairo/variables/Scarb.toml)
    Finished release target(s) in 4 seconds
     Running variables
the_char = 67
the_string = 87521618088882671231069284
Run completed successfully, returning []
Remaining gas: 198973730
```


