---
title: Install Cairo
date: 2023-08-05 15:31:03
tags:
---

# 安装
只需下载 Scarb，即可安装 Cairo。Scarb 将 Cairo 编译器和 Cairo 语言服务器捆绑在一个易于安装的软件包中，这样你就可以立即开始编写 Cairo 代码了。

Scarb同样是Cairo的软件包管理器，在很大程度上受到Cargo的启发，Rust的构建系统和软件包管理器。

Scarb会为你处理很多任务，比如构建你的代码（纯Cairo或Starknet合约），为你下载你的代码所依赖的库并构建他们，以及为VSCode Cairo 1扩展提供LSP支持。

如果你使用 Scarb 启动项目，管理外部代码和依赖关系就会容易得多。

让我们从安装Scarb开始。

### 安装Scarb
#### 要求
Scarb需要PATH环境变量里有一个Git可执行文件。

#### 安装
要安装 Scarb，请参阅 安装说明。我们强烈建议您通过 asdf 来安装Scarb 。 这一个 CLI 工具，可以按项目管理多个语言运行时版本。 这将确保您用于处理项目的 Scarb 版本始终与项目设置中定义的版本匹配，从而避免导致版本不匹配的问题。 否则，您只需在终端中运行以下命令，然后按照屏幕上的说明进行操作即可。这将安装 Scarb 的最新稳定版本。

curl --proto '=https' --tlsv1.2 -sSf https://docs.swmansion.com/scarb/install.sh | sh
Verify installation by running the following command in new terminal session, it should print both Scarb and Cairo language versions, e.g:
$ scarb --version
scarb 2.4.0 (cba988e68 2023-12-06)
cairo: 2.4.0 (https://crates.io/crates/cairo-lang-compiler/2.4.0)
sierra: 1.4.0
#### 安装 VSCode 扩展
Cairo 有一个 VSCode 扩展，它提供了语法突出显示、代码完成和其他有用的功能。您可以从 VSCode Marketplace安装它。 安装后，进入扩展设置，并确保勾选Enable Language Server 和Enable Scarb选项。