# Raft¶

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variables](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `raft_layers`, `raft_contact_distance`, `raft_expansion`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb): `raft_layers` (Integer), `raft_contact_distance` (Float), `raft_expansion` (Float).\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--raft-layers=1` (`raft_layers` shown; other variables above follow their own type).\
A raft is a platform of support material printed under the object. The object is printed on the raft instead of on the build plate, and the raft is removed after printing.

A raft helps when:

* The material tends to warp or lift at the corners, like ABS, ASA, PC or Nylon.
* The object touches the bed with a small area, thin features or sharp edges that would not stay attached.
* The build plate is uneven or worn: the raft absorbs small height variations before the first object layer.

In exchange, the bottom of the object is rougher, the print takes more time and material, and the raft has to be removed.

Tip

If the problem is only adhesion or warping, try a [brim](/broken/pages/8f34753934cc3186e335ccb9927588ff743c306a) first. It is faster, uses less material and keeps the bottom surface clean.

* [How a raft is built](raft.md#how-a-raft-is-built)
* [Layers](raft.md#layers)
* [Contact Z distance](raft.md#contact-z-distance)
* [Expansion](raft.md#expansion)
* [Interaction with other settings](raft.md#interaction-with-other-settings)

## How a raft is built[¶](raft.md#how-a-raft-is-built) <a href="#how-a-raft-is-built" id="how-a-raft-is-built"></a>

The raft is made by the support generator, so it is printed with the support settings and filaments even when [supports](/broken/pages/a5ac9e1d60ddd3e6c582c4a55c887162b3caeab4) are disabled. When supports are enabled, the raft also extends under the supports that stand on the build plate.

From the build plate up, a raft has:

1. **First layer**: with two or more raft layers, printed at the [first layer height](/broken/pages/2c08bb28e128ee0601904ad0a628782951bc11ea#first-layer-height), with the [Initial layer density](/broken/pages/a5ac9e1d60ddd3e6c582c4a55c887162b3caeab4#initial-layer-density), and widened by the [Initial layer expansion](/broken/pages/a5ac9e1d60ddd3e6c582c4a55c887162b3caeab4#initial-layer-expansion) to stick to the bed. A one-layer raft has only the contact layer, printed at the first layer height with the interface settings described below and without the extra widening of the Initial layer expansion.
2. **Base layers**: sparse layers spaced by the [Base pattern spacing](/broken/pages/3f8a8399cbd6c2877a5fa0209e485a798a78d168#base-pattern-spacing) and printed with the [base support filament](/broken/pages/f8e8b0069c82289658d3b22b23006874c7d547b9#base).
3. **Interface layers**: denser layers that alternate direction, spaced by the [Interface spacing](/broken/pages/3f8a8399cbd6c2877a5fa0209e485a798a78d168#interface-spacing) and printed with the [interface support filament](/broken/pages/f8e8b0069c82289658d3b22b23006874c7d547b9#interface). The top one is the contact layer the object sits on.

Above the contact layer comes the [Contact Z distance](raft.md#contact-z-distance) gap, then the first layer of the object.

## Layers[¶](raft.md#layers) <a href="#layers" id="layers"></a>

Number of raft layers printed under the object. The object is raised by the height of the raft. `0` disables the raft.

Half of the layers, rounded up, are interface layers, and the rest are base layers. With two or more layers, the first layer counts as a base layer.

| Layers | Base layers | Interface layers               |
| ------ | ----------- | ------------------------------ |
| 1      | 0           | 1 (printed as the first layer) |
| 2      | 1           | 1                              |
| 3      | 1           | 2                              |
| 4      | 2           | 2                              |
| 5      | 2           | 3                              |

Except for the first layer, raft layers are printed at least 75% of the nozzle diameter thick, or at the [layer height](/broken/pages/2c08bb28e128ee0601904ad0a628782951bc11ea) if that is thicker, so the raft is usually thicker than the number of layers times the layer height.

Because the first layer height applies to the raft, the first layer of the object is printed at the normal layer height.

Tip

2 to 4 layers are enough for most prints. Use more layers when the build plate is uneven, or when the material warps strongly.

## Contact Z distance[¶](raft.md#contact-z-distance) <a href="#contact-z-distance" id="contact-z-distance"></a>

Vertical gap between the top of the raft and the bottom of the object.

* **Larger gap**: the raft is easier to remove, but the bottom of the object is rougher because its first layer is printed over the gap.
* **Smaller gap**: the bottom surface is smoother, but the raft is harder to remove.

The value is rounded to a multiple of the layer height, unless [Independent support layer height](/broken/pages/3f8a8399cbd6c2877a5fa0209e485a798a78d168#independent-support-layer-height) is enabled.

Note

This setting is hidden and ignored when the support top [Z distance](/broken/pages/3f8a8399cbd6c2877a5fa0209e485a798a78d168#z-distance) is `0`, which is meant for soluble supports. The object is then printed directly on the raft without a gap.

## Expansion[¶](raft.md#expansion) <a href="#expansion" id="expansion"></a>

Important

NEW FEATURE: **Raft expansion in the Raft settings**\
Available in: [Nightly builds](https://github.com/OrcaSlicer/OrcaSlicer/releases/tag/nightly-builds) or Releases greater than **2.4.2**.

Expands every raft layer in the XY plane around the first layer of the object. A wider raft spreads the warping forces over a larger area and gives the object a more stable base, at the cost of more material, longer print time and more space on the build plate.

This setting is shown only when [Layers](raft.md#layers) is above `0`.

Note

The [Tree Slim](/broken/pages/a5ac9e1d60ddd3e6c582c4a55c887162b3caeab4#tree-slim), [Tree Strong](/broken/pages/a5ac9e1d60ddd3e6c582c4a55c887162b3caeab4#tree-strong) and [Tree Hybrid](/broken/pages/a5ac9e1d60ddd3e6c582c4a55c887162b3caeab4#tree-hybrid) support styles ignore this setting and size the raft with the [Initial layer expansion](/broken/pages/a5ac9e1d60ddd3e6c582c4a55c887162b3caeab4#initial-layer-expansion) only, so the setting is disabled when one of them is selected.

When the raft has more than one layer, its first layer is widened again by the [Initial layer expansion](/broken/pages/a5ac9e1d60ddd3e6c582c4a55c887162b3caeab4#initial-layer-expansion), so with the default values it reaches 1.5 mm + 2 mm = 3.5 mm beyond the object.

Tip

Rafts of neighboring objects are not merged. When several objects with rafts share a plate, set the [Auto Arrange](/broken/pages/0fcd3913806f2ebe7be268c6b82f8de56ec468b6) spacing to at least twice the raft's reach, so their rafts do not overlap.

## Interaction with other settings[¶](raft.md#interaction-with-other-settings) <a href="#interaction-with-other-settings" id="interaction-with-other-settings"></a>

* [**Elephant foot compensation**](/broken/pages/c70b83c3a32422c9168494b30baab0b5314ff4ad#elephant-foot-compensation) is not applied when a raft is used, because the object is not printed on the build plate.
* [**Support ironing**](/broken/pages/0a96a23ec4091c1aefc9bca8a50840f599340f7a) can be enabled with a raft, even when supports are disabled, to smooth the top of the raft. Ironing also makes the raft interface layers solid.
* [**Prime tower**](/broken/pages/5aa3302c55047356a98465bb114707e629d121d9): all objects on the plate must use the same number of raft layers.
* [**Belt printers**](/broken/pages/226f2361e5d5e6ef3f7abf3becc7918d447a2ef7#features-that-are-not-available) cannot print a raft.
