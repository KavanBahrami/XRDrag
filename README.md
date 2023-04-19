# VR Drag Locomotion Move/Rotate/Scale

Unreal Engine Virtual Reality Drag Locomotion. Using Grip/Grab Input, Move / Rotate / Scale your VR Pawn.

## Demo
Check out the [demo video on YouTube](https://youtu.be/P7NQBMlyEJs) for Unreal Engine 5.1+.

![Demo GIF](MoveScaleRotate.gif)

... [earlier version](https://youtu.be/nO2tA2GukM4) with a buggy scale function

## Introduction

This blueprint code allows users to move their VR character by grabbing and pulling in the x, y, and z directions, as well as rotating around the Z-axis and scaling the world by pulling the controllers together or apart.

Currently has Z-axis Yaw rotation (rotate self in a circle around pivot), x/y/z grab/pull movement. There is no X-axis Roll rotation or Y-axis Pitch rotation, though Pitch might be added as an expanded comfort setting.

This my prefered way to move in smaller roomscale VR experiences, and is similar to the locomotion used in Unreal Engine's built-in VR Editor, TiltBrush (Unity), and Demeo (Unity). Oculus had a version of this in their locomotion samples [GrabAndDrag](https://developer.oculus.com/documentation/unreal/unreal-samples/) - though it ran on tick and didn't handle rotation. Some insight was gained from [this forum thread](https://forums.unrealengine.com/t/using-controllers-to-scale-rotate-re-position-world/74892/12), though much of the og post has missing images the conversation was useful. 

I took inspiration from some climbing mechanics and allow full 360 movement. With slight tweaking you could limit the motion to one plane if you wanted, so users can't move into the sky or down below your level. 

This took me a really long time to get working properly for my own project, and it was something that I wanted to share with the community, so I've stripped out this locomotion functionality and made it available here. If you do end up using in your own projects, please let me know, I'd love to know it's been helpful for other creators.

If you have any questions reach out.

## Getting Started

These instructions will get the default VR template to function using the Grip/DragRotateScale locomotion. The two included VRPawn blueprints have added code commented in hard-to-miss purple, I think it's easy to follow.

### Setup

1. If you're using Unreal Engine versions prior to 5.1, you'll need to enable the "Enhanced Input" plugin and update your project settings to use it.
	- Edit > Plugins > Enable "Enhanced Input" Plugin + Restart Now
	- Edit > Project Settings >
	- Change the Default Player Input Class to "Enhanced"
	- Change the Default Input Component Class to "Enhanced"
	
2. Close your project.

3. Copy the "VRGripMovement" folder into your project's "Content" directory.

4. Delete the unused VRPawn. For example, if you're using "VRPawn_ue51", delete "VRPawn_ue4" because it won't compile since it's using the previous default pawns no-longer-avail functions.

5. Open your project.

6. In the "VRTemplateMap", go to "World Settings" and override the "Default Pawn Class" under "Selected GameMode" with either "VRPawn_ue4" or "VRPawn_ue51", depending on your UE version.

7. **(For UE5.1+ only)** Update the default input mappings by adding both included grip inputs to the "IMC_Default" Input Mapping Context(IMC). A sample IMC "IMC_GripDragScale" is included for reference.
	- IMC_Default can be located in "VRTemplate > Input > "

8. Turn "Consume Input" OFF on the current two default Grab InputActions, "IA_Grab_Left" and "IA_Grab_Right".
	- The default Grab InputActions can be located in "VRTemplate > Input > Actions > "
	- Double click them and turn off the check box, on by default.

### Usage

Play in VR preview or build to HMD. Use either controller grips to move your VRPawn around the scene. Use both grips, grip and rotate controllers around each other to rotate your VRPawn around. Use both grips, pull together or apart, to adjust the world scale. Scaling only works on builds (standalone, toHMD, packaged), if you try to scale in VRPreview you'll just scale your hands but the world stays the same.

## Compatibility

This blueprint code has been tested with Unreal Engine 4.27 and Unreal Engine 5+, default VR Template project, Enhanced Input, and Meta Quest HMD (tested with both v1 and v2).

## Known Issues

- When updating to 5.1, backwards compatibility for the enhanced input actions was broken. To use this with any version prior to 5.1, you'll have to manually remake the Enhanced Input Actions and assign them, which isn't too difficult, but isn't ideal.

- Unreal has a long-known bug that prevents WorldToMetersScale from working if you have multiple editor tabs open, so to see the adjusted scale at runtime you need to close all tabs but the main map. This is an Unreal issue, not an issue with this implementation: https://forums.unrealengine.com/t/changing-world-to-meters-scale-at-runtime-disrupts-hmd-rendering-on-htc-vive/409868/8

- Because the Grip buttons are set to a locomotion action, if you use them to grab an object your hand will be fixed where you grab that object and you will be moving, rather than the object.



