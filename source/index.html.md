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

# Quick Start

> A simple scene viewer application:

```javascript
// Import the base Oculus Mobile module
var app = require('ovrm-base');

// Set a scene for the application
app.setScene('theme-park.ovrscene');

// Print hello world

app.print("Hello World from Javascript!");
```

Once you've logged and created the .js that will drive your app, with a single line of code you can
create a virtual reality environment.

<aside class="notice"> For now, the only natively supported scene format is Oculus' <code>.ovrscene</code>. You can turn your <code>.fbx</code> files into <code>.ovrscene</code> using within the web app, or on your local machine using the SDK toolchain.</aside>

# Examples
## Creating an object
```javascript
// Create a new object based on a model package
var player = new SceneObject("batman.ovrscene");
```
Once created, object properties can be manipulated and animated. Before being visible, an object
has to get added to the scene.
## Adding an object to a scene
```javascript
// Add the previously created player object to the scene
app.addObject(player);
```
Use the application object's addObject function to add an object to the scene. Once added to the scene, objects will be displayed at their
set position and orientation.

## Manipulating an object
```javascript
// Changing an object's properties
player.x += .3;
player.y = maxHeight - 1.5;
player.rotationX = Math.PI / 2;
```
Object position and orientation can be manipulated directly on the object itself. Position (x, y, z) and orientation (rotationX, rotationY, rotationZ) are
immediately modifiable.

## Frame callbacks
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

# Video tutorial

<iframe style="margin-left: 15px" width="450" height="315" src="https://www.youtube.com/embed/FCKpRMZwByU" frameborder="0" allowfullscreen></iframe>
