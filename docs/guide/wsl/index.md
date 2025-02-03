---
title: WSL 安装与配置指南
---

!!! abstract "适用于 Linux 的 Windows 子系统（Windows Subsystem for Linux，WSL）[^1]"

    **WSL** 是 Windows 的一项功能，可用于在 Windows 计算机上运行 Linux 环境，而无需单独的虚拟机或双引导。 WSL 旨在为希望同时使用 Windows 和
    Linux 的开发人员提供无缝高效的体验。
    
    - **多发行版支持**：使用 WSL 安装和运行各种 Linux 发行版，例如 Ubuntu、Debian、Kali 等。 安装 Linux 发行版并从 Microsoft Store
      接收自动更新、导入 Microsoft Store 中不可用的 Linux 发行版。
    - **文件系统共享**：将文件存储在独立的 Linux 文件系统中，并实现 Windows 与 Linux 文件系统之间的双向访问。
    - **Shell 环境**：运行常用的 Bash 命令行工具（例如 `grep`、`sed`、`awk`）或其他 ELF-64 二进制文件；运行 Bash 脚本和 GNU/Linux
      命令行应用程序，包括 Vim、Python、C/C++、MySQL 等。
    - **包管理器**：通过自带的 GNU/Linux 软件包管理器安装其他软件。
    - **跨平台调用**：使用类似于 Unix 的命令行 Shell 调用 Windows 应用程序，或在 Windows 上调用 GNU/Linux 应用程序。
    - **图形界面集成**：运行直接集成到 Windows 桌面的 GNU/Linux 图形应用程序。
    - **GPU 加速**：使用 GPU 加速 Linux 上运行的机器学习工作负载。

---

**WSL 安装要求**

!!! Warning "安装 WSL 需要满足以下要求："

    - **Windows 10/11**
        - 对于 x64 系统：版本 1903 或更高版本，内部版本为 18362.1049 或更高版本。
        - 对于 ARM64 系统：版本 2004 或更高版本，内部版本为 19041 或更高版本。
    - **支持虚拟化（Intel VT 或 AMD-V）**
        - 安装 Hyper-V 虚拟化组件（如 Windows 虚拟机监控程序）
    - **至少 4GB 可用内存和 20GB 存储空间**

---

**WSL 1 vs WSL 2**

!!! info "WSL 1 和 WSL 2 之间的主要区别[^2]"

    - WSL 2 在托管 VM 内使用 **实际的 Linux 内核**、支持**完整的系统调用兼容性**以及**跨 Linux 和 Windows 操作系统的性能**。
    - WSL 2 是安装 Linux 发行版时的当前默认版本，它使用**最新最好的虚拟化技术**在**轻量级实用工具虚拟机 (VM)** 内运行 Linux 内核。
    - WSL 2 将 Linux 发行版作为**托管 VM 内的隔离容器**运行。

| 功能                                |      WSL 1       |      WSL 2       |
|:----------------------------------|:----------------:|:----------------:|
| Windows 和 Linux 之间的集成             | :material-check: | :material-check: |
| 启动时间短                             | :material-check: | :material-check: |
| 与传统虚拟机相比，占用的资源量少                  | :material-check: | :material-check: |
| 可以与当前版本的 VMware 和 VirtualBox 一起运行 | :material-check: | :material-close: |
| 托管 VM                             | :material-close: | :material-check: |
| 完整的 Linux 内核                      | :material-close: | :material-check: |
| 完全的系统调用兼容性                        | :material-close: | :material-check: |
| 跨 OS 文件系统的性能                      | :material-check: | :material-close: |
| systemd 支持                        | :material-close: | :material-check: |
| IPv6 支持                           | :material-check: | :material-check: |

!!! note "本指南主要聚焦于 WSL 2 和 Ubuntu"

    WSL 2 使用虚拟化技术并拥有完整的 Linux 内核，在文件 IO 性能和系统调用兼容性上相比 WSL 1 均有巨大提升，因此**建议安装最新的 WSL 2**。

[^1]: [适用于 Linux 的 Windows 子系统文档 | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/)
[^2]: [比较 WSL 版本 | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/compare-versions)
