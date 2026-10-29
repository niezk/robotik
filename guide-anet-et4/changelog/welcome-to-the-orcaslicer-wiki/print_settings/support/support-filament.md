# Support Filament¶

Support filament settings allow you to customize the material used for support structures in your 3D prints. You can choose separate filaments for the support base and raft, and for the support interface.

* [Base](support-filament.md#base)
* [Interface](support-filament.md#interface)
  * [Avoid interface filament for base](support-filament.md#avoid-interface-filament-for-base)
  * [Interface filament transitions](support-filament.md#interface-filament-transitions)

## Base[¶](support-filament.md#base) <a href="#base" id="base"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_filament`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-filament=1`.\
Filament to print the support base and raft. "Default" means no specific filament for support, and the current filament is used.

## Interface[¶](support-filament.md#interface) <a href="#interface" id="interface"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_interface_filament`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#integer-float-percentage): `Integer`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-interface-filament=1`.\
Filament to print the support interface. "Default" means no specific filament for the support interface, and the current filament is used.

### Avoid interface filament for base[¶](support-filament.md#avoid-interface-filament-for-base) <a href="#avoid-interface-filament-for-base" id="avoid-interface-filament-for-base"></a>

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Simple`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `support_interface_not_for_body`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#boolean): `Boolean`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--support-interface-not-for-body=1`.\
Avoid using the support interface filament to print the support base if possible. This option is shown only when an interface filament is selected and **Support/raft base** is `Default`.

This affects the support **body** only. It is a separate thing from the bonding layer described below, which is part of the interface itself.

### Interface filament transitions[¶](support-filament.md#interface-filament-transitions) <a href="#interface-filament-transitions" id="interface-filament-transitions"></a>

When you give the interface its own filament, the two materials have to meet somewhere. Rather than stacking the interface material straight onto the support body, Orca prints the **last** interface layer — the one at the back of the interface, touching the support body and furthest from the model — in the base filament. That layer is still shaped like an interface, with the same spacing and density, so the interface material lands on a solid, well matched surface instead of on open support lines.

How many layers you get of each material depends on the [Interface layers](/broken/pages/3f8a8399cbd6c2877a5fa0209e485a798a78d168#interface-layers) count:

| Interface layers | Interface filament             | Base filament |
| ---------------- | ------------------------------ | ------------- |
| 1                | 1 (the layer facing the model) | 0             |
| 2                | 1                              | 1             |
| 3                | 2                              | 1             |
| N                | N − 1                          | 1             |

The layer facing the model is always the interface material, so if you want the interface printed purely in its own filament, set the count to `1`. From `2` upwards you always get exactly one bonding layer in the base filament, no matter how thick the interface is or what [Z distance](/broken/pages/3f8a8399cbd6c2877a5fa0209e485a798a78d168#z-distance) you use, except in the soluble case described in the note below. Top and bottom interfaces are worked out separately, each from its own count.

Note

A soluble interface sitting directly on a non-soluble base, with no Z gap, is split differently: up to half the layers, and never more than two, are printed in the non-soluble filament, so the soluble material has something rigid underneath it.

Worth knowing:

* Going from `1` to `2` interface layers does more than add a layer — it brings a second material into the interface, which means extra tool changes and purge on a multi-material printer.
* The bonding layer counts as support base, so speed and cooling settings you have tuned for the interface do not apply to it.
* If **Support/raft base** is left as `Default`, that layer prints in whatever filament is already loaded, normally the one the model is being printed with.
* Choosing an interface filament while **Support/raft base** is `Default` still counts as two different materials, because support filaments cannot be used for the support body.
