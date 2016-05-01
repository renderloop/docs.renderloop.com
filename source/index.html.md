---
title: Renderloop - Documentation

language_tabs:

search: true
---

# Overview

With Renderhooks, our Javascript API, you can create virtual reality from the comfort of your browser.

The API is under heavy development, and is liable to change significantly. However, we'll try our best to maintain backwards compatibility within major versions.

If you happen to be particularly brave and want to help test our unstable development API, which
includes more features than what's publicly available, [send us an email](mailto:developers@renderloop.com).

Finally, we also really want to hear about what features you'd like to see, the bugs you find, or any general feedback on how to improve. Don't be shy, we'd love
to hear from you: [developers@renderloop.com](mailto:developers@renderloop.com).

# Quick start

> A simple scene viewer application:

```javascript
// Import the base Oculus Mobile module
var app = require('ovrm-base');

// Set a scene for the application
app.setScene('theme-park.ovrscene');

// Print hello world
app.print("Hello World from Javascript!");
```

Getting started takes a few steps:

1. Create a Renderhooks or OVRScript project
2. Make a build of your app
3. Install the app on your phone
4. Run the app and connect to it from your web browser

# API

## Renderhooks

```javascript
// Bind the right shader
gl.useProgram(pyramidProgram);

// Setup shader attributes and uniforms
setBuffersAndAttributes(pyramidAttributes);
setUniforms(pyramidUniforms);

// Draw our pyramid
gl.drawArrays(gl.TRIANGLES, 0, pyramidBuffer);
```

Renderhooks is the runtime that binds your scripts to the behind the scenes rendering work. It works similarly to other scripting runtimes -- sort of like Node or React Native.

You can use Renderhooks to give you access to the lowest level WebGL primitives and function calls, but also use higher level APIs like three.js. If you want to use your own rendering library, you can import it as well.

Finally, if you want to make apps specifically for GearVR, you'll have access to Oculus' native SDK. This lets you take advantage of their UI elements, and also their OVRScene format.

## OVRScript
```javascript
// Create a new object based on a model package
var player = new SceneObject("batman.ovrscene");
```
OVRScript gives you access to the native Oculus Mobile SDK API (in Oculus' terms, this is their "VR App Framework"). These bindings let you view .ovrscene files, but also use .ovrscene files as objects in your scene, play sounds, and use the Oculus specific UI widgets.

## WebGL
```javascript
// Clear the screen, calling OpenGL directly
gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);

// Create a shader
var program = gl.createProgram();

// Create and bind a buffer
var vertexBuffer = gl.createBuffer();
gl.bindBuffer( gl.ARRAY_BUFFER, vertexBuffer );
gl.bufferData( gl.ARRAY_BUFFER, vertices, gl.STATIC_DRAW );
```
You can call WebGL functions as if you were in a browser environment. The function parameters and return values are as they would be in a browser. So, for example, you can use glDrawArrays() to render objects in your scene.

# Examples

## Renderhooks: Setting up three.js

```javascript
// Import three.js
var THREE = require('three');

// Create a scene/camera
var scene = new THREE.Scene();
var camera = new THREE.PerspectiveCamera( fov, aspect, near, far );

// Create a renderer
var renderer = new THREE.WebGLRenderer();
```

The three.js API is available in both an OVRScript and a Renderhooks project. You can use it the same way you use three.js in any other projects.

## OVRScript: Creating an object
```javascript
// Create a new object based on a model package
var player = new SceneObject("batman.ovrscene");
```
Once created, object properties can be manipulated and animated. Before being visible, an object
has to get added to the scene.
## OVRScript: Adding an object to a scene
```javascript
// Add the previously created player object to the scene
app.addObject(player);
```
Use the application object's addObject function to add an object to the scene. Once added to the scene, objects will be displayed at their
set position and orientation.

## OVRScript: Manipulating an object
```javascript
// Changing an object's properties
player.x += .3;
player.y = maxHeight - 1.5;
player.rotationX = Math.PI / 2;
```
Object position and orientation can be manipulated directly on the object itself. Position (x, y, z) and orientation (rotationX, rotationY, rotationZ) are
immediately modifiable.

## OVRScript: Frame callbacks
```javascript
function onFrameCallback() {
    player.x += .1;
}

app.onFrameCallback = onFrameCallback
```
To animate an object, or make updates to the scene on a per frame basis, register a callback function. On every frame it will be called before
rendering occurs.
## Input callbacks

```javascript
function onInputCallback(event) {
    app.print("Received input event.");
}

app.onInputCallback = onInputCallback
```
To receive input from the GearVR HMD touchpad, register a callback function with the app object.

<aside class="notice">
Input isn't frame-precise and may be delayed by a frame.
</aside>

# OVRScript: Video tutorial

<iframe style="margin-left: 15px" width="450" height="315" src="https://www.youtube.com/embed/FCKpRMZwByU" frameborder="0" allowfullscreen></iframe>
