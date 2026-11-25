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
**Thermal infrared (LLVIP, RoadScene, TNO)**


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
MIT License

## Contact
Mohammad Mahdizadeh (Paul Mahdizadeh), m.mahdizadeh@newuu.uz

