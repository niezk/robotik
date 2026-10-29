---
description: Official downloads
---

# Download OrcaSlicer

Stable

## Stable release

Pick your platform. On Windows we recommend the Microsoft Store build, and on Linux the Flathub build — both update automatically.

### Windows

[Microsoft Storerecommended](https://apps.microsoft.com/detail/9mv6gl23xm59) [Installer x64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest) [Installer ARM64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest) [Portable x64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest) [Portable ARM64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest)

### macOS

[Mac Universal](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest)

### Linux

[Flathubrecommended](https://flathub.org/apps/com.orcaslicer.OrcaSlicer) [AppImage x64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest) [AppImage ARM64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest) [Flatpak x64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest) [Flatpak ARM64](https://github.com/OrcaSlicer/OrcaSlicer/releases/latest)

Nightly

## Nightly builds

Fresh from the latest commits, with features that haven't shipped yet. Expect rough edges — nightly builds may be unstable.

### Windows

unstable [View nightly builds on GitHub](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds)

### macOS

unstable [View nightly builds on GitHub](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds)

### Linux

unstable [View nightly builds on GitHub](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds)

Requirements

## System requirements

### Windows

* Windows 10 or later (64-bit)
* 4GB RAM minimum (8GB+ recommended)
* OpenGL 3.3 compatible graphics card
* 500MB free disk space
* Internet connection for updates

### macOS

* macOS 10.15 (Catalina) or later
* 4GB RAM minimum (8GB+ recommended)
* Intel or Apple Silicon (M1/M2/M3)
* 500MB free disk space
* Internet connection for updates

### Linux

* Ubuntu 20.04+ or equivalent distribution
* 4GB RAM minimum (8GB+ recommended)
* OpenGL 3.3 compatible graphics card
* 500MB free disk space
* Internet connection for updates

Setup

## Installation guide

### Choose your platform

Select the appropriate download for your operating system from the download section above. For Windows, the Microsoft Store build is the easiest and keeps itself up to date; otherwise pick Installer or Portable (x64 for most PCs, ARM64 for Windows on ARM devices). For macOS, the universal build covers both Apple Silicon and Intel Macs. For Linux, we recommend installing from Flathub; the AppImage also works on most distributions.

### Download the file

Click the download button for your chosen platform. Direct downloads come from our official GitHub releases page — always verify you're downloading from github.com/OrcaSlicer/OrcaSlicer to ensure authenticity and security. Store builds come from the Microsoft Store and Flathub.

### Install OrcaSlicer

**Windows:** Run the .exe installer and follow the installation wizard. Or extract the portable version to any folder.\
**macOS:** Open the .dmg file and drag OrcaSlicer to your Applications folder.\
**Linux:**

AppImage Flatpak

1. Open a terminal in your Downloads folder.
2. Make it executable:
3. Run it:

**Tip:** If it won't launch, you may need FUSE. Install it with `sudo apt install libfuse2` (Ubuntu/Debian) or `sudo dnf install fuse` (Fedora).

1. Make sure Flatpak is installed — [flatpak.org/setup](https://flatpak.org/setup/) has distro-specific instructions.
2. Install from Flathub (recommended — updates automatically): Or, if you downloaded a `.flatpak` file from GitHub instead:
3. Launch from your app menu, or run:

**Note:** Flatpak runs in a sandbox. If you need to access files outside your home folder, use [Flatseal](https://flathub.org/apps/com.github.tchx84.Flatseal) to manage permissions.

### Launch and configure

Open OrcaSlicer from your applications menu. On first launch, the Configuration Wizard will guide you through selecting your 3D printer model and setting up initial preferences. You can skip this and configure manually later if preferred.

### Start slicing

Import your 3D models (STL, OBJ, 3MF), adjust print settings, and generate G-code for your 3D printer. Check out our [documentation](welcome-to-the-orcaslicer-wiki/) for detailed guides and tips. Join our [Discord community](https://discord.gg/P4VE9UY9gJ) for support and discussions.
