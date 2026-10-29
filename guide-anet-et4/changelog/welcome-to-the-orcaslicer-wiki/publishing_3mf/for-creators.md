# For creators¶

Publishing lets you share a repeatable configuration with a model. You choose which settings are included, embed whole filament presets, and require or suggest the materials a design needs.

## Publishing a project[¶](for-creators.md#publishing-a-project) <a href="#publishing-a-project" id="publishing-a-project"></a>

### Opening the dialog[¶](for-creators.md#opening-the-dialog) <a href="#opening-the-dialog" id="opening-the-dialog"></a>

**File → Publish 3MF…**, or `Ctrl`/`Cmd` + `Shift` + `E`. (Needs at least one object on the plate.)

Settings that differ from your base presets are pre-checked and bold; the rest start unchecked.

![publish\_dialog](../../.gitbook/assets/publish_dialog.png)

### Choosing what to include[¶](for-creators.md#choosing-what-to-include) <a href="#choosing-what-to-include" id="choosing-what-to-include"></a>

* **Filter box** ("Type to filter...").
* **All** / **None** buttons.
* **Filter menu** (right-click or the menu button): Select/Deselect All, Select/Deselect visible, and Filter selected / Filter non-selected.

If you check nothing, the file carries only the geometry.

### Printer tab[¶](for-creators.md#printer-tab) <a href="#printer-tab" id="printer-tab"></a>

One tab per extruder, each listing that extruder's **Retraction** and **Z-Hop** values.

![publish\_dialog\_printer\_settings](../../.gitbook/assets/publish_dialog_printer_settings.png)

### Filament tab[¶](for-creators.md#filament-tab) <a href="#filament-tab" id="filament-tab"></a>

One tab per filament slot. A slot publishes nothing until **Enable** is ticked.

An enabled slot offers:

* **Material** requirements (these don't publish values — they constrain what the receiver applies):
  * **Color** — the required filament colour.
  * **Type** — the required material family (e.g. `PLA`).
* **Full Publish** — embed the whole filament preset; disables the per-setting rows.

### Mixed filaments[¶](for-creators.md#mixed-filaments) <a href="#mixed-filaments" id="mixed-filaments"></a>

Enabling a particular mixed filament automatically selects the required filament components. ![publish\_dialog\_filament\_settings](../../.gitbook/assets/publish_dialog_filament_settings.png)

Note

If a mixed filament is enabled, but its required components are either disabled or have their type unchecked, a warning message will be shown. This does not prevent publishing. ![publish\_dialog\_mixed\_filament\_warning](../../.gitbook/assets/publish_dialog_mixed_filament_warning.png)

### Process tab[¶](for-creators.md#process-tab) <a href="#process-tab" id="process-tab"></a>

Mirrors the Process settings that you see in the sidebar.

> <img src="../../.gitbook/assets/publish_dialog_process_settings.png" alt="publish_dialog_process_settings" data-size="original">

## Tips[¶](for-creators.md#tips) <a href="#tips" id="tips"></a>

* **Publish only what matters.** Include just the settings that affect how the model prints.
* **Use Full Publish for filaments you tuned hard** — it embeds the whole preset in the file.
* **Name files clearly** — OrcaSlicer suggests `.published.3mf`.
* **Check the tab indicator dots** to see what you've selected before **OK**.

## Things to note[¶](for-creators.md#things-to-note) <a href="#things-to-note" id="things-to-note"></a>

* **A mixed filament needs its components to be published too** — otherwise they can lose their material on the other side.
* **Not every setting survives a round-trip** — mismatches are skipped and reported after load.
* **The receiver's preset library is never modified** — Full Publish presets live only in the loaded project.
* **Single-extruder printers get only the first extruder's values.**
