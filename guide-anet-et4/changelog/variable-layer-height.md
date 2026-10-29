# Variable Layer Height¶

The Variable Layer Height feature allows for dynamic adjustment of layer heights throughout the print, optimizing both print quality and speed.\
As we know from [Layer Height](/broken/pages/2c08bb28e128ee0601904ad0a628782951bc11ea), smaller layer heights yield better detail but increase print time, while larger layer heights speed up printing at the cost of detail. With Variable Layer Height, we can strategically use different layer heights in different parts of the model.

Note

The Min and Max layer heights are defined in the [Machine/Extruder settings](/broken/pages/54fc4ba47d549303cf6c193b25f9585c9e1bda1e#extruder-layer-height-limits).

## Adaptive[¶](variable-layer-height.md#adaptive) <a href="#adaptive" id="adaptive"></a>

The Quality / Speed slider in the Adaptive Variable Layer Height settings allows users to balance print quality and speed dynamically:

* **Quality:** Prioritizes finer details by using smaller layer heights in intricate areas, resulting in higher print quality but longer print times.
* **Speed:** Focuses on faster printing by utilizing larger layer heights in less detailed areas, reducing print time but potentially sacrificing some detail.

## Smooth[¶](variable-layer-height.md#smooth) <a href="#smooth" id="smooth"></a>

This setting allows you to set a Radius of the width of the Gaussian filter that smooths the transition between different layer heights. A larger radius results in a smoother transition, which can help reduce visible layer lines and improve overall print quality.

## Manual[¶](variable-layer-height.md#manual) <a href="#manual" id="manual"></a>

This tool enables a vertical bar with a preview of the layer heights along the model. You click with left mouse button to reduce the layer height at a specific point, or with right mouse button to increase it.
