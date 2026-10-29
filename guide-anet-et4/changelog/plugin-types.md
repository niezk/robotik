# Plugin Types¶

A plugin can provide one or more features. Expand a plugin row to see its plugin capabilities.

![local-plugin-activated-capabilities](<.gitbook/assets/local plugin activated capabilities.png>)

## Script[¶](plugin-types.md#script) <a href="#script" id="script"></a>

Script plugins are run manually from the Plugins window.

1. Open **File** > **Plugins**.
2. Expand the plugin.
3. Find the script feature.
4. Click the **Run** button.

![script-plugin-run-result](<.gitbook/assets/script plugin run result.png>)

## Slicing Pipeline[¶](plugin-types.md#slicing-pipeline) <a href="#slicing-pipeline" id="slicing-pipeline"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `slicing_pipeline_plugin`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Text list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--slicing-pipeline-plugin=value`.\
Slicing-pipeline plugins run at selected points in the slicing workflow. They can inspect or modify the live slicing graph, or edit the exported G-code at the post-processing step. This capability is experimental and intended for plugin developers and testers.

The plugin's capability appears in the appropriate plugin setting or workflow when it is enabled. The `psGCodePostProcess` step runs after the classic post-processing scripts and receives the working G-code path; geometry steps receive the active slicing context instead.

Warning

Slicing-pipeline plugins can change generated geometry or G-code. Review and test plugins from sources you trust before using them for a print.

## Pages[¶](plugin-types.md#pages) <a href="#pages" id="pages"></a>

Page plugins add their own tab to the main window, after OrcaSlicer's built-in tabs. The tab appears while the plugin feature is activated and disappears when it is deactivated.

If many page plugins are activated, set how many tabs are shown side by side in **Preferences** > **General** > **Plugins** > **Visible plugin pages** (1 to 10, default 5). The remaining pages are listed in a dropdown on the last plugin tab.

## Resource Textures[¶](plugin-types.md#resource-textures) <a href="#resource-textures" id="resource-textures"></a>

Resource-texture plugins contribute height-map images as a resource pack. Each plugin provides one pack of images, and the pack's name is how it appears in the app.

These plugins install as wheels (`.whl`) only, because a pack ships image files alongside its code.

Enabling, disabling, or uninstalling a pack adds or removes its textures, and the change shows up without a restart. A project that has already used a pack texture keeps working, because it stores its own copy of the image.

## Plugin Configuration[¶](plugin-types.md#plugin-configuration) <a href="#plugin-configuration" id="plugin-configuration"></a>

Select a plugin, open the **Config** tab, and select one of its capabilities. Edit the JSON configuration and click **Save**. **Restore defaults** removes the saved configuration for that capability and uses the plugin's default configuration.

When a preset uses a plugin capability, its configuration can also be overridden for that preset. The override is stored with the preset when you save it; otherwise the capability uses its global configuration.

## Speed Dial[¶](plugin-types.md#speed-dial) <a href="#speed-dial" id="speed-dial"></a>

The [Speed Dial](/broken/pages/19ee981c30c040011461e6761ad003abb8e6a613) allows quick access to installed plugins.

## Printer Connection[¶](plugin-types.md#printer-connection) <a href="#printer-connection" id="printer-connection"></a>

Printer connection plugins add printer communication features. The Printer Agent workflow is still WIP.

For printers that are not Bambu Lab printers, OrcaSlicer only sends print jobs through a printer connection plugin when **Preferences** > **Developer** > **Experimental Features** > **Use printer agents instead of print hosts** is enabled. It is off by default, so the classic print host upload is used.

Each printer connection has an ID. If a plugin's printer connection uses an ID that another plugin or a built-in connection already uses, OrcaSlicer shows a warning, turns that feature off, and marks the plugin with a **RuntimeError** status. See [Managing Plugins](/broken/pages/e8ccd807251d77b89c24bb5d39284c462165dfbd#plugin-status).

If the plugin has its own setup instructions, check the **Description** or **Diagnostics** tab in the Plugins window.
