# THREE.UpdatableTexture

An extended `THREE.Texture` to provide support for partial updates, via [`texSubImage2D`](https://developer.mozilla.org/en-US/docs/Web/API/WebGLRenderingContext/texSubImage2D).

`UpdatableTexture` lets you update only a part of a texture: it's useful for incremental loads of large images, for tiled resources, etc.

**WARNING: requires a slightly modified version of three.js**

Check a [demo of partially updated texture](https://spite.github.io/THREE.UpdatableTexture/).

[![UpdatableTexture Demo](https://raw.githubusercontent.com/spite/THREE.UpdatableTexture/master/about/updatabletexture.jpg)](https://spite.github.io/THREE.UpdatableTexture)


#### How to use ####
Include the modified three.js lib and the script in your project:
```html
<script src="three_modified.js"></script>
<script src="UpdatableTexture.js"></script>
```

You can create `UpdatableTexture` like any other `THREE.Texture`:
```js
// UpdatableTexture has the same signature as THREE.Texture
let a = texture = new UpdatableTexture(); 
```
You have to attach a `renderer` to it (*this will change if this textures makes into three.js core*)
```js
texture.setRenderer( renderer );
```
You can modify the `UpdatableTexture` attributes the same way you do with `THREE.Texture`
```js
texture.minFilter = texture.magFilter = THREE.NearestFilter;
texture.generateMipmaps = false;
```
Since the `UpdatableTexture` will be updated from one or more pieces, first you need to set the size:
```js
texture.setSize( width, height );
```
From then on, you can use to update a part of the texture:
```js
texture.update( source, x, y );
```
`source` can be an `ArrayBufferView`, an `ImageData`, an `HTMLImageElement`, an `HTMLCanvasElement`, an `HTMLVideoElement` or an `ImageBitmap`.

`x` and `y` are the offsets inside the big texture in which to draw the smaller texture. The width and height of the smaller texture is read from the resource. Make sure offset plus dimensions is not bigger than the large texture dimensions.

### License ####

MIT licensed

Copyright (C) 2017 Jaume Sanchez Elias, http://www.clicktorelease.com

