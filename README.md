# UE_VR_Locomotion_GripToMoveRotateScale
Unreal Engine Virtual Reality Grip/Grab Locomotion. Grab to Move / Rotate (Scale not quite working)

Using 4.27.2 default VR Template project
Quest HMD (1/2)

1. Edit > Plugins > Enable "Enhanced Input" Plugin
2. Restart Now
3. Edit > Project Settings >
	- Change the Default Player Input Class to "Enhanced"
	- Change the Default Input Component Class to "Enhanced"
4. Close your project
5. Copy the "VRGripMovement" folder into your project's Content directory
6. Open Project
7. Open VRTemplateMap > World Settings > Override Default Pawn with included "VRPawn_Duplicate"


---
Play in VR preview or Build to HMD
Use either grip to move your VRPawn around the scene. Use both grips to rotate your VRPawn around.
---
Scale is partially implemented but the BP nodes are disconnected. I haven't yet figured out how to get it to work without being super jittery.
If you know what needs to be done please let me know.

The VRPawn_Duplicate has two sections of added code, commented in hard to miss Purple, should be pretty easy to follow.
If you have any questions reach out.
