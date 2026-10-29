# Build on macOS¶

How to building with Xcode on MacOS 64-bit.

* [MacOS Tools Required](build-on-macos.md#macos-tools-required)
* [MacOS Instructions](build-on-macos.md#macos-instructions)
* [Debugging in Xcode](build-on-macos.md#debugging-in-xcode)

## MacOS Tools Required[¶](build-on-macos.md#macos-tools-required) <a href="#macos-tools-required" id="macos-tools-required"></a>

* Xcode
* CMake
* Git
* gettext
* libtool
* automake
* autoconf
* texinfo
* pkgconf

Tip

You can install most of them by running:

```
brew install cmake gettext libtool automake autoconf texinfo pkgconf
```

Important

If you've recently upgraded Xcode, be sure to open Xcode at least once and install the required macOS build support.

Point the command-line tools at your Xcode installation and accept the license:

```
sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
sudo xcodebuild -license accept   # if you haven't accepted it yet
```

## MacOS Instructions[¶](build-on-macos.md#macos-instructions) <a href="#macos-instructions" id="macos-instructions"></a>

1. Clone the repository:

```
git clone https://github.com/OrcaSlicer/OrcaSlicer
cd OrcaSlicer
```

1. Build the application:

```
./build_release_macos.sh
```

> \[!TIP] If you're on the latest macOS and Xcode, set the deployment target explicitly so the build targets a supported SDK, e.g.:
>
> ```
> ./build_release_macos.sh -s -t 15.4
> ```

1. Open the application:

```
open build/arm64/OrcaSlicer/OrcaSlicer.app
```

## Debugging in Xcode[¶](build-on-macos.md#debugging-in-xcode) <a href="#debugging-in-xcode" id="debugging-in-xcode"></a>

To build and debug directly in Xcode:

1. Open the Xcode project:

```
open build/arm64/OrcaSlicer.xcodeproj
```

1. In the menu bar:
   * **Product > Scheme > OrcaSlicer**
   * **Product > Scheme > Edit Scheme...**
     * Under **Run > Info**, set **Build Configuration** to `RelWithDebInfo`
     * Under **Run > Options**, uncheck **Allow debugging when browsing versions**
   * **Product > Run**
