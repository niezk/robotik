# Resource Texture¶

The `orca.resource_texture` module exposes `ResourceTexturePluginCapabilityBase` for plugins that contribute height-map textures as a resource pack.

| Base class                                                  | `get_type()` returns | Required methods                             | Invoked by                                      |
| ----------------------------------------------------------- | -------------------- | -------------------------------------------- | ----------------------------------------------- |
| `orca.resource_texture.ResourceTexturePluginCapabilityBase` | `ResourceTexture`    | `get_name()`, `get_texture_dir(self) -> str` | OrcaSlicer, when the capability is materialized |

Lifecycle hooks `on_load()` / `on_unload()` are optional and available on every capability (defaults do nothing).

## Minimal Shape[¶](resource-texture.md#minimal-shape) <a href="#minimal-shape" id="minimal-shape"></a>

```
import os
import orca


class WoodPack(orca.resource_texture.ResourceTexturePluginCapabilityBase):
    def get_name(self):
        return "Wood Pack"

    def get_texture_dir(self):
        return os.path.join(os.path.dirname(__file__), "textures")


@orca.plugin
class WoodPackPlugin(orca.base):
    def register_capabilities(self):
        orca.register_capability(WoodPack)
```

`get_name()` is the pack's display name, so it must be unique among the loaded packs of this type (see [Registry](/broken/pages/e9237445ce2779a3a8d22a43bf68a6f7ef40741a)).

## The texture directory[¶](resource-texture.md#the-texture-directory) <a href="#the-texture-directory" id="the-texture-directory"></a>

`get_texture_dir()` returns a directory the host scans for images.

| Rule       | Detail                                                                                                                                                            |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Formats    | `.png`, `.jpg`, `.jpeg`, `.bmp`, matched case-insensitively                                                                                                       |
| Depth      | one level, non-recursive; images in a subdirectory are not listed                                                                                                 |
| Location   | the resolved directory must sit inside the plugin's own folder. A directory outside it is refused, and a symlink inside the pack that resolves outside is skipped |
| File limit | at most 64 images are listed                                                                                                                                      |

`get_texture_dir()` runs once, under the GIL, when the capability is materialized, and the result is cached. A changed directory takes effect on reload, not while the plugin stays loaded.

A directory that is empty, missing, unreadable, or outside the plugin folder costs the pack its textures only: the plugin still loads, and the pack is left out. The reason is written to the session log.

## Packaging[¶](resource-texture.md#packaging) <a href="#packaging" id="packaging"></a>

Ship a wheel (`.whl`). An install copies a single entry file, so a `.py` plugin cannot carry sibling images; a wheel is one file, and the loader extracts it on demand with the images inside the package's own directory. See [Wheel (`.whl`) plugins](/broken/pages/f01750c44235f91218b636b49a12b62edede9051#wheel-whl-plugins).

## Lifecycle[¶](resource-texture.md#lifecycle) <a href="#lifecycle" id="lifecycle"></a>

The host tracks loaded and enabled packs. A pack's textures become available to OrcaSlicer when the capability loads and is enabled, and are dropped when it is disabled, unloaded, or uninstalled. No restart is needed. Anything that has already embedded one of a pack's textures keeps it, because it holds its own copy of the image bytes.

## See Also[¶](resource-texture.md#see-also) <a href="#see-also" id="see-also"></a>

* [Registry](/broken/pages/e9237445ce2779a3a8d22a43bf68a6f7ef40741a) - registration, capability name rules, and `ExecutionResult`.
