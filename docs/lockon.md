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

Built to be precise and highly customizable, this system has math at its core. With a quick and easy installation, you can use it in the most varied projects. 

## Unreal library
First of all, download and add it to your project. You can find it in your [Unreal Engine Library](https://www.unrealengine.com/marketplace/en-US/product/lock-on-targeting-system).

<figure markdown>
  ![Unreal Engine Library](assets/lockon-assets/uelib.png){ width="300" }
  <figcaption>Unreal Engine Library</figcaption>
</figure>

##Getting started

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

This component is the LTS core. It contains several useful functions that you can check in details in the [{==#Functions==}](#functions) section.

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

???+ tip "Tip: how to free the movement axes"
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


Lorem ipsum dolor sit amet, (1) consectetur adipiscing elit.
{ .annotate }

1.  :man_raising_hand: I'm an annotation! I can contain `code`, __formatted
    text__, images, ... basically anything that can be expressed in Markdown.



!!! warning "Collision detection"
    Make sure to choose the object collision type of your targets on the lock-on component variable [].


!!! Note "Variables and functions tooltips"
    All variables have a tooltip explaining what they do. To see it, just hover over the variable. The same is valid for any function: hover over the function or open it to see what it does.


### Adding target component

!!! warning "Component object collision type"
    Make sure the component you have chosen has some type of collision present on the lock-on component. Otherwise this socket will not be detected!


### Customization

### Lock-on component

### Target component

## Extra components

### Debug component

### Reticle override component


## Update log

## Previous versions

## Commands

## Functions

## Variables

## Questions and Review


* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

!!! warning "Phasellus posuere in sem ut cursus"
    
    Referências em: https://squidfunk.github.io/mkdocs-material/reference/admonitions/
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

#bloco expandido: usar ??? em vez de !!!, com um + na frente do ??? fica automaticamente expandido
???+ note "Phasellus posuere in sem ut cursus"
    
    Referências em: https://squidfunk.github.io/mkdocs-material/reference/admonitions/
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.


<figure markdown>
  ![Image title](https://dummyimage.com/600x400/){ width="300" }
  <figcaption>Image caption</figcaption>
</figure>

![Image title](https://dummyimage.com/600x400/eee/aaa){ align=left, width="400" }