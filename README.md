# Quest-Post-Processing
A barebones project in Unity 2019.4.28f1 set up with URP and PostProcessing with Bloom and ACES tonemapping for Oculus Quest

Project setup from scratch step-by-step from memory and scribbled notes:
I'm using Unity 2019.4.28
In the package manager I installed URP 7.6.0
Post Processing 3.1.1
Oculus Android 2.38.6
Oculus Desktop 2.38.4

in the asset store I searched for Oculus Integration and installed it - it might ask you to update some things, I just click yes to them and it should restart unity or you can close it and re-open it
  - I'm using a version from Feb 10, 2021, not sure if this is relevant

In Player settings I set the color space to linear (not sure this is necessaray but I like it)
Under graphics apis, make sure OpenGLES3 is above Vulkan by dragging

for XR settings I'm still using Legacy VR support, so click Virtual Reality Supported so it's on and add the Oculus SDK
I set Stereo Rendering Mode to "singlepass"

In my setup I'm using URP so in the sample scene I added a plane and a cube and I created two URP materials. For the cube I added a red color and emission color, but for emmission I cranked up the hdr to 10

get the oculus rig from the oculus folder which was added when you imported oculus integration and drag it into the scene. I use the OVRCameraRig. The camera component is attached to the OVRCameraRig/TrackingSpace/CenterEyeAnchor
Select that and under the camera component make sure Post Processing is checked on and Output/HDR is set to "Use Pipeline Settings"
While you're in there look at the OVRManager component and set the tracking origin type to "floor level".

For URP you'll need to create a scriptable render pipeline asset
Once you have it you can add it to your graphics settings. Also with the new pipeline asset selected you can go into the inspector and turn on hdr

now in the scene 
create volume / Global Volume
select the volume object and in the inspector under the Volume component in the profile filed click new to create a new profile
add override bloom
inside the profile you can click "add override" to add postprocessing features like bloom and tonemapping
set tonemapping to aces - in my opinion this is the most important thing
In bloom I had to play with threshold, intensity and scatter to get it to look right
In build settings make sure you're on the android platform and you should be able to build and run
