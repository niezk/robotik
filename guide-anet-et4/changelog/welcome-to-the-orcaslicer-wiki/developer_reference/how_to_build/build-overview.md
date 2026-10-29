# Build Overview¶

OrcaSlicer builds from source on Windows, macOS, and Linux. Each platform has its own tools and build script:

* [Build on Windows](/broken/pages/410d4c6cff4dde672086ba2454c6d3423727c680)
* [Build on macOS](/broken/pages/0ae7328d11e9d4b62cea7995396c4cfd3500aea0)
* [Build on Linux](/broken/pages/4192bf3da572f4d6ec21c31c278451f57c4fcc95)
* [Compiler Caching](/broken/pages/f1b6a47d8244a0ef789baf8a0cea03450c07cbac)

## Build Stages[¶](build-overview.md#build-stages) <a href="#build-stages" id="build-stages"></a>

Every platform builds in the same two stages, and each build script can run either on its own:

1. **Dependencies.** Third-party libraries such as Boost, wxWidgets, TBB and OpenCV are compiled once under `deps/` and installed into a prefix there.
2. **OrcaSlicer.** The application is compiled and linked against that prefix.

The dependency stage is skipped on later builds unless you delete its build directory, so the first build takes far longer than later ones. It is also why a dependency change has to be rebuilt on its own; each platform page explains how.

## Running the Tests[¶](build-overview.md#running-the-tests) <a href="#running-the-tests" id="running-the-tests"></a>

See [How to Test](/broken/pages/722203a3f3a5837fbab40181145e7552a6c2afad).

## Portable User Configuration[¶](build-overview.md#portable-user-configuration) <a href="#portable-user-configuration" id="portable-user-configuration"></a>

Place a folder named `data_dir` next to the OrcaSlicer executable and OrcaSlicer uses it as its configuration directory. That gives you a portable installation on a USB stick, or several profile sets kept isolated.

Nothing needs recompiling, and each copy set up this way keeps its own user data.

### Example Folder Structure[¶](build-overview.md#example-folder-structure) <a href="#example-folder-structure" id="example-folder-structure"></a>

```
OrcaSlicer.exe
data_dir/
```
