# How to Download Pull Requests Artifacts for Testing¶

When a Pull Request (PR) is created or updated in the [OrcaSlicer repository](https://github.com/OrcaSlicer/OrcaSlicer/pulls), GitHub Actions automatically builds the project and generates artifacts that can be downloaded for testing purposes.

Important

It's recommended to [Backup your Presets](/broken/pages/f2c68b382bf7caa0d1c1d0addfed2d60d9583c14#export-preset-bundle) before testing PR artifacts.

1. Log in to your GitHub account.
2. Open the Pull Request you want to test.
3. Navigate to the "Checks" tab located at the top of the PR page.\
   ![pr-artifacts-1](<../../.gitbook/assets/pr artifacts 1.png>)
4. In the "Checks" tab, look for the "Build all" section.\
   ![pr-artifacts-2](<../../.gitbook/assets/pr artifacts 2.png>)
5. **Scroll down** to find the "Artifacts" section.\
   ![pr-artifacts-3](<../../.gitbook/assets/pr artifacts 3.png>)
6. Click on the artifact name or its download button to download the ZIP file containing the build artifacts.
   * Windows:
     * `OrcaSlicer_Windows_[PR_NUMBER]_portable` : Portable Version, **RECOMMENDED** for testing.
     * `OrcaSlicer_Windows_[PR_NUMBER]` : Installer Will overwrite existing installations.
   * macOS:
     * `OrcaSlicer_Mac_universal_[PR_NUMBER]` : Universal macOS DMG file.
   * Linux:
     * `OrcaSlicer-Linux-flatpak_[PR_NUMBER]_x86_64.flatpak` : Flatpak for x86\_64.
     * `OrcaSlicer-Linux-flatpak_[PR_NUMBER]_aarch64.flatpak` : Flatpak for ARM64.
     * `OrcaSlicer_Linux_ubuntu_2404_[PR_NUMBER]` : Ubuntu 24.04 DEB package.
7. Once downloaded, extract the ZIP file to access the build artifacts.

Tip

Share this guide to others!

Short Link:

```
https://www.orcaslicer.com/wiki/how_to_download_pr_artifacts
```

Markdown Link:

```
[How to Download Pull Requests Artifacts for Testing](https://www.orcaslicer.com/wiki/how_to_download_pr_artifacts)
```
