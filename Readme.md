# Turd Herder
## _The Porcelain Standard for 3D Printer Waste Management_

The Turd Herder is a dookie dispoasl system for 3D printers with toolheads that have limited to no travel past the edges of the print bed.  The bowl extends over the edge of the print bed, receives the "payload" and proceeds to retract and whisk it off to a tank in the depths below.  

Turd Herder was designed for use with the Voron Trident / Box Turtle AMS combo running Klipper firmware. The macros are designed to integrate with the AFC Macros (included with the Box Turtle system).
The motion system was inspired by [Dendrowen's Blobifier], the mounting system incorporates whole, and modified, parts from [Armored Turtle's AT Brush]  and the macros are modified versions of [ImSundee's Turtleblobifier].


## Features

- Can be used with any toolhead / probe combo as there aren't any negative Z moves
- A modified G28 allows for safe Z homing 
- Easy to Print components
- Designed to plug into a BL Touch Port for easy wiring
- Optional brush attachment creates an all-in-one solution

## Required Tools
- Sodering Iron
- Crimping Tool
- Wire Stripper
- Allen Wrenches / Hex Drivers (1.5, 2, 3 and 5 mm)

## BOM

| Part | QTY | 
| ------ | ------ |
| MG90S Servo (180°) | 1 |
| Servo Hardware Kit | 1 |
| D2F-01L Switch (with lever) | 1 |
| Bambu style silicone brush | 1 |
| 6 x 3 mm magnet | 2 |
| 15 x 15 x 1 mm metal square | 1 |
| M5 x 10 mm SHCS | 2 |
| M5 Rollnut | 2 |
| M3 Hex Nut | 2 |
| M3 Washer | 1 |
| M3 x 5 x 4 mm Heat Set Insert | 8 |
| M3 x 5 mm SHCS | 1 |
| M3 x 6 mm SHCS | 1 | 
| M3 x 8 mm SHCS | 2 |
| M3 x 8 mm BHCS | 1 |
| M3 x 6 mm BHCS | 1 |
| M2 x 8 mm SHCS | 2 |
| JST-XH Male / Female Plugs / Crimps | ~ |
| 3 mm ID Bowden Tube (optional) | ~4.5 mm |
| Zip Ties (optional) | ~ |
*Note the M3 Hex Nuts MUST be magnetic.  The sled mechanism will not work properly without a strong-ish magnetic connection.*

In addition to the included STLs in this repositiory, Turd Herder requires the following parts from the [AFC-Accessories] repo.
- [mount_lower.stl]
- [mount_upper.stl]

## Printing

Parts should be printed in ABS and in accordance to typical Voron specs which may be found [here]. Tolerances for the slots are a little tight and may require some filing to achieve a smooth translation from front to rear.
All parts are oriented correctly and don't require any modifications from the slicer.

# Assembly 


Install the dependencies and devDependencies and start the server.

```sh
cd dillinger
npm i
node app
```

For production environments...

```sh
npm install --production
NODE_ENV=production node app
```

## Plugins

Dillinger is currently extended with the following plugins.
Instructions on how to use them in your own application are linked below.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Development

Want to contribute? Great!

Dillinger uses Gulp + Webpack for fast developing.
Make a change in your file and instantaneously see your updates!

Open your favorite Terminal and run these commands.

First Tab:

```sh
node app
```

Second Tab:

```sh
gulp watch
```

(optional) Third:

```sh
karma test
```

#### Building for source

For production release:

```sh
gulp build --prod
```

Generating pre-built zip archives for distribution:

```sh
gulp build dist --prod
```

## Docker

Dillinger is very easy to install and deploy in a Docker container.

By default, the Docker will expose port 8080, so change this within the
Dockerfile if necessary. When ready, simply use the Dockerfile to
build the image.

```sh
cd dillinger
docker build -t <youruser>/dillinger:${package.json.version} .
```

This will create the dillinger image and pull in the necessary dependencies.
Be sure to swap out `${package.json.version}` with the actual
version of Dillinger.

Once done, run the Docker image and map the port to whatever you wish on
your host. In this example, we simply map port 8000 of the host to
port 8080 of the Docker (or whatever port was exposed in the Dockerfile):

```sh
docker run -d -p 8000:8080 --restart=always --cap-add=SYS_ADMIN --name=dillinger <youruser>/dillinger:${package.json.version}
```

> Note: `--capt-add=SYS-ADMIN` is required for PDF rendering.

Verify the deployment by navigating to your server address in
your preferred browser.

```sh
127.0.0.1:8000
```

## License

MIT

**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [Dendrowen's Blobifier]: <https://github.com/Dendrowen/Blobifier>
   [ImSundee's Turtleblobifier]: https://github.com/ImSundee/Turtleblobifier
   [Armored Turtle's AT Brush]: https://github.com/ArmoredTurtle/AFC-Accessories/tree/main/AT_Brush
   [AFC-Accessories]: https://github.com/ArmoredTurtle/AFC-Accessories
   [mount_lower.stl]: https://github.com/ArmoredTurtle/AFC-Accessories/blob/main/AT_Brush/STLs/mount_lower.stl
   [mount_upper.stl]: https://github.com/ArmoredTurtle/AFC-Accessories/blob/main/AT_Brush/STLs/mount_upper.stl
   [here]:<https://docs.vorondesign.com/sourcing.html#print-settings>
   
   
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
