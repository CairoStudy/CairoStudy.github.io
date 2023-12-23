---
title: Set up cairo development environment
date: 2022-12-01 15:33:46
tags:
---


# 安装
我手里没有mac电脑，这里我们使用ubuntu系统来安装cairo开发环境。
首先SSH连接到服务器, 我是有一台局域网服务器
```bash
ssh root@ 192.168.2.200
#输入你的密码
```
然后我们执行以下命令
```bash
curl --proto '=https' --tlsv1.2 -sSf https://docs.swmansion.com/scarb/install.sh | sh
```
应该会输出

```bash
scarb-install: retrieving latest version from https://github.com/software-mansion/scarb...
scarb-install: downloading scarb-v2.4.1-x86_64-unknown-linux-gnu.tar.gz...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
100 29.6M  100 29.6M    0     0  6391k      0  0:00:04  0:00:04 --:--:-- 9465k
scarb-install: installed scarb to /home/0xstark/.local/share/scarb-install/latest
scarb-install: created symlink /home/0xstark/.local/bin/scarb -> /home/0xstark/.local/share/scarb-install/latest/bin/scarb

Detected your preferred shell is bash and added '$HOME/.local/bin' to PATH. Run 'source /home/0xstark/.bashrc' or start a new terminal session to use Scarb.
Then, run 'scarb --version' to verify your installation. Happy coding!
```
然后我们执行
```bash
scarb --version
```
会提示命令不存在，我们需要引用一下环境变量设置
```bash
source /home/0xstark/.bashrc
```
再次执行就可以正确输出
```bash
scarb 2.4.1 (c93ee6249 2023-12-21)
cairo: 2.4.1 (https://crates.io/crates/cairo-lang-compiler/2.4.1)
sierra: 1.4.0
```
如果无法正确输出，那就检查一下是否在下载过程中出错或者环境变量不正确


# 安装 VSCode 扩展
开发工具我们选择[VsCode](https://code.visualstudio.com/) 免费，而且有插件可进行提示
大家选择对应版本进行安装即可
插件我们使用[cairo 1.0](https://marketplace.visualstudio.com/items?itemName=starkware.cairo1)直接安装即可
安装后，进入扩展设置，并确保勾选Enable Language Server 和Enable Scarb选项。

# 总结
这样我们就为cairo的开发环境搭建完成了，下一篇我们将讲解cairo语法