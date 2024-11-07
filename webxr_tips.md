# WebXR Tips
Subtleties and best practices

## Look at the [THREE.js WebXR examples](https://threejs.org/examples/?q=webxr)

- you can search the examples
- you can check the code of each example by clicking on the `<>` icon

### 1️⃣ AR Cones

https://threejs.org/examples/webxr_ar_cones

Simplest AR example: when you tap on your mobile a cone appears
- WebXR AR module ```immersive-ar``` initilization sequence
- ```select``` event, XR equivalent to ```click```

### 2️⃣ AR Hit Test

https://threejs.org/examples/webxr_ar_hittest

Cast a ray on real world planar surfaces
- WebXR ```hit-test``` feature request
- interaction with the world


### 3️⃣ XR Dragging

![](https://threejs.org/examples/screenshots/webxr_xr_dragging.jpg)

https://threejs.org/examples/webxr_xr_dragging

Select cubes and drag them around
- ```selectstart``` and ```selectend``` events, XR equivalents to ```mousedown``` or ```touchstart``` and ```mouseup``` or ```touchend```
- ```object.attach()``` method to temporarily make an object follow the controller
- interesting use of ```object.userData```
- ```ShadowMaterial``` on the ground
- check if the current event comes from the ```screen``` of the device using

```js
event.data.targetRayMode === 'screen'
```

See WebXR API

https://developer.mozilla.org/en-US/docs/Web/API/XRInputSource/targetRayMode


which points to

https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API/Inputs

### 4️⃣ Ball Shooter

https://threejs.org/examples/webxr_xr_ballshooter

![](https://threejs.org/examples/screenshots/webxr_xr_ballshooter.jpg)

- instancing for improved performance
- ```connected``` and ```disconnected``` events on controller

## Advanced Features

### Depth sensing for realistic occlusions

![](https://threejs.org/examples/screenshots/webxr_xr_dragging_custom_depth.jpg)

https://threejs.org/examples/webxr_xr_dragging_custom_depth

Ask for the depth of the frame to hide virtual object behind real ones (not widely implemented, works great on Meta Quest 3)

- WebXR ```depth-sensing``` feature request
- custom depth processing on the GPU using shaders

### Mesh occlusions

You can use any mesh to occlude virtual objects. You need to set ```colorWrite = false```, ```depthWrite = true``` and ```depthTest = true```.
Works great with hands or wit a mesh of the real world that you might have scanned beforehand

### AR Shadows

Shadows are essential in AR and VR. They give cues to the brain to understand how far an object is from the ground.

Use ```ShadowMaterial``` a transparent material which can receive shadows

https://threejs.org/docs/#api/en/materials/ShadowMaterial

Example: https://threejs.org/examples/webxr_xr_dragging


```js
const floorGeometry = new THREE.PlaneGeometry( 6, 6 );
const floorMaterial = new THREE.ShadowMaterial( { opacity: 0.25, blending: THREE.CustomBlending, transparent: false } );
const floor = new THREE.Mesh( floorGeometry, floorMaterial );
floor.rotation.x = - Math.PI / 2;
floor.receiveShadow = true;
scene.add( floor );

```

### Haptic feedback

![](https://threejs.org/examples/screenshots/webxr_xr_haptics.jpg)

https://threejs.org/examples/webxr_xr_haptics

Make your VR controller vibrate

```js
const supportHaptic = 'hapticActuators' in gamepad && gamepad.hapticActuators != null && gamepad.hapticActuators.length > 0;

if(supportHaptic) {
  gamepad.hapticActuators[0].pulse(intensity, 100);

}
```

On your android phone you can use the vibration API (sadly unavailable on iOS as of nov 2024))

```js
navigator.vibrate(200); // vibrate for 200ms
navigator.vibrate([
  100, 30, 100, 30, 100, 30, 200, 30, 200, 30, 200, 30, 100, 30, 100, 30, 100,
]); // Vibrate 'SOS' in Morse.
```

### Eye tracking (Apple Vision Pro)



Use ```transient-pointer```

See https://webkit.org/blog/15162/introducing-natural-input-for-webxr-in-apple-vision-pro/


### WebXR Lighting

 https://github.com/immersive-web/lighting-estimation/blob/main/lighting-estimation-explainer.md

on iOS

```js
frame.getGlobalLightEstimate().then(lightProbe => {
  const ambientIntensity = lightProbe.indirectIrradiance; // @TODO: Fix me
  ambientLight.intensity = ambientIntensity;
  directionalLight.intensity = ambientIntensity * 0.5;
});
```

### WebXR world sensing


https://github.com/immersive-web/real-world-geometry

https://immersive-web.github.io/real-world-meshing/


iOS

https://github.com/MozillaReality/webxr-ios-js/blob/master/examples/sensing/index.html



```js
let worldInfo = frame.worldInformation;

if (worldInfo.meshes) 
...

```


## Device Detection

Make your WebXR app as responsive and cross-platform as possible. Reuse this code (MIT License) to detect the type of your current device

https://github.com/aframevr/aframe/blob/master/src/utils/device.js

Alternativly, you can use

```js
event.data.targetRayMode === 'screen'
```

as explained earlier

## Gestures

No more gestures, they need to be recoded from scratch. Here is an example (**WARNING: DO NOT reuse as-is, GPL license**)

https://github.com/NikLever/XRGestures/

## You can't move the camera!

The camera is "connected" to your head (or phone camera)

### Retrieve the head of the user

In raw WebXR: 

```js
XRFrame.getViewerPose();
```

In THREE.js, the pose of the head of the user is copied to the current camera, see

three.js/src/renderers/webxr
/WebXRManager.js

You simply need to retrieve the position of the camera to get the head of the user



## No more HTML Buttons

Unless WebXR DOM overlays are supported

https://github.com/immersive-web/dom-overlays

## Hand detection

See https://threejs.org/examples/webxr_vr_handinput_profiles

## Controller / Gamepad

Use Gamepad API https://www.w3.org/TR/gamepad/
WebXR Gamepad API https://immersive-web.github.io/webxr-gamepads-module/#dom-xrinputsource-gamepad

Or a wrapper suche as https://github.com/felixtrz/gamepad-wrapper

## WebXR Viewer / XR Player (iOS only)

### Face

https://github.com/MozillaReality/webxr-ios-js/blob/master/examples/face_tracking/index.html

No WebXR equivalent

https://github.com/immersive-web/body-tracking/blob/main/explainer.md



### Image detection

https://github.com/MozillaReality/webxr-ios-js/blob/master/examples/image_detection/index.html

See WebXR tracked image draft

https://github.com/MozillaReality/webxr-ios-js/blob/master/examples/image_detection/index.html


https://immersive-web.github.io/marker-tracking/


## Fonts

Use 3D Text, troika text, MeshUI or vrsandbox example HTMLMesh

