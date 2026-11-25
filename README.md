# GamutFuse

**The manuscript is in review at the moment. We will upload the code and the trained models here after it is accepted.**

This repository belongs to our paper *GamutFuse: Beyond Y-Channel Substitution in RGB–Infrared Fusion with Registration and Hue-Preserving Color Reconstruction* 


## Why we built it

Two practical issues kept coming back whenever we combined a color photo with an infrared one.

**One is geometry.** The two cameras never look at the scene from exactly the same spot, so their pictures do not line up.

**The other is color.** The common recipe merges the brightness channel and then pastes the original color back on. If the new brightness is far from the old one, some pixels no longer fit into the valid RGB range. They get cut off, and their color tone drifts.

## How it works

- **Line up first.** For every pair we look for a small affine warp (six numbers, each with a hard limit) that makes the edges of the two pictures agree, working from low to high resolution. Nothing is learned at this stage.
- **Merge the brightness.** A network does this part. It mixes a U-Net with the early layers of a ConvNeXt-Tiny (ImageNet weights) that both inputs go through.
- **Give the color back with a formula.** Each pixel keeps as much of its original chroma as the RGB range allows, so no value is ever cut off and the color tone stays put.

## Numbers

**EPFL RGB–NIR (143 test pairs, ten fusion methods)**

- Pairs that start 14 to 68 pixels apart end up 2.6 to 5.6 pixels apart on average, and 75 % to 79 % of them land within 3 pixels. None of the six registration methods we tested against it did better, at any level.
- Misaligned inputs hardly move our fusion scores (0.7 % at most). Methods built for aligned inputs drop by 11 % to 57 %. Our MI, VIF and Q<sup>AB/F</sup> are the highest of the ten.
- When the inputs are already aligned, we have the top MI (4.737) and tie for the top Q<sup>AB/F</sup> (0.599).
- Color: zero out-of-range pixels, zero opponent hue error, and the smallest CIELAB hue error and CIEDE2000 chroma and hue errors. Methods that swap the Y channel push up to 8.7 % of the pixels out of range.

**Thermal infrared (LLVIP, RoadScene, TNO)**

- Our hue error never goes above 0.017°, which is lower than every other method.


## Citing

```bibtex
@article{mahdizadeh2026gamutfuse,
  title   = {{GamutFuse}: Beyond {Y}-Channel Substitution in {RGB}--Infrared Fusion with Registration and Hue-Preserving Color Reconstruction},
  author  = {Mahdizadeh, Mohammad and Mirzayev, Temurbek},
  year    = {2026},
  note    = {Manuscript under review}
}
```

## License

Academic and other non-commercial research use is free, under the PolyForm Noncommercial License 1.0.0 (see `LICENSE`). For any commercial or industrial use, ask us first; it needs our written permission.

## Contact
Mohammad Mahdizadeh (Paul Mahdizadeh), m.mahdizadeh@newuu.uz

