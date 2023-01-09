---
hide:
    - navigation
---
*[LTS]: Lock-on Targeting System


# Lock-on Targeting System V4

## Introduction
This project was influenced by the Souls series, especially Bloodborne.

<div class="grid" markdown>

=== ":material-image: Bloodborne"
    ![Bloordborne - Cleric Beast](assets/lockon-assets/cleric-beast.jpg)

=== ":material-image: Demon's Souls"
    ![Demon's Souls - Old King Allant](assets/lockon-assets/old-king-allant.jpg)

=== ":material-image: Dark Souls"
    ![Dark Souls - Taurus Demon](assets/lockon-assets/dark-souls.jpg)

=== ":material-image: Elden Ring"
    ![Elden Ring - Random enemy](assets/lockon-assets/elden-ring.jpg)

=== ":material-image: Sekiro"
    ![Elden Ring - Random enemy](assets/lockon-assets/sekiro.jpg)

</div>

Built to be precise and highly customizable, this system has math at its core. With a quick and easy installation, you can use it in the most varied projects. Made using blueprints only.

## Supported versions
Version 4.0 was launched for Unreal Engine 4.26 to 5.1. So you still have access to previous versions (all of them are compatible with 4.26-5.1), being version 3.0 available in 4.24-4.25 and version 2.0 available in 4.17-4.23. You can check the documentation for previous versions in the [{==#previous-versions==}](#previous-versions) section.

This new version brings a lot of new content, including a new input system (now you can switch targets in any direction), multitargeting system, simple softlock, native support for splitscreen projects and much more. Check it in the [{==#update log==}](#update-log) section.

### Supported projects
* Third and first person games
* Top/down games
* Fixed camera games
* Splitscreen games
* Network games

## Getting started

### Unreal library
First of all, download and add it to your project. You can find it in your [Unreal Engine Library](https://www.unrealengine.com/marketplace/en-US/product/lock-on-targeting-system).

<figure markdown>
  ![Unreal Engine Library](assets/lockon-assets/uelib.png){ width="300" }
  <figcaption>Unreal Engine Library</figcaption>
</figure>

### Setup
You can check out [this video](https://youtu.be/pr8rlD5Ygtc) to watch the LTS setup, or follow the steps below.
The LTS V4 uses two main components: the lock-on component and the target component. They were separated into _two_ for optimization and practicality purposes, so that only the necessary variables are used in the target. The main steps you'll check below are, in summary:

| `Lock-on component`             | `Target component`        | `Extra stuff: tips and customization` |
|-------------------------------|-------------------------|-------------------------------------|
| Adding lock-on component      | Adding target component | Debug component                     |
| Setting up the input settings | Setting up the sockets  | Reticle override component          |

### Adding the lock-on component
This component goes to the pawn you want to perform the lock-on action (so controlled by a player).

Open your character blueprint and go to the components panel (normally at the top left corner). Click `Add Component` and search for "Lock". Add the `BPC Lock On` component.


<figure markdown>
![Unreal Engine Library](assets/lockon-assets/components.png){ width="300" }
<figcaption>Lock-on component (BPC_LockOn)</figcaption>
</figure>

!!! info

    We'll take a look on the `BPC Lock On Debug` later.

This component is the LTS core. It contains several useful functions that you can check in details in the [{==#functions==}](#functions) section.

#### Lock-on setup
Now let's setup the action keys. Drag and drop the lock-on component from your components panel into your event graph.

<figure markdown>
![Lock-on reference](assets/lockon-assets/lock-on-reference.png){width=200}
<figcaption>Lock-on reference</figcaption>
</figure>

We'll call it `lock-on reference` from now on. Using this reference, call the function `LockOn Toggle`. Connect it to an event key you want or to an action key. This function is used to lock-on and unlock the target. You should have something like one of the two possibilities below:

<figure markdown>
![LockOn Toggle function](assets/lockon-assets/lock-on-toggle.png){width=450}
<figcaption>LockOn Toggle function</figcaption>
</figure>

##### Switch targets setup
To setup the targeting switch, go to your camera movement nodes, [if you have one](#lock-on-setup "If not, check the tip below."). Connect the boolean returned by the function `isLockedOn` of the `lock-on reference` to a `branch` node. In the `false` output, connect your current logic flow. In the `true` output, connect the corresponding `Swap Target` function of the `lock-on reference`: `Yaw` for left/right movement and `Pitch` for up/down movement. You should have something like this:

<div class="grid" markdown>

=== ":material-mouse: Mouse Input"
    ![Targeting switch - Mouse](assets/lockon-assets/mouse-swap.png)

=== ":fontawesome-solid-gamepad: Gamepad Input"
    ![Targeting switch - Gamepad](assets/lockon-assets/gamepad-swap.png)

</div>

Below you can use `copy to clipboard` note and paste the functions mentioned right into your blueprint.

??? abstract "Copy-paste"

    === ":octicons-file-code-16: `Swap Target Yaw`"
        --8<-- "docs/codes/lock-on/swap-target-yaw.txt"

    === ":octicons-file-code-16: `Swap Target Pitch`"
        --8<-- "docs/codes/lock-on/swap-target-pitch.txt"

    === ":octicons-file-code-16: `isLockedOn`"
        --8<-- "docs/codes/lock-on/locked-on.txt"

??? tip "Tip: how to free the movement axes"
    If you want to free the movement of one or both axis, you can use the functions `Filter Yaw Axis` and `Filter Pitch Axis` and mark the option(s) `Free Yaw Axis` or/and `Filter Pitch Axis` in the `BPC_LockOn` details panel to do it. [Here is a demonstrative video](https://youtu.be/fi-yxiadYgI). Below you can check the setup in the tabs.

    === ":material-axis: Free Axis options"
        ![Free Axis](assets/lockon-assets/free-axis.png)

    === ":material-mouse: Mouse Input"
        ![Targeting switch + filter - Mouse](assets/lockon-assets/mouse-filter.png)

    === ":fontawesome-solid-gamepad: Gamepad Input"
        ![Targeting switch + filter - Gamepad](assets/lockon-assets/gamepad-filter.png)

    ??? abstract "Copy-paste"
        === ":octicons-file-code-16: `Filter function`"
            --8<-- "docs/codes/lock-on/swap-target-example.txt"


??? tip "Tip: I do not have control over my camera in my game"
    If you do not have controls for your camera, you can use the same logic above, but using it on your functions to rotate the character or in the axis mappings for the mouse x and y (or gamepad stick). For example calling `Mouse X` and `Mouse Y` events (or the corresponding gamepad):

    <figure markdown>
    ![Setup example, without control over the camera](assets/lockon-assets/targeting-switch-example.png)
    <figcaption>Setup example, without control over the camera</figcaption>
    </figure>

    Feel free to copy and paste the nodes above using the code below.

    ??? abstract "Copy-paste"
        === ":octicons-file-code-16: `Swap Target: mouse and gamepad example`"
            --8<-- "docs/codes/lock-on/swap-target-example.txt"


If you do not want to use the mouse or/and gamepad to switch targets, but still can be able to switch them, you can use the function `Swap Target Manually` using the `lock-on reference`. This function requires as parameter a coordinate as following:

<figure markdown>
![Swap Target Manually](assets/lockon-assets/manually-swap.png){ align='left' width=500 }
![Coordinate system](assets/lockon-assets/coordinate.png){ align='right' width=290 }
<figcaption>Swap Target Manually and coordinate system</figcaption>
</figure>

??? abstract "Copy-paste"
    === ":octicons-file-code-16: `Swap Target Manually`"
        --8<-- "docs/codes/lock-on/swap-manually.txt"

The `X` and `Y` axes have the range `[-1, 1]`. For the `X` axis, -1 means left and +1 means right. For the `Y` axis, -1 means backwards and +1 means forwards. You can combine them to create a direction.

##### Quick notes
You can customize the lock-on component by clicking on the BPC_LockOn component and going to the details panel. There are several customization options, which will be discussed in the [{==#variables==}](#variables) section.

!!! warning "Collision detection"
    Before going further, please make sure to check the object collision types detection, on the `lock-on component` details panel. Here you choose what kind of `objects` will be considered as possible target.

    <figure markdown>
    ![Collision detection](assets/lockon-assets/Colision-type.png)
    <figcaption>Detected collision type</figcaption>
    </figure>


!!! Note "Variables and functions tooltips"
    All variables have a tooltip explaining what they do. To see it, just hover over the variable. The same is valid for any function: hover over the function or open it to see what it does.


### Adding target component
This component goes to any actor you want to be able to lock-on. The only requirement is that this target must have at least one component with collision, otherwise the target will not be detected by the lock-on system.

!!! warning "Component object collision type"
    Make sure that at least one component of the actor has as `Object Type` some type of collision present in the lock-on component. Otherwise this target will not be detected!

    <figure markdown>
    ![Object type](assets/lockon-assets/target-object-type.png)
    <figcaption>Object type in at least one component collision</figcaption>
    </figure>

    In this example, the object type is `WorldDynamic`, which is included in the array `Target Collision Type Filter` of the `lock-on component`. If it was `WorldStatic`, for example, you have two options: or to change the `object type` to something present in the `Target Collision Type Filter`, or to include `WorldStatic` in the `Target Collision Type Filter` array. You can find the collision going to details panel after clicking in one component inside the actor blueprint.

To add the `Target Component`, open the actor you want to be able to lock-on, go to the components panel. Click `Add Component` and search for "Target". Add the `BPC Target` component.

<figure markdown>
![Target Component](assets/lockon-assets/bpc-target.png)
<figcaption>Target component</figcaption>
</figure>

!!! info

    We'll take a look on the `BPC Reticle Override` later.


##### Choosing sockets to lock-on
After adding the `Target Component`, you need to choose the component(s) and socket(s) you want to lock-on on this actor. To do that, click on the `Target Component` and check the `details` panel. Search the variable `Mesh and Sockets` and add the component name you want to lock-on.

!!! danger "Attention"
    If this component is `inherited`, you need to use the component name which is enclosed in parentheses. For example, if I have a pawn and I want to add to lock-on the pawn `skeletal mesh`, I'll use its name enclosed in parentheses, because it is `inherited`, as showed below:
    <figure markdown>
    ![Component Inherited](assets/lockon-assets/target-inheritance.png)
    <figcaption>Inherited components are indicated as `(inherited)`</figcaption>
    </figure>
    In this example, I'll use `CharacterMesh0` as the component name. After that, you can add a socket present in this component. In my example, `spine_02`. If your component doesn't have sockets, you can leave it as "None" and edit the offset. Vector at the right side of the socket name is the offset in relation to the chosen socket.
    <figure markdown>
    ![Component, socket and offset](assets/lockon-assets/target-1.png)
    <figcaption>Chosen component, socket and offset</figcaption>
    </figure>
    If the component is not inherited, as the example below, you can use its normal name:
    <figure markdown>
    ![Target Component](assets/lockon-assets/target-2.png){ align=left }
    ![Component, socket and offset](assets/lockon-assets/target-3.png){ align=right width=600 }
    <figcaption>Chosen component not inherited, socket and offset</figcaption>
    </figure>

    ??? tip "Tip: how do I find sockets in a skeletal mesh?"
        You can find sockets by opening the skeleton of the skeletal mesh. You can copy the bone name of the skeleton you want to lock-on and use it as the socket name.

Notice that you can add more than one component, and for each component you can add multiple sockets. Thais means you can have targets with multiple lock-on points.

That's all for the `Target Component`. You can check some extra details in the [{==#variables==}](#variables) section, such as `bShowReticle` and `bIsTarget` variables.

!!! success "Setup finished"
    With these two components properly configured, you can use the Lock-on Targeting System V4.
    
    In the next sections, you'll see some details about the components and customization, but they're optional, not required to use the tool.



### Customization
Under construction.

#### Lock-on component
Under construction.

#### Target component
Under construction.

## Extra components
Under construction.

### Debug component
Under construction.

### Reticle override component
Under construction.

## Useful functions
Under construction.
### Lock-on component
Under construction.

### Target component
Under construction.

## Functions
You can find the functions descriptions below. They have a tooltip description and comments inside it (to check in the project, just hover over the function or open it!).

??? abstract "Functions descriptions"
    === ":material-table: `BPC_LockOn component`"
        --8<-- "docs/codes/lock-on/lock-on-functions.txt"
    === ":material-table: `BPC_Target component`"
        --8<-- "docs/codes/lock-on/target-functions.txt"
    === ":material-table: `BPC_LockOnDebug component`"
        This component doesn't have functions.
    === ":material-table: `BPC_TargetReticleOverride component`"
        --8<-- "docs/codes/lock-on/reticle-functions.txt"


## Variables
You can find the variables descriptions below. They have a tooltip in the project (to check there, just hover over the variable!).

??? abstract "Variables descriptions"
    === ":material-table: `BPC_LockOn component`"
        --8<-- "docs/codes/lock-on/lock-on-variables-table.txt"
    === ":material-table: `BPC_Target component`"
        --8<-- "docs/codes/lock-on/target-variables-table.txt"
    === ":material-table: `BPC_LockOnDebug component`"
        --8<-- "docs/codes/lock-on/debug-variables-table.txt"
    === ":material-table: `BPC_TargetReticleOverride component`"
        --8<-- "docs/codes/lock-on/target-reticle-variables-table.txt"

## Previous versions
* [Version 3.0 documentation | :material-unreal: 4.24-4.25](https://sites.google.com/view/lockontargetingsystem)
* [Version 2.0 documentation | :material-unreal: 4.17-4.23](https://sites.google.com/view/lockontargetingsystem#h.zba6c1gskubb)


## Update log
**`2023/01:` version 4.0 released.**
??? info "4.0 news"
    * New input system, switch targets in any direction
    * Use the target component in any actor with collision
    * Multitargeting in one or more meshes and sockets
    * Target preview option
    * Softlock (call the `softlock` function)
    * Several useful functions
    * Performance improved
    * Easier to use
    * First/third person support
    * Splitscreen support
    * Top/down games support
    * Network support

`2021/09:` version 3.0 released.

`2020/09:` version 2.0 released.

`2020/05:` version 1.0 released.

