本页面主要介绍了各系统下各类编译器/解释器的安装步骤。

## GCC

### Windows

#### 手动下载安装

方便起见，我们在 Windows 系统下使用由 MinGW-w64 项目提供的 GCC 编译器。

首先前往 MinGW 的 [Releases](https://github.com/niXman/mingw-builds-binaries/releases/latest) 页面下载最新的安装包，如下图中红色箭头所示：

![](./images/compiler1.png)

下载好后将其解压到电脑中的某个位置，教程中将其解压到了 C 盘的根目录。目录名中最好不要包含非英文字符和空格，否则可能会在后期导致一些问题。

![](./images/compiler2.png)

接下来我们需要将编译器的可执行文件目录添加到系统环境变量中，这样在编译时就不需要指定编译器的路径了，方便使用。上方我们将 MinGW 解压到了 `C:\mingw64` 目录中，那么可执行文件所在的目录就是 `C:\mingw64\bin`。

按下 Windows 徽标 + R 组合键，输入 `rundll32.exe sysdm.cpl,EditEnvironmentVariables`，打开系统环境变量设置窗口，并在「系统变量」一节中选中名为「Path」的变量，然后点击「编辑」按钮：

![](./images/compiler3.png)

在编辑窗口中点击右侧的「新建」按钮，为「Path」变量新建一个条目，并填入上文中记录下的可执行文件所在的目录（教程中为 `C:\mingw64\bin`）。

![](./images/compiler4.png)

??? note "对部分老版本系统的提示"
    部分老版本系统只能手动修改变量的文本值，那么需要在变量的值的末尾插入一个 **半角分号**，再将可执行文件所在的目录粘贴到这个半角分号的后面，如图所示：
    
    ![](./images/compiler5.png)

完成后一路点击「确定」按钮退出即可。

接下来打开终端，输入 `g++ --version` 并按下回车，如果出现如图所示的提示则代表安装成功。

![](./images/compiler6.png)

#### Scoop 安装

打开 PowerShell，运行以下脚本：

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
irm get.scoop.sh | iex
scoop install mingw-winlibs
```

### Linux

#### Debian/Ubuntu

首先先更新软件包列表：

```bash
sudo apt update
```

再使用命令直接安装即可：

```bash
sudo apt install g++
```

#### Arch Linux

使用命令直接安装即可：

```bash
sudo pacman -Syu gcc
```

#### openSUSE

使用命令直接安装即可：

```bash
sudo zypper in gcc-c++
```

### macOS

首先更新包管理器：

```bash
brew upgrade
brew update
```

再使用命令直接安装即可：

```bash
brew install gcc
```

## JDK

JDK 版本有很多，本文以 OpenJDK 为例。

### Windows

#### 直接下载安装

访问 [Adoptium OpenJDK](https://adoptium.net/zh-CN/temurin/releases) 的下载页面，选择合适的版本，本文选择了 Windows 下的 x64 Java 18。

点击右侧的 msi 文件进行下载。

如果你的网络质量不佳，你也可以选择访问 [清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/Adoptium/) 进行下载。

下载完成后打开 .msi 文件，持续点击 Next，即可完成安装。

随后打开终端，输入 `java --version` 并回车，出现

```text
openjdk 18.0.2.1 2022-08-18                                                                                             
OpenJDK Runtime Environment Temurin-18.0.2.1+1 (build 18.0.2.1+1)                                                       
OpenJDK 64-Bit Server VM Temurin-18.0.2.1+1 (build 18.0.2.1+1, mixed mode, sharing) 
```

类似物即可算作成功。

#### Scoop 安装

打开 PowerShell，运行以下脚本：

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
irm get.scoop.sh | iex
scoop bucket add java
scoop install openjdk18
```

### Linux

#### openSUSE

使用命令直接安装即可：

```bash
sudo zypper in java-18-openjdk-devel
```

## Python 3 (CPython 3)

### Windows

#### 直接下载安装

访问 [Python](https://www.python.org/downloads/) 的下载页面，点击页面中央的黄色按钮进行下载。

打开 .exe，勾选 Add to path 后点击 Install Now。

完成后打开终端，输入 `python` 并回车，出现 REPL 代表安装成功。

#### Scoop 安装

打开 PowerShell，运行以下脚本：

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
irm get.scoop.sh | iex
scoop install python
```

#### Microsoft Store 安装

打开 Microsoft Store，搜索 Python。

点击第一个搜索结果，点击安装，等待安装完成。

### Linux

#### openSUSE

使用命令直接安装即可：

```bash
sudo zypper in python3
```

## LLVM

### Windows

??? note "LLVM 在 Windows 上的坑"
    由于 LLVM 在 Windows 上缺失标准库，所以你仍需安装 MSVC 或 GCC。

#### 直接安装

访问 [LLVM](https://github.com/llvm/llvm-project/releases/latest) 的下载页面，选择 LLVM-\*-win64.exe 下载。

如果你的网络质量不佳，你也可以选择访问 [清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/github-release/llvm/llvm-project/LatestRelease/) 进行下载。

打开 .exe 文件，安装时勾选 Add LLVM to system PATH for current user，随后一直点击下一步即可安装完成。

打开终端，输入 `clang++ --version` 并回车，出现

```text
clang version 15.0.1
Target: x86_64-pc-windows-msvc
Thread model: posix
InstalledDir: <omitted>
```

类似物即代表成功。

#### Scoop 安装

打开 PowerShell，运行以下脚本：

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
irm get.scoop.sh | iex
scoop install llvm
```

### Linux

#### openSUSE

使用命令直接安装即可：

```bash
sudo zypper in llvm clang
```

## MSVC (Visual Studio)

访问 [Visual Studio](https://visualstudio.microsoft.com/zh-hans/) 的下载页面，将光标移动到 下载 Visual Studio，在下来菜单中点击 Community 2022 下载。

打开安装器，选择 Community 2022 安装。

在随后弹出来的窗口中仅选择 使用 C++ 的桌面开发，然后单击安装。
