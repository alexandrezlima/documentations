---
hide:
    - navigation
---


# ICON GENERATOR | version 1.05
##### Last mod.: 2022/12/29

## Introduction: what does this asset do?
This asset allows you to create icons for objects in your game. It works with static meshes, skeletal meshes or blueprint actors. These icons can have a transparent background, a solid color or a texture as background. They can be loaded via data tables, automatic load (loading all the assets in the project, via folder scanning) or you can specify the folders your assets are in.

![Icon Generator V1.05](assets/icongenerator-assets/icon-generator-main.png)

| `background texture`     | `transparent background`  | `color background`  | `foreground + no background`  | `foreground + background`  |
|:----------------:|:----------------:|:----------------:|:----------------:|:----------------:|
| ![1](assets/icongenerator-assets/SM_MatPreviewMesh_02_512x512_2.png) {width=200} | ![1](assets/icongenerator-assets/SM_MatPreviewMesh_02_512x512.png) {width=200} | ![1](assets/icongenerator-assets/SM_MatPreviewMesh_02_512x512_1.png) {width=200} | ![1](assets/icongenerator-assets/SM_MatPreviewMesh_02_512x512_3.png) {width=200} | ![1](assets/icongenerator-assets/SM_MatPreviewMesh_02_512x512_4.png) {width=200} |

Using the export option, you can generate .png, .jpg, .TGA and other output formats. Using the import option, a texture will be generated inside your project folder. You can use your own background textures (and foreground), a transparent background, 
or any solid color as background.

## Getting started
### Unreal library
First of all, download and add it to your project. You can find it in your [Unreal Engine Library](https://www.unrealengine.com/marketplace/en-US/product/icon-generator).

<figure markdown>
  ![Unreal Engine Library](assets/icongenerator-assets/icon-generator-download.png){ width="250" }
  <figcaption>Unreal Engine Library</figcaption>
</figure>

### Setup
After adding the asset to your project, open the `M_IconSetup` map. It can be found in: `Content → Icon Generator → Maps`.

$under construction$