# Ara3D Online Model Viewer 

The Ara 3D Viewer is an open-source and easy to configure and use 3D model viewer built as a thin wrapper on top of the popular [Three.JS](https://threejs.org) library. 

The Ara 3D viewer combines the Three.JS library with several common loaders and utilities, and a boilerplate helper, into a single file (`ara3d-viewer.js`) making it easy to integrate a custom 3D viewer into your website with just a couple of lines of code. 

The goal of the Ara3D online model viewer is to enable users to be able to start leveraging the power of WebGL and Three.JS to integrate 3D content in their web application and HTML pages with a minimal investment of time learning about 3D and Three.JS.

## Features 

* Orbit controls - movement with the mouse
* Default scene set-up:
    * Ground plane 
    * Two shadowed lights 
    * Slow model rotation 
* Drag and drop of models 
* Automatic phong material 
* UI controls for changing various settings 
* Frame rate and memory statistics 
* WebGL detector 

## Using the Model Viewer 

Virtually the simplest usage of the Ara viewer is the following example: 

```
    <html>
    <head>
        <title>Simple Ara Viewer Example</title>
    </head>
    <script src="araviewer.js"></script>
    <script>
        ara.view({ url: 'testmodel.ply' });
    </script>
    <body>
    </body>
    </html>
```

## How it works 

The viewer code is launched using a single function called `ara.view` that accepts a JavaScript object that contains minimally the URL for the model to load, and a number of options for controlling the behavior and appearance of the viewer.

### Options

```    
{
    showGui: false,
    camera: {
        near: 0.1,
        far: 15000,
        fov: 50,
        zoom: 1,
        rotate: 1.0,
        position: { x: 0, y: 5, z: -5 },
        target: { x: 0, y: -1, z: 0, },
    },
    background: {
        color: { r: 0x72, g: 0x64, b: 0x5b, }
    },
    plane: {
        show: true, 
        material: {
            color: { r: 0x99, g: 0x99, b: 0x99, },
            specular: { r: 0x10, g: 0x10, b: 0x10, }
        },
        position: {
            x:0, y :0, z:0
        }
    },
    sunlight: { 
        skyColor: { r: 0x44, g: 0x33, b: 0x33 },
        groundColor: { r: 0x11, g: 0x11, b: 0x22 },
        intensity: 1,
    },
    light1: {
        // TODO: the positions of the lights are all wrong. 
        position: { x: 1, y: 1, z: 1 }, 
        color: { r: 0xFF, g: 0xFF, b: 0xFF },
        intensity: 1.35,
    },
    light2: {
        position: { x: 0.5, y: 1, z: -1 }, 
        color: { r: 0xFF, g: 0xAA, b: 0x00 },
        intensity: 1,
    },
    object: {
        scale: 0.01,
        position: { x: 0, y: 0, z: 0 },
        rotation: { x: 0, y: 0, z: 0 },
        material: {
            color: { r: 0x00, g: 0x55, b: 0xFF },
            emissive: { r: 0x00, g: 0x00, b: 0x00 },
            specular: { r: 0x11, g: 0x11, b: 0x11 },
            flatShading: true,
            shininess: 30,
            wireframe: false,
        }
    }            
}
```

## Supported File Formats 

* .obj
* .ply
* .stl 
* .g3d
* .dae 
* .3ds
* .pdb
* .pcb
* .gcode
* .gltf 
* .fbx

## Build Process

Call `npm run build`. This will call a gulp script (`gulpfile.js`) that minifies and concatenates the sources. 

The main viewer code is writtein in TypeScript, and has to be built separately before running gulp.

## Testing Process 

Testing is done using Mocha and can be executed by `npm test`:
https://threejs.org/docs/#manual/en/buildTools/Testing-with-NPM

## Running the Examples Localy

Using `npm run serve` from the main directory will launch a web server that allows you to view the different examples locally. For example:

[`localhost:8080/examples/example1.html`](localhost:8080/examples/example1.html)

## The Sources and Dependencies

The distributable file `ara-viewer.js` is a concatenation of: 

* [Three.JS](https://threejs.org)
    * The main Three.JS distributable
    * WebGL statistics utility
    * WebGL detector utility
    * Several file loaders for Three.JS from the `examples/loaders` folder
    * Three.JS Orbit controls from the `examples/controls` folder    
* [Dat.GUI](https://github.com/dataarts/dat.gui) 
* The `ara-viewer-main.js` source file which encapsulates common Three JS boiler plate 

## Options

The Ara viewer can be fully customized by passing a JSON object, describing the 3D scene.

```
    {
    dom: document.getElement().body,
    models: [
        { 
            url: 'myfiles.stl',
            transform: {
            },
        },        
        {
            primitive: plane, 
            width: 40,
            height: 40,
            material: {
                color: 0x999999, 
                specular: 0x101010,
            },
            transform: {
                rotation: {
                    x: -Math.PI/2,
                },
                position: {
                    y: -0.5
                }
            },
        },
    ],
    lights: [
        {             
            type: hemisphere,
            skyColor: 0x443333, 
            groundColor: 0x111122,
            intensity: 1,
        },
        {
            type: shadowedLight,
            position: { x: },
            color: 
            intensity: 
        }
        
    ]
    camera: {
        target: { y: -0.1 },
        position: { x: 3, y: 0.15, z: 3 },
        fov: 35,
        near: 1,
        far: 15, 
    },
    background: {
        color: 0x72645b,
    },
    fog: {
        color: 0x72645b
        near: 2,
        far: 15, 
    },
    stats: true,
    controls: true, 
}
```