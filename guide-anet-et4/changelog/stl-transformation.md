# STL Transformation¶

OrcaSlicer primarily relies on STL meshes for slicing, but STL files may come with several limitations.

Typically, STL files feature a low polygon count, which can adversely affect print quality.\
In contrast, STEP files offer the [option of importing](/broken/pages/f2c68b382bf7caa0d1c1d0addfed2d60d9583c14#importing-step-files) a higher-quality mesh that more accurately represents the original design. However, be aware that both high-polygon STL and STEP files can increase slicing time.

![stl-transformation-smooth-rough](<.gitbook/assets/stl transformation smooth rough.png>)

## Simplify model[¶](stl-transformation.md#simplify-model) <a href="#simplify-model" id="simplify-model"></a>

When working with models that have a high polygon count, the Simplify Model option can significantly reduce complexity and help decrease slicing times.

This function is especially useful for improving the performance of the slicer or achieving a specific faceted look for artistic or technical reasons.

To access the Simplify Model option, right-click on the object to simplify in the "Prepare" menu.

![simplify-menu](<.gitbook/assets/simplify menu.png>)

It is recommended to enable the "Show Wireframe" option when running a simplification process to visually inspect the outcome. However, be cautious: overly aggressive simplification may lead to noticeable detail loss, increased ringing, or other printing issues.

### You can Simplify your model using the following options[¶](stl-transformation.md#you-can-simplify-your-model-using-the-following-options) <a href="#you-can-simplify-your-model-using-the-following-options" id="you-can-simplify-your-model-using-the-following-options"></a>

* **Detail Level:** Control the level of detail in the simplified model by choosing from five preset options. This setting allows for a balance between mesh fidelity and performance.
* **Decimate Ratio:** Adjust the ratio between the original model's polygon count and that of the simplified model. For instance, a decimate ratio of 0.5 will yield a model with approximately half the original number of polygons.

## Fix Model[¶](stl-transformation.md#fix-model) <a href="#fix-model" id="fix-model"></a>

Important

NEW FEATURE: **Fix Model on every platform, Fix All and Fix All Plates** Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

Fix Model repairs the mesh errors that make a model slice unpredictably or break other tools such as cut, mesh boolean and painting. It works on Windows, macOS and Linux.

* [Running Fix Model](stl-transformation.md#running-fix-model)
* [What it fixes](stl-transformation.md#what-it-fixes)
* [Parts](stl-transformation.md#parts)
* [Painting](stl-transformation.md#painting)

### Running Fix Model[¶](stl-transformation.md#running-fix-model) <a href="#running-fix-model" id="running-fix-model"></a>

* **An object or a part:** right-click it in the 3D view or in the object list and choose **Fix Model**, or click the warning icon next to it in the object list.
* **A plate:** right-click a plate, in the 3D view or in the object list. **Fix All** repairs every object on that plate, and **Fix All Plates** every object of the project.
* **After a cut:** when a cut leaves open edges, the [Cutting Tool](/broken/pages/6926c4336cc1890b7d358be5a6c828112493e42c) offers to fix the result.
* **From the command line:** [`--repair`](/broken/pages/c4bdcf8107a63e5f7b78401a5f9b4cc677fe24b9#geometry) repairs every loaded model before slicing.

A progress dialog follows the repair and can cancel it. A notification then lists the models that were repaired and those that could not be, and counts the ones that needed no repair. Each run is a single undo step.

### What it fixes[¶](stl-transformation.md#what-it-fixes) <a href="#what-it-fixes" id="what-it-fixes"></a>

* **Holes and cracks** are closed, including gaps between triangles that should share corners and T-junctions. A missing cap at the end of a tube is filled as a ring, so the bore stays open.
* **Orientation:** flipped triangles take the orientation of their neighbours, and a model turned inside out is turned outward.
* **Duplicates:** coincident duplicate triangles are removed, and so is the internal wall between two solids that touch face to face.
* **Stray geometry:** flat patches and other pieces that enclose no volume are removed.
* **Self-intersections:** small ones inside a part, such as slivers and folds, are removed. Larger overlaps, such as two bodies crossing each other, are left in place, because slicing merges them anyway.
* **Nested shells** follow the same rule as slicing: a shell inside a solid that faces inward stays a cavity, and one that faces outward, adding nothing, is removed.

A model that needs no change is left untouched. A part that cannot be turned into a solid, such as a single flat sheet, is left as it was and listed as failed.

### Parts[¶](stl-transformation.md#parts) <a href="#parts" id="parts"></a>

Fix Model repairs each part in place and never splits it, so cavities stay cavities. When the repaired part holds several separate solids, [Split to Parts](/broken/pages/a8af0b8ce0249203e2777bb45c50be863fbaa112#split-to-parts) separates them.

### Painting[¶](stl-transformation.md#painting) <a href="#painting" id="painting"></a>

Painted supports, seams, colors and fuzzy skin stay on every part the repair does not change. On a part whose mesh changes, the painting is moved onto the repaired mesh when **Preferences > Developer > Keep painted feature after mesh change** is enabled, and removed otherwise.
