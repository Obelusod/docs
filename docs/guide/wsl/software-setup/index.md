---
title: 软件安装与配置
---

!!! abstract "WSL 配置差异"

    大部分软件的安装和配置均与其他 Ubuntu 发行版相同，但需要注意以下两点：
    
    - WSL 主要以 Shell 环境与 [Windows Terminal](https://learn.microsoft.com/zh-cn/windows/terminal/) 交互使用，**对 WSL 上的
      GUI 应用的支持不提供完整的桌面体验**，它依赖于 Windows 桌面，因此可能不支持安装以桌面为中心的工具或应用。
    - 某些硬件驱动（如 NVIDIA 显卡驱动）会**直接调用 Windows 所安装的版本（而无需另行安装）**，如果在 WSL 安装适用于 Linux
      的版本可能会出现问题。

    !!! tip ""

        除了 NVIDIA 显卡驱动 和 CUDA Toolkit 的安装方式不同外，**其他均可参考一般 Linux 发行版的[软件安装与配置](../../ubuntu/development-tools/index.md)**

---

## 文本编辑器

!!! info "文本编辑器（Text Editor）"

    当使用命令打开文本文件并编辑时，需要用到文本编辑器，WSL 的 Ubuntu 可能并未默认安装，主要推荐三款文本编辑器：**Vim**、**Gedit** 和 
    **GNOME Text Editor**。

    **本篇指南所有涉及文本编辑的命令，均使用具有图形界面的 `gedit` 编辑，可自行更换。**

!!! warning "中文乱码问题"

    在 WSL Ubuntu 中使用图形化文本编辑器（如 Gedit 和 GNOME Text Editor），打开含有中文字符的文本文件时可能会出现乱码，
    可以通过**设置字符编码**、**安装中文字体**等方法解决。

=== "Vim"

    [Vim](https://www.vim.org/) 是一款功能强大的、基于命令行的文本编辑器，支持语法高亮、智能缩进、代码折叠等高级编辑功能，
    还可以通过插件扩展它的功能，特别适合于程序员和系统管理员等专业人士使用。
    
    ``` bash
    sudo apt install vim
    ```

=== "Gedit"

    [Gedit](https://gedit-text-editor.org/) 是一款轻量级的、基于图形界面的文本编辑器，具有代码高亮、自动缩进、多标签编辑、插件扩展等功能，是
    Ubuntu GNOME 桌面环境中预安装的编辑器之一。
    
    ``` bash
    sudo apt install gedit
    ```

=== "GNOME Text Editor"

    [GNOME Text Editor](https://apps.gnome.org/TextEditor/) 是一款专注于会话管理的简单文本编辑器，致力于跟踪更改和状态，
    具有现代化的界面和功能，包括语法高亮显示、搜索替换、内联拼写检查、文档打印等特性，并且支持 Vim 键绑定。目前在 Ubuntu 24.04 上，已取代 Gedit
    成为 GNOME 默认的文本编辑器（Text Editor）。
    
    ``` bash
    sudo apt install gnome-text-editor
    ```
