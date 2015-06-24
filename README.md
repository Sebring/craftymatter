# craftyMatter

> Crafty Wrapper for Matter.js physics library

## install 

Install the required packages:

```js
npm install craftyjs matter-js crafty-matter
```
Load the script on your HTML file:

```html
<script type="text/javascript" src="../path/to/craftyjs"></script>
<script type="text/javascript" src="../path/to/matter-js"></script>
<script type="text/javascript" src="../path/to/crafty-matter"></script>
```
And you're ready to go!

## Usage

### Init matter

Launch `Crafty.Matter.Init` passing an options object [optional].

```js
Crafty.Matter.init({
	debug : true,
	gravity : {
		x : 0,
		y : 0.098
	}
});
```

Options suported:

*debug*: will create a debug body for each entity containing the `Matter` component. It will
also highlight the physic world with a light green color.

*gravity*: by default { x: 0, y: 0 }

*size*: matter world size. by default { x: Crafty.viewport.width, y: Crafty.viewport.height }

### Component

```js
Crafty.e( '2D, DOM, Matter' )
	.attr({
		x : Crafty.viewport.width * 0.45,
		y : Crafty.viewport.height * 0.1,
		w : Crafty.viewport.width * 0.1,
		h : Crafty.viewport.width * 0.1,
		rotation : 15,
		matter : {
			isStatic : true
		}
	});
```

It will create a Matter rectangle body with the dimensions in the attr object. The matter sub-object allows you to set matter specific config to your entity body.

Objects rotation origin will automatically to center, to fit Matter-js. Changing the origin will give unexpected results.

### Modify matter directly

The matter body reference for an entity with the `Matter` component will be the property `_body`. Use it to apply matter changes directly.

```js
var entity = Crafty.e( '2D, DOM, Matter' )
	.attr({
		x : 300,
		y : 200,
		w : 100,
		h : 100,
	});

Matter.Body.setAngle( entity._body, Crafty.math.degToRad( 90 ) );
```

Also the `Crafty.Matter` contains a reference to `engine` and `world` matter components.

```js

Matter.World.add( 
	Crafty.Matter.world, 
	Matter.Constraint.create({
	    pointA: { x: 300, y: 100 },
	    bodyB: entity._body
	})
);
```