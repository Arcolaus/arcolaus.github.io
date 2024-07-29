+++
title = "MacBook Silicon Configuraion"
description = "记录一下MacBook的一些环境配置"
date = 2024-07-29
slug = "macbook-silicon-configuration"
readingTime = true
categories = [
    "折腾"
]
tags = [
	"OSX",
	"ZSH",
	"Homebrew"
]
image = "screenshot_1.png"
+++




# 安装APP
## 压缩软件
### Keka
官网下载免费，AppStore下载收费


# CLI

## Alacritty
### 安装
homebrew:
```bash
brew install --cask alacritty
```

### 下载字体
homebrew:
```bash
brew install font-hack-nerd-font
```

### Configuration
创建配置文件：
```bash
mkdir -p ~/.config/alacritty
vim alacritty.toml
```

`alacritty.toml`：
```toml
import = [
	"~/.config/alacritty/themes/themes/night_owl.toml"
]

live_config_reload=true

[env]
TERM = "xterm-256color"

[window]
padding.x = 30
padding.y = 30
dimensions.columns = 135
dimensions.lines = 40
opacity=0.85


[font]
normal.family = "Hack Nerd Font"
size = 14.0
```

### powerlevel10k
安装、启用：
```bash
brew install powerlevel10k
echo "source $(brew --prefix)/share/powerlevel10k/powerlevel10k.zsh-theme" >> ~/.zshrc
source ~/.zshrc
```

卸载：
[GitHubGist](https://gist.github.com/breithbarbot/254e58bd87009963b3f58405d75cbe6c)

### ZSH plugin
#### zsh-autosuggestions
安装
```
brew install zsh-autosuggestions
```

启用
```
echo "source $(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc
```

生效
```
source ~/.zshrc
```

#### Setup zsh-syntax-highlighting
安装
```
brew install zsh-syntax-highlighting
```

启用
```
echo "source $(brew --prefix)/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc
```

生效
```
source ~/.zshrc
```

## miniconda3
到官网使用`Command Line Quick install`安装，会安装到当前用户下；使用官网或者镜像提供的`.pkg`文件安装会使用管理员权限，安装到`/opt/miniconda3`环境下
如果安装到`/opt`目录下想要卸载，直接删除相关文件以及配置文件即可
## homebrew

### 安装
只能安装到`/opt/homebrew`目录下，其原因参考[Release Note](https://brew.sh/2021/02/05/homebrew-3.0.0/)，卸载homebrew参考[博客](https://mac.install.guide/homebrew/5)
### formulae和cask的区别
#### Formulae（复数形式为Formula）

- **定义**：Formulae是Homebrew中用于描述如何构建和安装软件的脚本文件。这些脚本通常是用Ruby语言编写的，并且存储在Homebrew的GitHub仓库中。
- **功能**：Formulae负责处理源代码的下载、编译、链接以及安装过程。它们允许用户安装命令行工具或其他可以通过编译源代码来构建的软件。
- **示例**：常见的命令行工具如`git`, `wget`, `curl`等都有对应的Formula。

#### Casks
- **定义**：Casks是Homebrew的一个扩展，用于安装图形界面应用、字体或需要额外步骤来安装的软件。
- **功能**：与Formulae不同，Casks通常用于安装那些以二进制形式发布的应用程序，比如安装程序或压缩包。Casks会将应用程序移动到`/Applications`目录，并可能创建一些符号链接或菜单项。
- **示例**：像`google-chrome`, `visual-studio-code`, `spotify`这样的桌面应用就是通过Cask来安装的。

#### 区别
1. **安装方式**：
    - Formulae通常涉及编译源代码，而Casks则是直接安装预编译好的二进制文件或应用程序包。
2. **适用类型**：
    - Formulae适用于命令行工具和其他可通过编译安装的软件。
    - Casks适用于GUI应用程序、字体或需要特殊安装过程的软件。

#### 使用方法
- 安装Formulae: `brew install <formula-name>`
- 安装Cask: `brew install --cask <cask-name>`
