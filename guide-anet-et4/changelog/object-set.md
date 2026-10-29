# Object Set¶

The object set is the basic structure used to organize and manage 3D models within OrcaSlicer. It allows users to group multiple objects and their respective parts for easier manipulation, configuration, and slicing.

## Part[¶](object-set.md#part) <a href="#part" id="part"></a>

Each Object Set consists of one or more Parts.\
A Part represents a single 3D model or mesh that has been imported into the project. Each Part can have its own unique settings, such as print parameters, supports, and modifiers.

## Instance[¶](object-set.md#instance) <a href="#instance" id="instance"></a>

An instance is a specific instance of an Object Set placed on the print bed.\
All instances of the same Object Set share the same Parts, size, and settings. However, each instance can have its own position and rotation on the print bed.\
This could be useful when printing multiple copies of the same model while keeping same painted settings ([Color](/broken/pages/ce3f2c39bd778e693abe651878da8af77be3cdc4), [Fuzzy Skin](/broken/pages/d8d0341929abdb0d17007e2fa7d9f15256221cf7), [Seams](/broken/pages/499549f00852518c397f84b689890171edbe0e30), [supports](/broken/pages/e142152c4a8336fa79900a69f2cd265fa6e43ef5), etc).

## Splitting[¶](object-set.md#splitting) <a href="#splitting" id="splitting"></a>

### Split to Objects[¶](object-set.md#split-to-objects) <a href="#split-to-objects" id="split-to-objects"></a>

When selecting an Object Set with multiple Parts, users can choose to split the Object Set into individual Objects.\
Each Object will contain a single Part from the original Object Set.

### Split to Parts[¶](object-set.md#split-to-parts) <a href="#split-to-parts" id="split-to-parts"></a>

When selecting an Object with a single Part that contains multiple meshes, users can choose to split the Object into individual Parts.\
Each Part will represent a single mesh from the original Object and will allow for independent manipulation and settings.

![stl-transformation-split](<.gitbook/assets/stl transformation split.png>)
