# VR Locomotion Move Rotate Scale
Unreal Engine Virtual Reality Grip/Grab Locomotion. Grab to Move / Rotate / Scale.

YOUTUBE demo in UE 5.1 : https://youtu.be/P7NQBMlyEJs

![](MoveScaleRotate.gif)

YOUTUBE demo of an earlier version with a buggy scale function: https://youtu.be/nO2tA2GukM4

This is my preferred way to move around smaller roomscale VR scenes.
As seen in Unreal Engine's built-in VR Editor / TiltBrush (unity) / Demeo (unity) / and other experiences. I'm not sure how they did their versions. Oculus had a version of this in their locomotion samples [GrabAndDrag](https://developer.oculus.com/documentation/unreal/unreal-samples/) though it ran on tick and didn't handle rotation. I took inspiration from some basic climbing mechanics and allow full 360 movement. With slight tweaking you could limit the motion to one plane if you wanted, so users can't move into the sky or down below your level.

Currently has Z-axis Yaw rotation (rotate self in a circle around pivot), x/y/z grab/pull movement.
There is no X-axis Roll rotation or Y-axis Pitch rotation, though Pitch might be added as an expanded comfort setting.

```diff
- When updating to 5.1 I broke backwards compatability for the enahanced input actions, so for the moment,
- if you want to use this with any version prior to 5.1, you'll have to manually remake the Enhanced Input Actions
- and assign them etc, which isn't too difficult, but isn't ideal. Sorry :|
```
*step 1 can be skipped if using ue5.1+ since Enhanced Input is now on by default*
1. Add Enhanced Input.
	Edit > Plugins > Enable "Enhanced Input" Plugin + Restart Now
	Edit > Project Settings >
	- Change the Default Player Input Class to "Enhanced"
	- Change the Default Input Component Class to "Enhanced"
2. Close your project
3. Copy the "VRGripMovement" folder into your project's Content directory
4. Open Project
5. Open VRTemplateMap > World Settings > Override Default Pawn with included "VRPawn_ue4" or "VRPawn_ue51"
6. For UE5.1+ update the default input mappings: IMC_Default with both included grip inputs (sample IMC is included for reference)
- VRTemplate>Input>IMC_Default
7. Turn consume input OFF on the current two Grab(R/L) inputs.
8. Delete unused VRPawn, ex: if using VRPawn_ue51 delete VRPawn_ue4 as it won't compile since it's using the previous default pawns no-longer-avail functions.

Feature consists of 7 macros, 16 variables, 2 enchanced input actions, and two VRPawn samples (one for UE5.1 and another tested on UE4). The two included VRPawn blueprints have two sections of added code, commented in hard-to-miss Purple, should be pretty easy to follow.


Play in VR preview or Build to HMD. Use either controller grips to move your VRPawn around the scene. Use both grips, grip and rotate controllers around each other to rotate your VRPawn around. Use both grips, pull together or apart, to adjust the world scale. Scaling only works on builds (standalone, toHMD, packaged), if you try to scale in VRPreview you'll just scale your hands but the world stays the same.


If you have any questions reach out.

Tested with:
 - Unreal Engine 4.27
 - Unreal Engine 5+ 
 - default VR Template project
 - Enhanced Input (*I like it and it seems to be the way the engine is moving, but it could be replaced with default input mappings*)
 - Meta Quest HMD (*tested with both v1 and v2*)

Known Issues:
- ** When updating to 5.1 I broke backwards compatability for the enahanced input actions, so for the moment, if you want to use this with any version prior to 5.1, you'll have to manually remake the Enhanced Input Actions and assign them etc, which isn't too difficult, but isn't ideal. Sorry :|
- Unreal has a long-known bug that prevents WorldToMetersScale from working if you have multiple editor tabs open, so to see the adjusted scale at runtime you need to close all tabs but the main map. This is an Unreal issue, not an issue with this implementation: https://forums.unrealengine.com/t/changing-world-to-meters-scale-at-runtime-disrupts-hmd-rendering-on-htc-vive/409868/8
- Because the Grip buttons are set to a locomotion action if you use them to grab an object your hand will be fixed where you grab that object and you will be moving, rather than the gun or box (per default example). Since this isn't an issue in my experience I haven't built the required check into this code to decide how to react to different use cases. If you're using Grip buttons to grab objects you will need to do so.
- There might be a few unused variables. Since I stripped this feature from a live project I might have missed a variable to two. Sorry. If this was a paid plug-in I would have spent more time making it perfect, enjoy. 

Some insight was gained from this forums thread, though much of the og post has missing images the conversation was useful:
https://forums.unrealengine.com/t/using-controllers-to-scale-rotate-re-position-world/74892/12
