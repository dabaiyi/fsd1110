# FSD 项目中文文档

## 项目概述

FSD (Flight Simulation Daemon) 是一个用于 Squawkbox/Pro Controller 客户端的多服务器系统，允许飞行模拟器玩家在网络上互相连接和通信。本版本基于 Marty Bochane 的 FSD 2 源代码，根据全局定义显示这是 "FSFDT Windows FSD Beta from FSD V3.000 draft 9"。

## 项目历史

这个仓库源自 Marty Bochane 的 FSD 2 源代码的最后已知公开副本。它起源于一个名为 'fsd1110.zip' 的压缩文件，显示它可能是 "FSFDT Windows FSD Beta from FSD V3.000 draft 9"。它几乎与 Apollo3 飞行模拟器网站上仍然可用的 fsd-ubuntu-120413.tar.bz2 发行版内容相同。

## 许可证

源代码中未包含许可证，也没有版权声明。这些源代码被假定在公共领域可用。

## 目录结构

在这个包中，您会找到以下目录：

- **fsd**: FSD 系统的源代码。
- **docs**: 包含文档文件。
- **windows**: 包含 Windows 相关文件，如配置文件、批处理脚本和可执行文件。
- **unix**: 包含 Unix/Linux 相关文件，如脚本和配置文件。

## 编译指南

### Unix 系统

1. 进入 fsd 子目录：`cd fsd`
2. 编译项目：`make`
3. 编译后的 fsd 程序将在 unix 目录中生成
4. 清理项目：`make clean`

### Windows 系统

1. 使用 Visual Studio 6 或更高版本打开 fsd/fsd.dsw
2. 编译后的 Release 版本将在 windows 目录中生成
3. 清理项目时删除生成的 Debug 或 Release 文件夹

## 配置和运行服务器

### 配置服务器

所有运行服务器所需的文件都在 'fsd help files' 目录中。您会找到以下文件：
- **fsd.conf.sample**: 配置文件样本。
- **help.txt**: 系统界面的在线帮助文件。
- **motd.txt.sample**: 客户端连接后将显示的消息。

配置过程：
1. 将 fsd.conf.sample 复制到 fsd.conf
2. 编辑 fsd.conf 文件，主要修改 [system] 组中的以下字段：
   - **ident**: 服务器的唯一标识
   - **email**: 您的电子邮件地址
   - **hostname**: 服务器的主机名或 IP 地址
   - **name**: 服务器的文本描述
   - **password**: 访问系统端口上特权命令的密码
   - **location**: 服务器在世界上的物理位置

### 启动服务器

#### Windows 系统
- 有脚本可以交互式运行 FSD、将 FSD 安装为服务并运行、卸载服务

#### Unix 系统
- 查看 fsd.sh 以将 fsd 安装为服务器启动时自动启动
- 运行 ./fsd_d.sh 以将 fsd 作为守护进程启动
- 运行 killfsd.sh 以杀死守护进程

### 测试服务器

启动后，服务器会打开端口 3012（或您配置的其他端口）。此端口可用于管理服务器。您可以使用 telnet 连接到此端口：`telnet localhost 3012`

连接后，您可以发出命令。使用 'help' 命令可以获取在线帮助。

### 连接到网络（可选）

如果您的服务器将 24 小时连接到互联网，您可以连接到 FSD 网络。连接到网络非常简单，只需找到运行 FSD 的另一台服务器的主机地址，然后使用 'connect <hostname>' 命令连接。

## fsd 目录文件说明

fsd 目录包含 FSD 系统的核心源代码，以下是对主要文件的说明：

### 核心文件

- **global.h**: 包含全局定义、常量、版本信息和平台特定的宏定义。
- **main.cpp**: 程序的入口点，包含主函数和 Windows 服务相关代码。
- **fsd.h/cpp**: 定义核心服务器类 `fsd`，包含服务器的主要功能和运行逻辑。
- **protocol.h**: 定义通信协议中的命令和错误代码常量。

### 配置和管理

- **config.h/cpp**: 处理配置文件的读取和解析。
- **manage.h/cpp**: 包含管理功能和变量。
- **fsdpaths.h**: 定义文件路径相关的宏。

### 网络和接口

- **interface.h/cpp**: 定义基础接口类。
- **clinterface.h/cpp**: 处理客户端接口。
- **servinterface.h/cpp**: 处理服务器间接口。
- **sysinterface.h/cpp**: 处理系统接口（管理接口）。
- **client.h/cpp**: 处理客户端连接和数据。
- **server.h/cpp**: 处理服务器间连接和数据。

### 用户和认证

- **user.h/cpp**: 定义基础用户类。
- **cluser.h/cpp**: 客户端用户相关功能。
- **servuser.h/cpp**: 服务器用户相关功能。
- **sysuser.h/cpp**: 系统用户相关功能。
- **authenticate.h/c**: 处理用户认证。
- **certificate.h/cpp**: 处理证书管理。

### 支持功能

- **support.h/cpp**: 提供各种支持函数。
- **process.h/cpp**: 处理数据包和消息。
- **mm.h/cpp**: 可能是内存管理相关。
- **attributes.h**: 定义属性相关的结构或常量。
- **wprofile.h/cpp**: 可能与气象配置文件相关。

### 项目文件

- **Makefile**: Unix/Linux 系统的编译脚本。
- **fsd.dsp/fsd.dsw**: Visual Studio 项目文件。
- **fsd.ncb/fsd.opt**: Visual Studio 生成的辅助文件。

## 系统功能

### 主要功能

1. **多服务器网络**: 允许多个服务器相互连接，形成一个大型网络
2. **客户端支持**: 支持 Squawkbox 和 Pro Controller 客户端连接
3. **气象服务**: 提供 METAR 气象信息
4. **证书管理**: 可以添加、删除和修改证书
5. **服务器管理**: 通过系统端口提供命令行管理界面
6. **自动重连**: 服务器连接断开后会自动尝试重连

### 常用命令

- **help**: 获取在线帮助
- **servers**: 查看服务器列表
- **clients**: 查看客户端列表
- **ping**: 检查与单个服务器的连接
- **connect**: 连接到其他服务器
- **disconnect**: 断开与服务器的连接
- **weather**: 获取指定机场的气象信息
- **cert**: 查看、添加、删除和修改证书
- **log**: 查看和管理日志

## 注意事项

1. 服务器标识（ident）必须在网络中是唯一的，且不要太长（通常5个字符足够）
2. 确保服务器的时区设置正确
3. 连接到网络前确保您有足够的带宽
4. 定期检查服务器连接的延迟（Lag）值，如果太高可能需要连接到其他服务器
5. 注意证书管理，您的更改将在整个网络中可用
