# Mesh Boolean¶

Mesh Boolean operations allow you to combine, subtract, or find the intersection of two or more mesh objects. This is particularly useful in 3D modeling and printing when you want to create complex shapes or modify existing ones.

This can be done using an object with more than one part, an assembly of multiple objects, or by using modifiers.

## Union[¶](mesh-boolean.md#union) <a href="#union" id="union"></a>

The Union operation combines two or more mesh objects into a single mesh. This is useful when you want to create a single object from multiple parts.

## Difference[¶](mesh-boolean.md#difference) <a href="#difference" id="difference"></a>

The Difference operation subtracts one mesh from another. This is useful for creating holes or cutouts in a mesh by removing the volume of another mesh.

## Intersection[¶](mesh-boolean.md#intersection) <a href="#intersection" id="intersection"></a>

The Intersection operation creates a new mesh from the overlapping volume of two or more meshes. This is useful when you want to isolate the common area shared by multiple objects.
