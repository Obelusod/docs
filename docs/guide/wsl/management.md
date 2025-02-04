---
title: 管理 WSL
---

## 管理 WSL 磁盘空间

### 查找 WSL 硬盘位置

在 PowerShell 中输入并执行下列命令，需要将 `<distribution-name>` 替换为特定发行版名称（如 Ubuntu）

``` powershell
(Get-ChildItem -Path HKCU:\Software\Microsoft\Windows\CurrentVersion\Lxss | Where-Object { $_.GetValue("DistributionName") -eq '<distribution-name>' }).GetValue("BasePath") + "\ext4.vhdx"
```

!!! tip "使用 Everything 搜索"

    除此之外，也可以使用 [Everything](https://www.voidtools.com) 工具，搜索文件名 `ext4.vhdx` 快速定位到 WSL 硬盘位置

---

### 扩展 WSL 空间大小

!!! quote "TODO"

---

### 压缩 WSL 空间大小

!!! quote "TODO"
