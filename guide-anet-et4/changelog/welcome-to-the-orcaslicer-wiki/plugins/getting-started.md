# Getting Started¶

Plugins add extra features to OrcaSlicer. They are managed from the Plugins window.

Important

NEW FEATURE: **Python Plugin System**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

* [Local Plugins](/broken/pages/b3dcaea65c240db3d8c707fc23633ef32f3fc6e1)
* [Cloud Plugins](/broken/pages/88983d82c7b1961edec0eff9cef807020b87e4b5)
* [Plugin Types](/broken/pages/2fa3de38bea8cd1ecedaffd1347aed0b4843c419)
* [Managing Plugins](/broken/pages/e8ccd807251d77b89c24bb5d39284c462165dfbd)

## Open the Plugins Window[¶](getting-started.md#open-the-plugins-window) <a href="#open-the-plugins-window" id="open-the-plugins-window"></a>

1. Open the main menu.
2. Click **Plugins**.

![open-plugins-menu](<../../.gitbook/assets/open plugins menu.png>)

The Plugins window shows installed and available plugins. The upper table lists plugins, and the lower section shows details for the selected plugin.

The details section includes these tabs:

* **Plugin Info** — source, author, version, capabilities, and status.
* **Description** — information supplied by the plugin author.
* **Config** — configuration for the selected plugin's capabilities.
* **Changelog** — available version history.
* **Diagnostics** — loading and error information.

Every capability has a configuration. OrcaSlicer provides a JSON editor by default; a plugin can provide a custom configuration page instead. See [Plugin configuration](/broken/pages/f01750c44235f91218b636b49a12b62edede9051#capability-configuration) for the plugin-author API.

![plugins-dialog-empty](<../../.gitbook/assets/plugins dialog empty.png>)

Use the split **Browse plugins** button to choose how you want to add plugins:

* **Browse plugins** opens the cloud plugin browser.
* **Install local plugin** installs a plugin file from your computer.

![plugins-browse-menu](<../../.gitbook/assets/plugins browse menu.png>)

Note

Only install plugins from sources you trust. Plugins can interact with your files and print workflow.
