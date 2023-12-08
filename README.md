# OoooooS Most Frequently Used Commands

`lsb_release` 命令用于显示 Linux 发行版的信息。运行该命令时，它会返回有关系统发行版的信息，包括版本号、发行代号、发行名称等。
  
`lsmod` 命令用于列出当前在 Linux 内核中加载的模块（也称为内核模块）。内核模块是一种动态加载到内核中的可执行代码，通常用于扩展内核的功能，支持新的硬件设备或提供额外的功能。
  - Module（模块）： 内核模块的名字。
  - Size（大小）： 模块的大小，通常以字节为单位。
  - Used by（被使用）： 使用该模块的进程数，表示有多少个进程正在使用这个模块。
  - Load Address（加载地址）： 模块加载到内存的地址。

`blacklist`
- 在Linux中，内核模块是一种动态加载到内核中的可执行代码，用于扩展内核的功能。有时候，你可能希望阻止某个特定的内核模块被加载。为了实现这个目的，可以使用 /etc/modprobe.d/ 目录下的配置文件，并在其中使用 blacklist 关键字。

### 编译器
- gcc
- Clang: Clang 是一个开源的编译器前端，支持多种语言，包括C、C++、Objective-C 和 Objective-C++。它的设计注重速度和模块化，并在许多方面与 gcc 相似。
- Microsoft Visual C++ Compiler: 用于 Windows 平台的 Microsoft Visual C++ 编译器。它通常与 Microsoft Visual Studio 集成，用于编译 C++ 代码。
- Intel C++ Compiler: 由英特尔提供的编译器，支持多种平台，包括 x86 和 x86-64 架构。它通常用于优化针对 Intel 处理器的代码。
- LLVM: LLVM 不仅是一个编译器，还是一个 modulal 编译器框架。Clang 是 LLVM 框架中的一个前端。LLVM 具有可扩展性，可以用于多种语言和用途。
- Sun Studio: 由甲骨文公司提供，主要用于编译支持 Solaris 操作系统的应用程序。
- IBM XL C/C++ Compiler: 由 IBM 提供，支持多种 IBM 平台，如 AIX。
- Open64: 开源的编译器，支持多种平台，包括 x86、x86-64、ARM 和 MIPS 等。
- PGI Compiler (Portland Group): 用于科学和工程计算的编译器，支持多种平台和加速器，如 NVIDIA GPU。

`service` 命令在 Linux 系统中用于管理系统服务（daemons）。它允许用户启动、停止、重新启动、查看服务状态等操作。服务是在后台运行的系统进程，负责执行各种系统任务，如网络服务、日志记录等。

- `sudo service serviceName start` 用于启动指定服务，其中 serviceName 是服务的名称。
- `sudo service serviceName stop`
- `sudo service serviceName restart`
- `sudo service serviceName status`
- `sudo service --status-all` 用于显示系统中所有服务的状态。






