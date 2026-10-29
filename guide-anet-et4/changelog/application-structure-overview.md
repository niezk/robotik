# Application Structure Overview¶

WIP...

Warning

!! incomplete, possibly inaccurate, being updated with new info !!

## [`Plater`](https://github.com/OrcaSlicer/OrcaSlicer/blob/main/src/slic3r/GUI/Plater.hpp)[¶](application-structure-overview.md#plater) <a href="#plater" id="plater"></a>

Refers to the entire application. The whole view, file loading, project saving and loading is all managed by this class. This class contains members for the model viewer, the sidebar, gcode viewer and everything else.

## [`Sidebar`](https://github.com/OrcaSlicer/OrcaSlicer/blob/main/src/slic3r/GUI/Plater.hpp)[¶](application-structure-overview.md#sidebar) <a href="#sidebar" id="sidebar"></a>

This is relating the the sidebar in the application window

![full-sidebar](<.gitbook/assets/full sidebar.png>)

## [`ComboBox`](https://github.com/OrcaSlicer/OrcaSlicer/blob/main/src/slic3r/GUI/Widgets/ComboBox.hpp)[¶](application-structure-overview.md#combobox) <a href="#combobox" id="combobox"></a>

The drop down menus where you can see and select presets

![combobox](.gitbook/assets/combobox.png)

## [`Tab`](https://github.com/OrcaSlicer/OrcaSlicer/blob/main/src/slic3r/GUI/Tab.hpp)[¶](application-structure-overview.md#tab) <a href="#tab" id="tab"></a>

Refers to the various windows with settings. e.g. the Popup to edit printer or filament preset. Also the section to edit process preset and the object list. These 4 are managed by `TabPrinter`, `TabFilament`, `TabPrint` and `TabPrintModel` respectively.

![tab-popup](<.gitbook/assets/tab popup.png>)
