# 命令行界面CLI(Command-Line Interface)

## 简介

**命令行界面CLI是和图形界面GUI相对应的界面，如Windows的cmd就是一个命令行界面。命令行界面的操作没有图形界面那么简单易懂，但是由于省去了很多图形资源，在熟练记住命令行指令的情况下，命令行界面的执行效率要比图形界面高很多**

## Cobra-创造命令行界面的工具包

**cobra是go语言中的一个工具包，它的主要作用便是用来创建一个命令行界面**

### 提供功能

* 轻松创建基于子命令的CLI

* 创建完全符合POSIX标准的flag

* 支持嵌套子命令

* 支持全局、本地、级联的flag

* 智能建议（app srver ...did you mean app server？）

* 自动的命令和flag 的帮助性信息

* 子命令分组

* 自动识别-h,--help等flag的信息

* 命令别名

**cobra遵循commands、arguments、flags的结构**

```shell
#commands arguments flags
docker ps -a
```

### cobra的基础使用

#### 初始化

```go
cobra-cli init
//安装cobra-cli工具之后的cobra初始化
 
tree filename
filename
|——cmd
|    |_root.go
|——go.mod
|——go.sum
|——LICENSE
|__main.go
```

**在利用cobra-cli工具初始化一个命令行界面之后，cobra会自动创建一个命令行界面的目录结构，包括main.go程序文件入口**

#### Commands

```go
cobra-cli add wget
cobra-cli add ping
//增加命令行工具的commands
之后的项目结构如下
filename
|——cmd
|    |——root.go
|    |——ping.go
|    |__wget.go
|——go.mod
|——go.sum
|——LICENSE
|__main.go
```

**cobra通过add来添加命令，且添加的命令会成为go文件存储在cmd文件夹下，对命令进行编写即在对应的go文件进行编写即可**

#### Flags

```go
/*flag包括全局和局部两种。全局定义的flag在父命令定义后子命令也会生效。局部flag在哪里定义就在哪里生效s*/
```

**flag的设置在main.go文件和其它对应的文件里面**
