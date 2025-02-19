---
title: 卸载 Snap 组件及其软件包
---

!!! abstract "Snap"

    **Snap** 是 Ubuntu 推出的容器化软件打包格式，由 Canonical 开发，通过自包含依赖和沙盒隔离技术，简化应用安装与管理，
    避免依赖冲突并增强安全性；其应用默认自动更新，支持跨 Linux 发行版，并依托 Snap Store 提供集中化分发平台。

    **但由于的 snap 在国内网络下体验较差，软件包占用空间较多而软件启动速度较慢，并且强制捆绑、夹带私货等原因，在不需要的情况下可以将其卸载。**

!!! danger "谨慎卸载 Snap！"

    Ubuntu 新版本中已经深度集成了 Snap，某些 Ubuntu 特定的功能可能需要依赖于 Snap 才能使用，请谨慎执行完全卸载操作！

---

卸载前，先停止所有 Snapd 服务

```bash
sudo systemctl disable snapd.service
sudo systemctl disable snapd.socket
sudo systemctl disable snapd.seeded.service
sudo systemctl stop snapd
```

---

获取 Snap 软件包列表 `${package}`

```bash
snap list
```

---

使用下列命令卸载所有 Snap 软件包和 Snapd 服务

```bash
sudo snap remove --purge ${package}
sudo snap remove --purge snapd
```

---

清理 Snap 缓存数据

```bash
sudo rm -rf /var/cache/snapd/
```

使用 APT 完全卸载 Snap

```bash
sudo apt autoremove --purge snapd
```

---

删除 Snap 文件夹

```bash
sudo rm -rf ~/snap
```

---

为了禁止 APT 重新安装 Snap，新建并编辑以下规则（`nosnap`）

```bash
sudo gedit /etc/apt/preferences.d/nosnap
```

---

在 `nosnap` 文件中写入以下内容，并保存即可

```yaml title="nosnap"
Package: snapd
Pin: release a=*
Pin-Priority: -10
```
