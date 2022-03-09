# UnrealEngine VR Locomotion GripToMoveRotateScale
Unreal Engine Virtual Reality Grip/Grab Locomotion. Grab to Move / Rotate / Scale.

This is my preferred way to move around smaller roomscale VR scenes. As seen in Unreal Engine's built-in VR Editor / TiltBrush (unity) / Demeo (unity) / and other experiences. I'm not sure how they did their versions, but Oculus also has a version of this in their locomotion samples [GrabAndDrag](https://developer.oculus.com/documentation/unreal/unreal-samples/) though it runs on tick and doesn't handle rotation. I took inspiration from some basic climbing mechanics because I'm building a project that allows full 360 movement. With slight tweaking you could limit the motion to one plane if you wanted, so users can't move into the sky or down below your level.

An earlier version of it: https://youtu.be/nO2tA2GukM4

Dependencies in my version, *recommended to avoid additional tweaking*:
 - Unreal Engine 4.27.2
 - default VR Template project
 - Enhanced Input (*I like it and it seems to be the way the engine is moving, but it could be replaced with default input mappings*)
 - Meta Quest HMD (*tested with both v1 and v2*)


**Setup:**
1. Edit > Plugins > Enable "Enhanced Input" Plugin
2. Restart Now
3. Edit > Project Settings >
	- Change the Default Player Input Class to "Enhanced"
	- Change the Default Input Component Class to "Enhanced"
4. Close your project
5. Copy the "VRGripMovement" folder into your project's Content directory
6. Open Project
7. Open VRTemplateMap > World Settings > Override Default Pawn with included "VRPawn_Duplicate"


Play in VR preview or Build to HMD. Use either controller grips to move your VRPawn around the scene. Use both grips, grip and rotate controllers around each other to rotate your VRPawn around. Use both grips, pull together or apart, to adjust the world scale.

The VRPawn_Duplicate has two sections of added code, commented in hard to miss Purple, should be pretty easy to follow.
If you have any questions reach out.

Known Issues:
- Unreal has a long-known bug that prevents WorldToMetersScale from working if you have multiple editor tabs open, so to see the adjusted scale at runtime you need to close all tabs but the main map. This is an Unreal issue, not an issue with this implementation: https://forums.unrealengine.com/t/changing-world-to-meters-scale-at-runtime-disrupts-hmd-rendering-on-htc-vive/409868/8
- Because the Grip buttons are set to a locomotion action if you use them to grab an object your hand will be fixed where you grab that object and you will be moving, rather than the gun or box (per default example). Since this isn't an issue in my experience I haven't built the required check into this code to decide how to react to different use cases. If you're using Grip buttons to grab objects you will need to do so.
- There might be a few unused variables. Since I stripped this feature from a live project I might have missed a variable to two. Sorry. If this was a paid plug-in I would have spent more time making it perfect, enjoy. 

Some insight was gained from this forums thread, though much of the og post has missing images the conversation was useful:
https://forums.unrealengine.com/t/using-controllers-to-scale-rotate-re-position-world/74892/12
