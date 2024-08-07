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

## 安装APP
### Skim
PDF轻量级浏览软件，homebrew下载

### keka
压缩软件

### VLC
播放器


## CLI

### ~~Alacritty~~
~~（已放弃该软件，感觉维护力度不够，虽然够轻量级，但是没有tab页是硬伤，tmux懒得折腾了）~~

#### 安装
homebrew:
```bash
brew install --cask alacritty
```

#### 下载字体
homebrew:
```bash
brew install font-hack-nerd-font
```

#### Configuration
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
安装、启用：
```
brew install zsh-autosuggestions
echo "source $(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc
source ~/.zshrc
```

#### Setup zsh-syntax-highlighting
安装、启用：
```
brew install zsh-syntax-highlighting
echo "source $(brew --prefix)/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ~/.zshrc
source ~/.zshrc
```

### VIM
#### 关于.vimrc位置
##### 系统级及本地 vimrc 文件
当 Vim 启动时，编辑器会去搜索一个系统级的 vimrc 文件来进行系统范围内的默认初始化工作。

这个文件通常在你系统里`$VIM/vimrc`的路径下，如果没在那里，那你可以通过在 Vim 里面运行`:version`命令来找到它的正确存放位置。比如说，在我这里，这个命令的相关部分的输出结果如下：
```bash
：version
... ... ... 
system vimrc file: "$VIM/vimrc" 
user vimrc file: "$HOME/.vimrc" 
2nd user vimrc file: "~/.vim/vimrc" 
user exrc file: "$HOME/.exrc" 
fall-back for $VIM: "/usr/share/vim" 
... ... ...
```

可以看到那个系统 `vimrc` 文件确实位于 `$VIM/vimrc` ，但我检查了我机子上没设置过`$VIM` 环境变量。所以在这个例子里 - 正如你在上面的输出所看到的 - `$VIM`在我这的路径是`/usr/share/vim`，是一个回落值（LCTT 译注：即如果前面失败的话，最终采用的结果）。

于是我试着在这个路径寻找 `vimrc` ，我看到这个文件是存在的。如上即是我的系统`vimrc`文件，就如前面提过的那样 - 它在 Vim 启动时会被读取。

在这个系统级 `vimrc` 文件被读取解析完后，编辑器会查找一个用户特定的（或者说本地的）`vimrc` 文件。

这个本地 `vimrc` 的搜索顺序是：环境变量`VIMINIT`、`$HOME/.vimrc`、`环境变量 EXINIT`，和一个叫 `exrc`的文件。
通常情况下，会存在`$HOME/.vimrc`或`~/.vimrc`这样的文件，这个文件可看作是本地`vimrc`。

##### 设置 vimrc 的路径
如上文所述，在 Vim 中，`.vimrc`文件是用户配置文件，用于存放 Vim 的个性化设置。这个文件通常位于用户的主目录下（也就是 `~/.vimrc`）。然而，如果你想要更改`.vimrc`文件的位置，你可以设置 VIMINIT 环境变量。 `VIMINIT` 环境变量包含了在 Vim 启动时会被执行的 Vim 命令。

例如，如果你想让 Vim 使用位于 `/path/to/your/vimrc` 的配置文件，你可以设置 `VIMINIT` 环境变量如下：
```bash
export VIMINIT='source /path/to/your/vimrc'
```
你可以将这行命令添加到你的 `.bashrc` 或 `.bash_profile` 文件中（取决于你的系统和shell），以确保每次启动新的 shell 时 `VIMINIT` 都会被设置。
然后，当你启动 Vim 时，它会执行 `VIMINIT` 环境变量中的命令，也就是 `source /path/to/your/vimrc`，从而加载你指定的 `.vimrc` 文件。

**需要注意的是，`.vimrc` 文件中的配置仍然会影响到 Vim 的全局设置，所以在多用户环境下要谨慎使用这种方法。**

### miniconda3
到官网使用`Command Line Quick install`安装，会安装到当前用户下；使用官网或者镜像提供的`.pkg`文件安装会使用管理员权限，安装到`/opt/miniconda3`环境下
如果安装到`/opt`目录下想要卸载，直接删除相关文件以及配置文件即可
### homebrew

#### 安装
只能安装到`/opt/homebrew`目录下，其原因参考[Release Note](https://brew.sh/2021/02/05/homebrew-3.0.0/)，卸载homebrew参考[博客](https://mac.install.guide/homebrew/5)
#### formulae和cask的区别
##### Formulae（复数形式为Formula）

- **定义**：Formulae是Homebrew中用于描述如何构建和安装软件的脚本文件。这些脚本通常是用Ruby语言编写的，并且存储在Homebrew的GitHub仓库中。
- **功能**：Formulae负责处理源代码的下载、编译、链接以及安装过程。它们允许用户安装命令行工具或其他可以通过编译源代码来构建的软件。
- **示例**：常见的命令行工具如`git`, `wget`, `curl`等都有对应的Formula。

#### Casks
- **定义**：Casks是Homebrew的一个扩展，用于安装图形界面应用、字体或需要额外步骤来安装的软件。
- **功能**：与Formulae不同，Casks通常用于安装那些以二进制形式发布的应用程序，比如安装程序或压缩包。Casks会将应用程序移动到`/Applications`目录，并可能创建一些符号链接或菜单项。
- **示例**：像`google-chrome`, `visual-studio-code`, `spotify`这样的桌面应用就是通过Cask来安装的。

##### 区别
1. **安装方式**：
    - Formulae通常涉及编译源代码，而Casks则是直接安装预编译好的二进制文件或应用程序包。
2. **适用类型**：
    - Formulae适用于命令行工具和其他可通过编译安装的软件。
    - Casks适用于GUI应用程序、字体或需要特殊安装过程的软件。

##### 使用方法
- 安装Formulae: `brew install <formula-name>`
- 安装Cask: `brew install --cask <cask-name>`
