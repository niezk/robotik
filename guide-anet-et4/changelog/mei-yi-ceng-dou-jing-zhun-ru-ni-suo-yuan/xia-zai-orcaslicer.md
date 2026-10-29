---
description: 官方下载
---

# 下载 OrcaSlicer

稳定版

## 稳定版本

选择你的平台。在 Windows 上我们推荐 Microsoft Store 版本，在 Linux 上推荐 Flathub 版本——两者都会自动更新。

### Windows

[Microsoft Store推荐](https://apps.microsoft.com/detail/9mv6gl23xm59) [安装程序 x64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest) [安装程序 ARM64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest) [便携版 x64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest) [便携版 ARM64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest)

### macOS

[Mac 通用版](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest)

### Linux

[Flathub推荐](https://flathub.org/apps/com.orcaslicer.OrcaSlicer) [AppImage x64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest) [AppImage ARM64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest) [Flatpak x64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest) [Flatpak ARM64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest)

每日构建

## 每日构建版

来自最新提交的构建版本，包含尚未正式发布的功能。可能存在不完善之处——每日构建版可能不稳定。

### Windows

不稳定 [在 GitHub 上查看每日构建版](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds)

### macOS

不稳定 [在 GitHub 上查看每日构建版](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds)

### Linux

不稳定 [在 GitHub 上查看每日构建版](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds)

要求

## 系统要求

### Windows

* Windows 10 或更高版本（64 位）
* 至少 4GB 内存（建议 8GB 及以上）
* 支持 OpenGL 3.3 的显卡
* 500MB 可用磁盘空间
* 需要网络连接以获取更新

### macOS

* macOS 10.15（Catalina）或更高版本
* 至少 4GB 内存（建议 8GB 及以上）
* Intel 或 Apple 芯片（M1/M2/M3）
* 500MB 可用磁盘空间
* 需要网络连接以获取更新

### Linux

* Ubuntu 20.04+ 或同等发行版
* 至少 4GB 内存（建议 8GB 及以上）
* 支持 OpenGL 3.3 的显卡
* 500MB 可用磁盘空间
* 需要网络连接以获取更新

安装

## 安装指南

### 选择你的平台

从上方的下载区域为你的操作系统选择合适的下载版本。对于 Windows，Microsoft Store 版本最简单，且会自动保持更新；否则可选择安装程序或便携版（大多数电脑选 x64，Windows on ARM 设备选 ARM64）。对于 macOS，通用版同时支持 Apple 芯片和 Intel Mac。对于 Linux，我们建议从 Flathub 安装；AppImage 同样适用于大多数发行版。

### 下载文件

点击你所选平台对应的下载按钮。直接下载来自我们官方的 GitHub 发布页面——请务必确认下载地址为 github.com/OrcaSlicer/OrcaSlicer，以确保来源真实可靠。商店版本来自 Microsoft Store 和 Flathub。

### 安装 OrcaSlicer

**Windows：**&#x8FD0;行 .exe 安装程序并按照安装向导操作。或将便携版解压到任意文件夹。\
**macOS：**&#x6253;开 .dmg 文件，将 OrcaSlicer 拖入你的应用程序文件夹。\
**Linux：**

AppImage Flatpak

1. 在你的下载文件夹中打开终端。
2. 为其添加可执行权限：
3. 运行它：

**提示：**&#x5982;果无法启动，可能需要安装 FUSE。可执行 `sudo apt install libfuse2`（Ubuntu/Debian）或 `sudo dnf install fuse`（Fedora）进行安装。

1. 请确保已安装 Flatpak —— [flatpak.org/setup](https://flatpak.org/setup/) 提供了各发行版的具体安装说明。
2. 从 Flathub 安装（推荐——自动更新）： 或者，如果你从 GitHub 下载了 `.flatpak` 文件：
3. 从应用菜单启动，或运行：

**注意：**&#x46;latpak 运行在沙盒环境中。如果需要访问主目录之外的文件，请使用 [Flatseal](https://flathub.org/apps/com.github.tchx84.Flatseal) 管理权限。

### 启动并配置

从应用程序菜单启动 OrcaSlicer。首次启动时，配置向导会引导你选择 3D 打印机型号并设置初始首选项。你也可以跳过此步骤，之后再手动配置。

### 开始切片

导入你的 3D 模型（STL、OBJ、3MF），调整打印设置，并为你的 3D 打印机生成 G-code。查看我们的[文档](../welcome-to-the-orcaslicer-wiki/)获取详细指南与技巧。加入我们的[Discord 社区](https://discord.gg/P4VE9UY9gJ)获取支持与交流。
