ENSG 2021 - WebXR - Projets - Handsfree

Handsfree uses MediaPipe which uses FaceMesh

# MediaPipe Handpose with code

tfjs-models/handpose at master · tensorflow/tfjs-models

https://github.com/LingDong-/handpose-facemesh-demos




https://github.com/LingDong-/handpose-facemesh-demos/tree/master/mediapipe-hand-3js-tf174-handv1

Check SinglePlayer 3D demo


Install model locally


https://github.com/LingDong-/handpose-facemesh-demos/issues/5#issuecomment-744151485

"
It is possible to run this offline, by downloading the entire model in a folder structure.
For example: https://glitch.com/edit/#!/networked-hand-3js-tf174-handv1
where the models are downloaded to the /public/frozen/models/ folder.
Simply change the path to point to the local link, and it should then work.
"


# Face Mesh

https://google.github.io/mediapipe/solutions/face_mesh

Example:
https://mediapipe.dev/demo/face_mesh


Code sample:

https://blog.tensorflow.org/2020/03/face-and-hand-tracking-in-browser-with-mediapipe-and-tensorflowjs.html?m=1


old version:

https://github.com/tensorflow/tfjs-models/tree/master/facemesh

=> simple API : facemesh > face > landmarks

new version:


https://github.com/tensorflow/tfjs-models/tree/master/face-landmarks-detection

Face Landmark Model

https://google.github.io/mediapipe/solutions/face_mesh#face-landmark-model

Paper

[Geometry from Monocular Video on Mobile GPUs]
(https://arxiv.org/abs/1907.06724)



FaceMeshGeometry

https://github.com/spite/FaceMeshFaceGeometry

Vertex IDs

https://user-images.githubusercontent.com/7452527/53465316-4a282000-3a02-11e9-8e85-0006e3100da0.png

https://github.com/tensorflow/tfjs-models/blob/master/facemesh/mesh_map.jpg

Mesh annotations

https://github.com/tensorflow/tfjs-models/blob/master/facemesh/src/keypoints.ts



Demos
With Keypoint subsets


https://awesomeopensource.com/project/LingDong-/handpose-facemesh-demos

>>> Great source code with reduced landmarks

See SinglePlauer 3D

https://github.com/LingDong-/handpose-facemesh-demos/blob/master/mediapipe-facemesh-3js-tf2/landmarks.js


FaceMesh2THREEjs
https://github.com/LingDong-/handpose-facemesh-demos/blob/master/mediapipe-facemesh-3js-tf2/sketch.js



https://mediapipe-facemesh-3js-tf2.glitch.me

=> almost works, but does not refresh properly?



Simple example: 2D lines

Old

https://github.com/tensorflow/tfjs-models/blob/master/facemesh/demo/index.js

New

https://github.com/tensorflow/tfjs-models/blob/master/face-landmarks-detection/demo/index.js


# JeelizAR

https://github.com/jeeliz/jeelizAR




# FaceFilter

https://github.com/jeeliz/jeelizFaceFilter


THREE JS cube


live demo

source code


https://jeeliz.com/demos/faceFilter/demos/threejs/gltf_fullScreen/

Snapchat clone!!


# Weboji

https://github.com/jeeliz/jeelizWeboji



NOTE: Weboji: good for Animoji on the web

Head rotation + expression
2D only?!


* face detection and tracking,
* detects 11 facial expressions,
* face rotation around the 3 axis,
* robust to lighting conditions,
* mobile friendly,
* examples provided using SVG and THREE.js.
