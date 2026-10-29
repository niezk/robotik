# Filament Tolerance Calibration¶

Each filament and printer combination can result in different tolerances. This means that even using the same filament and print profile, tolerances may vary from one printer to another. To correct for these variations, OrcaSlicer provides:

* Filament Compensation:
  * [Shrinkage (XY)](/broken/pages/517fb235be4603cea00c908adde9ed8048ec88d6#shrinkage-xy)
  * [Shrinkage (Z)](/broken/pages/517fb235be4603cea00c908adde9ed8048ec88d6#shrinkage-z)\
    ![FilamentShrinkageCompensation](.gitbook/assets/FilamentShrinkageCompensation.png)
* [Process Compensation](/broken/pages/c70b83c3a32422c9168494b30baab0b5314ff4ad):
  * [X-Y hole compensation](/broken/pages/c70b83c3a32422c9168494b30baab0b5314ff4ad#x-y-compensation)
  * [X-Y contour compensation](/broken/pages/c70b83c3a32422c9168494b30baab0b5314ff4ad#x-y-compensation)
  * [Precise wall](/broken/pages/c70b83c3a32422c9168494b30baab0b5314ff4ad#precise-wall)
  * [Precise Z height](/broken/pages/c70b83c3a32422c9168494b30baab0b5314ff4ad#precise-z-height)\
    ![QualityPrecision](.gitbook/assets/QualityPrecision.png)

Tip

Follow the recommended calibration order in the [Calibration Guide](/broken/pages/11c07341f1c2537a4800ccab7e8c9c26d87a5246).

## Handy Models[¶](filament-tolerance-calibration.md#handy-models) <a href="#handy-models" id="handy-models"></a>

OrcaSlicer includes several handy models to help you test and calibrate your printer.\
Right-click on your plate in Prepare mode and select "Add Handy Model" to access these models.\
![handy-models-list](<.gitbook/assets/handy models list.png>)

### Orca Tolerance Test[¶](filament-tolerance-calibration.md#orca-tolerance-test) <a href="#orca-tolerance-test" id="orca-tolerance-test"></a>

This calibration test is designed to evaluate the dimensional accuracy of your printer and filament. The model consists of a base with six hexagonal holes, each with a different tolerance: 0.0 mm, 0.05 mm, 0.1 mm, 0.2 mm, 0.3 mm, and 0.4 mm, as well as a hexagon-shaped tester.

![tolerance\_hole](https://www.orcaslicer.com/wiki/images/Tolerance/tolerance_hole.svg?raw=true)

You can check the tolerance using either an 6mm Allen key or the included printed hexagon tester. Use calipers to measure both the holes and the inner tester. Based on your results, you can fine-tune the X-Y hole compensation and X-Y contour compensation settings. Repeat the process until you achieve the desired precision.

![OrcaToleranceTes\_m6](.gitbook/assets/OrcaToleranceTes_m6.jpg) ![OrcaToleranceTest\_print](.gitbook/assets/OrcaToleranceTest_print.jpg)
