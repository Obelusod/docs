!!! abstract "WSL 配置差异"

    大部分软件的安装和配置均与其他 Ubuntu 发行版相同，但需要注意以下两点：
    
    - WSL 主要以 Shell 环境与 [Windows Terminal](https://learn.microsoft.com/zh-cn/windows/terminal/) 交互使用，**对 WSL 上的
      GUI 应用的支持不提供完整的桌面体验**，它依赖于 Windows 桌面，因此可能不支持安装以桌面为中心的工具或应用
    - 某些硬件驱动和软件（如 NVIDIA 显卡驱动、CUDA）会**直接调用 Windows 所安装的版本（而无需另行安装）**，如果在 WSL 再次安装适用于 Linux
      的版本可能会出现问题

---

## 文本编辑器

!!! info "文本编辑器（Text Editor）"

    当使用命令打开文本文件并编辑时，需要用到文本编辑器，WSL 的 Ubuntu 可能并未默认安装，主要推荐三款文本编辑器：Vim、Gedit 和 
    GNOME Text Editor。

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

---

## CUDA Toolkit

!!! danger "无需再为 WSL 安装 NVIDIA 显卡驱动！"

    只要在 Windows 上安装了 NVIDIA 显卡驱动，CUDA 就能够在 WSL 2 中使用；安装在 Windows 主机上的 CUDA 驱动程序将在 WSL 2 内部以
    `libcuda.so` 库的形式进行模拟（stub），因此不应在 WSL 2 环境中安装任何 NVIDIA 显卡的 Linux 驱动程序。

    **使用 `WSL-Ubuntu CUDA toolkit` 安装程序安装将不会附带 NVIDIA 显卡驱动。**

??? example "NVIDIA 显卡驱动、CUDA、PyTorch 的兼容版本要求"

    ![](../../assets/images/guide/compatibility-matrix-1.png)
    
    ![](../../assets/images/guide/compatibility-matrix-2.png)
    
    | PyTorch |   torchvision   |      CUDA Toolkit       |     Python     |
    |:-------:|:---------------:|:-----------------------:|:--------------:|
    |  2.3.1  |     0.18.1      |       11.8, 12.1        | >= 3.8, <=3.11 |
    |  2.3.0  |     0.18.0      |       11.8, 12.1        | >= 3.8, <=3.11 |
    |  2.2.2  |     0.17.2      |       11.8, 12.1        | >= 3.8, <=3.11 |
    |  2.2.1  |     0.17.1      |       11.8, 12.1        | >= 3.8, <=3.11 |
    |  2.2.0  |     0.17.0      |       11.8, 12.1        | >= 3.8, <=3.11 |
    |  2.1.2  |     0.16.2      |       11.8, 12.1        | >= 3.8, <=3.11 |
    |  2.1.1  |     0.16.1      |       11.8, 12.1        | >= 3.8, <=3.11 |
    |  2.1.0  |     0.16.0      |       11.8, 12.1        | >= 3.8, <=3.11 |
    |  2.0.1  |     0.15.2      |       11.7, 11.8        | >= 3.8, <=3.11 |
    |  2.0.0  | 0.15.0 (0.15.1) |       11.7, 11.8        | >= 3.8, <=3.11 |
    | 1.13.1  |     0.14.1      |       11.6, 11.7        | >= 3.7, <=3.11 |
    | 1.13.0  |     0.14.0      |       11.6, 11.7        | >= 3.7, <=3.11 |
    | 1.12.1  |     0.13.1      |    10.2, 11.3, 11.6     | >= 3.7, <=3.10 |
    | 1.12.0  |     0.13.0      |    10.2, 11.3, 11.6     | >= 3.7, <=3.10 |
    | 1.11.0  |     0.12.0      |       10.2, 11.3        | >= 3.7, <=3.10 |
    | 1.10.1  |     0.11.2      |       10.2, 11.3        | >= 3.6, <=3.9  |
    | 1.10.0  |     0.11.0      | 10.2, 11.3 (10.2, 11.1) | >= 3.6, <=3.9  |

    详见：[CUDA Toolkit Major Component Versions](https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html#cuda-toolkit-major-component-versions)
    和 [Previous PyTorch Versions](https://pytorch.org/get-started/previous-versions)

---

### 安装 CUDA Toolkit

!!! tip "CUDA 版本选择"

    选择 CUDA Toolkit 版本时，需要根据实际开发环境（如 PyTorch）选择

=== "使用 APT 安装（网络安装）"

    删除旧的 GPG 密钥
    
    ``` bash
    sudo apt-key del 7fa2af80
    ```
    
    ---
    
    安装 NVIDIA CUDA 密钥环，以获取最新软件源
    
    ``` bash
    wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-keyring_1.1-1_all.deb

    sudo dpkg -i cuda-keyring_1.1-1_all.deb
    ```
    
    ---
    
    使用 APT 命令，选择一个合适的 CUDA Toolkit 版本进行安装
    
    !!! example "可用的 CUDA Toolkit 版本 `${cuda-toolkit}`"
    
        - `cuda-toolkit-11-6`
        - `cuda-toolkit-11-7`
        - `cuda-toolkit-11-8`
        - `cuda-toolkit-12-0`
        - `cuda-toolkit-12-1`
        - `cuda-toolkit-12-2`
        - `cuda-toolkit-12-3`
        - `cuda-toolkit-12-4`

    !!! tip ""

        目前兼容性最佳的版本为：`CUDA Toolkit 11.8.0`    

    !!! tip "自动补全"

        建议使用 ++tab++ 键自动补全，或执行 `apt search cuda-toolkit` 命令，搜索当前可用的 CUDA Toolkit 版本
    
    ``` bash
    sudo apt install ${cuda-toolkit}
    ```
    
    ---
    
    安装完成后，可以使用以下命令查看 CUDA 版本以验证安装：
    
    ``` bash
    nvcc --version
    ```

=== "使用软件包安装（本地安装）"

    访问 [CUDA Toolkit Archive 官网](https://developer.nvidia.com/cuda-toolkit-archive)，根据实际开发需求，选择一个合适的 CUDA
    Toolkit 版本
    
    !!! tip ""

        目前兼容性最佳的版本为：`CUDA Toolkit 11.8.0`
    
    ![](../../assets/images/wsl/cuda-toolkit-archive.png){: .shadow }
    
    ---
    
    选择目标平台的操作系统（Linux）、架构（x86_64）、发行版（WSL-Ubuntu）和安装类型
    
    !!! danger "务必选择 `deb (local)` 方式安装"
    
        安装类型**务必选择 `deb (local)`**，使用 `deb (network)` 将会在线安装最新版，而 `runfile (local)` 无法确保不安装驱动！
    
    ![](../../assets/images/wsl/cuda-toolkit-downloads-1.png){: .shadow }
    
    ---
    
    依照所选 Installer Type（安装类型）的安装命令进行安装
    
    ``` bash
    wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin

    sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600

    wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda-repo-wsl-ubuntu-11-8-local_11.8.0-1_amd64.deb
    
    sudo dpkg -i cuda-repo-wsl-ubuntu-11-8-local_11.8.0-1_amd64.deb

    sudo cp /var/cuda-repo-wsl-ubuntu-11-8-local/cuda-*-keyring.gpg /usr/share/keyrings/

    sudo apt-get update

    sudo apt-get -y install cuda
    ```
    
    ![](../../assets/images/wsl/cuda-toolkit-downloads-2.png){: .shadow }
    
    ---

    安装完成后，可以使用以下命令查看 CUDA 版本以验证安装：
    
    ``` bash
    nvcc --version
    ```

---

**卸载 CUDA Toolkit**

- **删除 CUDA Toolkit**

``` bash
sudo apt --purge remove "*cuda*" "*cublas*" "*cufft*" "*cufile*" "*curand*" \
  "*cusolver*" "*cusparse*" "*gds-tools*" "*npp*" "*nvjpeg*" "nsight*" "*nvvm*"
```

- **删除 NVIDIA 驱动程序**

``` bash
sudo apt --purge remove "*nvidia*" "libxnvctrl*"
```

- **清理缓存及无用的相关依赖**

``` bash
sudo apt autoremove
```

---

## Pip (Python Install Package)

### 安装 Pip

=== "使用 APT 安装"

    ``` bash
    sudo apt install python3-pip
    ```

=== "使用 `ensurepip` 模块安装"
    
    ``` bash
    python -m ensurepip --upgrade # (1)!
    ```

    1. `ensurepip` 模块需要 Python 3.4 及以上版本

=== "使用 `get-pip.py` 脚本安装"

    ``` bash
    wget https://bootstrap.pypa.io/get-pip.py # (1)!

    python get-pip.py
    ```

    1. 下载 `get-pip.py` 脚本

---

### 更新 Pip

!!! tip "更新 Pip"

    默认安装的 Pip 可能较旧，建议使用以下命令更新至最新版

``` bash
pip install --upgrade pip # (1)!
```

1. 或 `python -m pip install --upgrade pip`

---

### 更换软件源

选择一个国内镜像站，建议优先选择地理位置较近、相同运营商的镜像站 (1)
{ .annotate }

1. 可在[校园网联合镜像站](https://mirrors.cernet.edu.cn/site)中查询

|       推荐镜像站       | 镜像站帮助页（Ubuntu）                                            |
|:-----------------:|-----------------------------------------------------------|
| 清华大学镜像站（tsinghua） | <https://mirror.tuna.tsinghua.edu.cn/help/pypi/>          |
|   南京大学镜像站（nju）    | <https://mirror.nju.edu.cn/mirrorz-help/pypi/?mirror=NJU> |
|  上海交通大学镜像站（sjtu）  | <https://mirrors.sjtug.sjtu.edu.cn/docs/pypi-packages>    |
|  阿里云镜像站（aliyun）   | <https://developer.aliyun.com/mirror/pypi>                |

=== "临时使用"

    ``` bash
    pip install -i ${index-url} ${package}
    ```

=== "设为默认（使用命令）"

    ``` bash
    pip config set global.index-url ${index-url}
    ```

=== "设为默认（编辑配置文件）"

    ``` bash
    gedit ~/.config/pip/pip.conf
    ```

    ![](../../assets/images/wsl/pip-config.png){: .shadow }
    /// caption
    图中，使用南京大学镜像站
    ///

---

### 常用命令

| 描述              | 命令                                                                                                                                              |
|:----------------|:------------------------------------------------------------------------------------------------------------------------------------------------|
| 验证 pip 安装，检查版本等 | `pip --version, pip -V`                                                                                                                         |
| 安装包             | `pip install <options> <package>` <br/> &emsp; `-r, --requirement <file>` <br/> &emsp; `-U, --upgrade` <br/> &emsp; `-e, --editable <path/url>` |
| 卸载包             | `pip uninstall <options> <package>` <br/> &emsp; `-r, --requirement <file>` <br/> &emsp; `-y, --yes`                                            |
| 列出已安装包          | `pip list`                                                                                                                                      |
| 显示已安装包的信息       | `pip show <package>`                                                                                                                            |
| 显示缓存信息          | `pip cache info`                                                                                                                                |
| 删除所有缓存          | `pip cache purge`                                                                                                                               |
