# Cannon

A few tips for using the Cannon phyiscs library with THREE.js

## Basic THREE JS example

[https://github.com/pmndrs/cannon-es/blob/master/examples/threejs.html](https://github.com/pmndrs/cannon-es/blob/master/examples/threejs.html)

## THREE vs CANNON

| THREE | CANNON |
| --- | --- |
| Scene | World|
| Scene.add()  | World.addBody() |
| Geometry| Shape |
| THREE.Material | CANNON.Material('name') |
| Mesh| Body |
| .position| .position |
| .quaternion| .quaternion |
| static object| body.mass = 0 |

> [!WARNING]
> `THREE` and `CANNON` objects don't always have the same conventions for the center of the object and its dimensions.

```javascript
const cubeGeometry = new THREE.BoxGeometry(1, 1, 1)
// ...
const cubeShape = new CANNON.Box(new CANNON.Vec3(0.5, 0.5, 0.5))
```

or [better](https://discourse.threejs.org/t/tutorial-three-js-cannon-es-in-typescript/42036/2) (more generic):

```javascript
const box3 = new Box3();
box3.expandByObject(target);

const objectSize = new Vector3();
box3.getSize(objectSize);

const shape = new Cannon.Box(new Cannon.Vec3(objectSize.x / 2.0, objectSize.y / 2.0, objectSize.z / 2.0);
```
More info here:

[https://sbcode.net/threejs/physics-cannonjs/](https://sbcode.net/threejs/physics-cannonjs/)

# Init wth gravity

See [https://pmndrs.github.io/cannon-es/docs/]([https://pmndrs.github.io/cannon-es/docs/)

```javascript
const world = new CANNON.World({
  gravity: new CANNON.Vec3(0, -9.81, 0)
})

```

## Update

```javascript

function animate() {
  requestAnimationFrame(animate)

  // world stepping...
  world.fixedStep()

  mesh.position.copy(body.position)
  mesh.quaternion.copy(body.quaternion)

  // three.js render...
}
animate()
```


## Apply a force

`applyForce` / `applyImpulse` ? => reset every frame to avoid accumulation issues...

=> consider setting `velocity` instead, see:

[https://github.com/schteppe/cannon.js/issues/257](https://github.com/schteppe/cannon.js/issues/257)

[https://stackoverflow.com/questions/72719561/applyimpulse-and-applyforce-accumulate-forces-they-dont-replace-them](https://stackoverflow.com/questions/72719561/applyimpulse-and-applyforce-accumulate-forces-they-dont-replace-them)

##  Trigger

[https://github.com/pmndrs/cannon-es/blob/master/examples/trigger.html](https://github.com/pmndrs/cannon-es/blob/master/examples/trigger.html)

## Debugger

[https://www.npmjs.com/package/cannon-es-debugger](https://www.npmjs.com/package/cannon-es-debugger)

![](https://i.imgur.com/2Bf8KfJ.png)

try it here (check source code):

[https://pmndrs.github.io/cannon-es-debugger/](https://pmndrs.github.io/cannon-es-debugger/)

## Tutorial

**Excellent tutorial** with code demonstrating dice physics:

[https://tympanus.net/codrops/2023/01/25/crafting-a-dice-roller-with-three-js-and-cannon-es/](https://tympanus.net/codrops/2023/01/25/crafting-a-dice-roller-with-three-js-and-cannon-es/)

