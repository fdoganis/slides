# THREE.js Tips
Subtleties and best practices

## Look at the [examples](threejs.org/examples)

- you can search the examples
- you can check the code of each example by clicking on the `<>` icon

## Use the [editor](threejs.org/editor)

- to understand the API (Nodes, Materials, Lights etc.)
- to load, resize, convert your models
- to create a scene and save it so that you can load it later in your code

## Give a `name` to your objects 

so that you can use [`getObjectByName`](https://threejs.org/docs/#api/en/core/Object3D.getObjectByName)

```js
scene.getObjectByName('name')
```

It also makes debugging easier.

:warning: Slow method, do not use during the animation loop.
:point_right: Retrieve the object once and [store it in a variable](https://discourse.threejs.org/t/effeciency-of-getobjectbyname-getobjectid/55014/2)

## [`userData`](https://threejs.org/docs/#api/en/core/Object3D.userData) is your friend

You can store anything in it, here are a few [examples](https://github.com/mrdoob/three.js/search?utf8=%E2%9C%93&q=userdata): 

```js
obj.userData.velocity.x = ...
```
See https://threejs.org/examples/webxr_xr_cubes.html

```js
obj.userData.isSelecting = true
```
See https://threejs.org/examples/webxr_xr_sculpt.html

```js
userData.physicsBody
```
See https://threejs.org/examples/physics_ammo_cloth.html

```js
object.userData.mass
```
See https://threejs.org/examples/physics_ammo_break.html

## Performance issues? Check the number of draw calls

```js
console.log(renderer.info.render.calls) 
```

## [`Group`](https://threejs.org/docs/index.html?q=group#api/en/objects/Group) your objects

Consider this as a single matrix, an empty object with children but no geometry 

## Avoid scaling your objects

- Add to group, and transform group
- Or [`applyMatrix4`](https://threejs.org/docs/#api/en/core/Object3D.applyMatrix4) on geometry

:warning: Slow! Modifies the vertex buffer!

## Use [`lookAt`](https://threejs.org/docs/index.html#api/en/core/Object3D.lookAt) for easy rotations

Often used for the camera but can be used for any object.

See the last part of https://threejs.org/manual/#en/scenegraph

## Hide / Show objects with [`obj.visible`](https://threejs.org/docs/index.html#api/en/core/Object3D.visible)

## Parse children

- using `traverse`
- See webgl_loader_3ds :

```js
object.traverse / scene.traverse 
  if(child.isMesh) child.material.map = ...
```

- using `obj.children.includes`
or other [Array](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/) methods


## Object manipulation

```js
obj.position.set

obj.rotateX

obj.position.distanceTo // most basic collision detection
```

## Center an object in its bounding box

```js
const mesh = new THREE.Mesh(geometry, createMaterial());
geometry.computeBoundingBox();
geometry.boundingBox.getCenter(mesh.position).multiplyScalar(-1);
```

See https://threejs.org/manual/#en/primitives
(search textgeometry)

## How to modify Geometry

Example: 

```js
 
const position = geometry.attributes.position;

position.usage = THREE.DynamicDrawUsage;
for ( let i = 0; i < position.count; i ++ ) {
  const y = 35 * Math.sin( i / 2 );
  position.setY( i, y );
}
```

See 

https://sbcode.net/threejs/geometry-to-buffergeometry/

https://github.com/mrdoob/three.js/blob/master/examples/webgl_geometry_dynamic.html


## Instancing

See batching example

## TWEEN / GSAP for smooth interpolation

- GSAP : cannot be used in commercial projects, avoid it
- TWEEN : import TWEEN

```js
import TWEEN from 'three/addons/libs/tween.module.js';
```


Tutorial:

https://sbcode.net/threejs/tween/



## Lifecycle / dispose

See https://threejs.org/manual/#en/cleanup

## Shadows / Lights

See https://threejs.org/examples/webgl_lights_hemisphere
 
## Three js Math

:warning: Objects are referenced, not copied by default.
Use `clone()`
Define and reuse temp vectors, quaternions, matrices
     

## Matrices

Local matrix: relative to parent
World matrix: relative to scene
       
## Custom shaders

## Three Shading Language (NEW!)

https://github.com/mrdoob/three.js/wiki/Three.js-Shading-Language

- Simpler than raw `glsl`
- More robust
- Optimized
- Renderer agnostic (your shaders will still work with `webgpu`)

## Useful for debugging

- Helpers
- Orbitcontrols
- Dat.gui
- Stats
- VR stats

### Dump SceneGraph

```js
(function printGraph( obj ) {
    console.group( ' <%o> ' + obj.name, obj );
    obj.children.forEach( printGraph );    
    console.groupEnd();
} ( scene ) );
```

See https://github.com/mrdoob/three.js/issues/10961



