# Cannon

A few tips for using the Cannon phyiscs library with THREE.js

## Basic THREE JS example

https://github.com/pmndrs/cannon-es/blob/master/examples/threejs.html

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

# Init wth gravity

See https://pmndrs.github.io/cannon-es/docs/

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

`applyForce` / `applyImpulse` ? => avoid, accumulation issues...

=> set `velocity` instead, see:

https://github.com/schteppe/cannon.js/issues/257

https://stackoverflow.com/questions/72719561/applyimpulse-and-applyforce-accumulate-forces-they-dont-replace-them

##  Trigger

https://github.com/pmndrs/cannon-es/blob/master/examples/trigger.html

## Debugger

https://www.npmjs.com/package/cannon-es-debugger

![](https://i.imgur.com/2Bf8KfJ.png)

try it here:

https://pmndrs.github.io/cannon-es-debugger/

## Tutorial

Excellent tutorial with code demonstrating dice physics

https://tympanus.net/codrops/2023/01/25/crafting-a-dice-roller-with-three-js-and-cannon-es/

