# wakkl
Wakkl is a JavaScript library for multi-sensory three-dimensional photographs. For more background information to the project or to find out how to contribute, please read the Wiki.

## File structure
The file structure inside your `images` directory needs to look as follows.
```
images
├── [your-image].wakkl
└── [your-image]
    ├── 01.jpg
    ├── 02.jpg
    ├── ...
    ├── 29.jpg
    ├── 30.jpg
    ├── sound.mp3
    ├── mask.svg
    └── meta.json
```

As you can see, the image name `[your-image]` is represented on two places. This is at `[your-image].wakkl` which is a two-dimensional preview and at `[your-image]` which is the directory that contains the wakkl image's assets. 
 
Assets are a sequence of three-dimensionally photographed subject and other files such as sound or the photos's meta data (e.g. exif).

`[your-image].wakkl` equals in this case `15.jpg` inside wakkl's assets folder. It is the mid of the sequence (30 images ÷ 2 = image number 15).

### [your-image].wakkl
For better visibility you can replace the original file extension `.jpg` with `.wakkl`. Since the file's internal headers remain in tact the image can still be displayed by the browser and act as a fallback in case the browser cannot execute the `wakkl.js` properly.
 
Make sure that the folder which includes the image's assets has the same name as your wakkl-image but without its file extension.

### meta.json
`meta.json` contains the exif data of any image of the sequence. As you can see, it contains amongst other things information about the camera, the artist and the lens. 
 
But the most important information is the `FOV` (= Field Of View) which is used to map generated element into the scene.
 
Depending on the feature components (see below) you would like to use, you can include dataset attributes to the file as well.
```
{
    "XMP-exif": {

        ...

        "Make": "Canon",
        "Model": "Canon EOS 600D",
        "Artist": "Friedrich Schultheiss",
        "Lens": "11-16mm",
        "ApproximateFocusDistance": 4294967295,
        
        ...

        "FOV": "92.3 deg",
        "FocalLength35efl": "11.0 mm (35 mm equivalent: 17.3 mm)",
        "HyperfocalDistance": "1.27 m",
        "LensID": "Tokina AT-X 116 AF Pro DX 11-16mm f/2.8"
    },

    "WAKKL-dataset": {
        "Count": 30,
        "Phi": -36,
        "Chi": 14,
        "OriginX": "50%",
        "OriginY": "55%",
        "Sound": "sound.mp3"
    }
}
```




## Useage
1. Simply insert your multi-sensory, three-dimensional photograph into your html document the following way.
```html
<img src="images/[your-image].wakkl">
``` 
2. Add the JavaScript file at the end of your html document, before the closing body tag.
```html
<script src="wakkl.min.js"></script>
```
3. Initialize wakkl by calling
```html
<script>
    var options = {}; // your options (instructions below)
    wakkl.init( options );
</script>
```


## Options

- `grid`: (default: `false`) A grid on the xy plane in the scene
- `ui`: (default: `true`) Icons that allow switch between different controllers
- `fullscreen`: (default: `false`) Fullscreen button


## Controllers

### Mouse move

### Mouse drag

### Device orientation

### Touch drag

### Head move



## Feature components

### Image
This component requires the `count` dataset attribute which contains the length of the sequence. It can be set inside `meta.json` (recommended) or as html attribute.

### Sound
This component requires the `sound` dataset attribute which contains the path to a sound file (relative to the image's asset folder). It can be set inside `meta.json` (recommended) or as html attribute.

### Markup
This component requires `phi` and `chi` dataset attribute or the `arc`'s angle value as well as rapping your image between `<wakkl-image>` and `</wakkl-image>`.
```html
<wakkl-image>
    <img src="images/[your-image].wakkl">
    <object><!-- HTML goes here. --></object>
</wakkl-image>
```
Elements wrapped inside the object will be mapped automatically  to the user's interaction. In addition, they can be moved and rotated with attributes `x`. `y`, `z` and `rotation-x`, `rotation-y`and `rotation-z`.

### Vector
This feature is not yet supported but coming soon!
```html
<svg><!-- SVG goes here. --></svg>
```

### Masks
This feature is not yet supported but coming soon!