---
hide:
    - navigation

title: Orbit Camera
---

*[UE4]: Unreal Engine 4
*[UE5]: Unreal Engine 5

# ORBIT CAMERA | version 1.0
##### Last mod.: 2024-01

## Introduction
This asset enables the visualization of objects through orbital movement. You have the flexibility to choose the behavior: orbit under click location, around the object's center, or around its original pivot. The asset provides a range of variables for customization. Try the web demo at this [link](https://alexandrezlima.github.io/orbitcamerademo/) or download the Windows version for free at [this link](https://drive.google.com/file/d/15wPyf7BoVktPu3DqqN-iDd5KeHNA2Etk/view?usp=sharing).

## Getting started
### Unreal library
First of all, download and add it to your project. You can find it in your [Unreal Engine Library](https://google.com).

<figure markdown>
![Unreal Engine Library](assets/icongenerator-assets/icon-generator-download.png){ width="250" }
<figcaption>Unreal Engine Library</figcaption>
</figure>

### How to use
The orbit camera is a pawn class. That means it is controlled by a controller (any controller, you can use even the default controller, no need to setup it!).

Go to the `Content → OrbitCamera → Blueprints → BP_OrbitCamera`, drag and drop the `BP_OrbitCamera` into your level and that's all, after hitting play you'll control the orbit camera.

<figure markdown>
![Drag and drop](assets/orbitcamera-assets/orbit-camera-usage.png)
<figcaption>Drag and drop the `BP_OrbitCamera`</figcaption>
</figure>

You may want to customize the orbit camera settings. The process to edit it is very simple: click over the orbit camera in the world, go to the details panel and you'll notice a lot of exposed variables to customize.

<figure markdown>
![Orbit camera customizations](assets/orbitcamera-assets/settings.png)
<figcaption>Orbit camera settings</figcaption>
</figure>

Each variable has a tooltip with a description that tells you what it does (hover the mouse cursor over the variable). If you want to test most of the variables at runtime, make sure to mark the variable `bEnableDebugMenu` as `True` and a menu will show up after you hit `play`.

<figure markdown>
![Orbit camera customizations](assets/orbitcamera-assets/orbit-camera-debug.png)
<figcaption>Orbit camera settings</figcaption>
</figure>

With this menu you can change the settings at runtime and check how it impacts in the camera behavior. Take your time and tweak it!

#### Orbit mode




??? info "Testing the demo level"
	After adding the asset to your project, you can test it by opening the `L_Showcase` map. It can be found at: `Content → OrbitCamera → Demo → Maps`.

	<figure markdown>
	![Unreal Engine Library](assets/orbitcamera-assets/orbit-camera-map.png)
	<figcaption>Orbit Camera map</figcaption>
	</figure>

	Once in the map level, you can hit play and try out 4 cameras in the level. They're all the same camera class with different settings (you can customize these settings by clicking over the camera and checking the details panel).

	<figure markdown>
	![Orbit camera customizations](assets/orbitcamera-assets/settings.png)
	<figcaption>Orbit camera settings</figcaption>
	</figure>


### Screenshots and album

### Variables
You can find the variables descriptions below. All the variables have a tooltip in the project (to check there, just hover over the variable!).

??? abstract "Variables"
    --8<-- "docs/codes/orbitcamera/orbit-cam-variables.txt"

### Controls
The orbit camera has some input controls:

| 	`Key`     			| `Action/Description`
|	----------------:	| :----------------
|	Left mouse button 	| Click to focus on an object or point (if the orbit mode is `OnClickedLocation`, `OnObjectCenter` or `OnObjectPivot`)
|	Right mouse button	| Click and hold. Move the mouse to move the rotate the camera.
|	Middle mouse button	| Click and hold. Move the mouse to move the camera (pan).
|	Middle mouse button	| Double click. Set the focus under the mouse position in the world.
|	Middle mouse button	| Triple click. Remove the focus and set it to the default focus.
|	R 					| Resets the camera position (shortcut).

All the keys are customizable, you can change it to your own controls and adapt it to use with touch devices (for this case, check the touch section).


### Update log
**`2024/02:` version 1.0 launch.**

### Questions and Answers

??? question "I would like to try this asset. Do you have any demo available?"
	Yes! You can try this asset directly in your browser at this [link](https://alexandrezlima.github.io/orbitcamerademo/) or you can download the Windows version at [this link](https://drive.google.com/file/d/15wPyf7BoVktPu3DqqN-iDd5KeHNA2Etk/view?usp=sharing). This demo brings a debug menu where you can test a lot of customization options at runtime that are available in the asset. The web demo version doesn't supoport high resolution screenshots and the blur effects are reduced compared to the desktop version.

??? question "Can I have more than one camera in my level?"
	Yes, you can have one or multiple orbit cameras in your level. For example, you can setup multiple cameras to view different points of an object. You can limit the movement and rotation of each camera individually.

	To control the first possessed camera, make sure to click over your secondary cameras, go to the details panel and mark `Auto Possess Player` as `Disabled`.

	If you want to be able to switch over multiple cameras at runtime, mark the `bShowCamerasMenu` variable as `True` in the `BP_OrbitCamera` blueprint. A menu will show up with your multiple cameras. You can edit their names in the `CameraName` variable in the details panel of each camera (this name will be displayed in the widget).

??? question "Can I choose a different path for my screenshots?"
	Yes, you can. First, make sure to mark `bCustomScreenshotPath` variable as `True`. Then, you can set the custom path in two ways: 1) call the function `SetScreenshotPath` (for example in the begin play node) and pass your path as a parameter; or 2) set the `CustomScreenshotPath` string variable with your custom path.

??? question "Can I increase the screenshot resolution?"
	Yes, you can increase the screenshot resolution. Open the `GetScreenshotResolution` function in the `BP_OrbitCamera` blueprint and edit the resolution return. By default, the screenshot resolution is the same as your application window size.

	<figure markdown>
	![Screenshot resolution](assets/orbitcamera-assets/screenshot-resolution.png)
	<figcaption>Screenshot resolution</figcaption>
	</figure>