# node-imaginary [![Build Status](https://api.travis-ci.org/h2non/node-imaginary.svg?branch=master)][travis] [![Dependency Status](https://gemnasium.com/h2non/node-imaginary.svg)][gemnasium] [![NPM version](https://badge.fury.io/js/imaginary.svg)][npm]

Minimalist node.js/io.js CLI & programmatic stream-based interface for [imaginary](https://github.com/h2non/imaginary) HTTP API

## Installation

For command-line usage, install it as global package:
```bash
npm install -g imaginary
```

For programmatic usage, install it in the tree dependency:
```bash
npm install imaginary --save[-dev]
```

## CLI

```bash
$ imaginary --help
```

```bash
Usage: imaginary [options] [command]

Commands:

  crop [options] [url]           Crop any image to a given square thumbnail in pixels
  width [options] [imageUrl]     Resize any image to a given width in pixels
  height [options] [imageUrl]    Resize the image to the given height in pixels
  resizei [options] [imageUrl]   The image will be resized to fit the given resolution box (but not cropped). White will be added for the padding, if needed

Options:

  -h, --help     output usage information
  -V, --version  output the version number

Examples:

  $ imaginary crop -r 200x200 http://server.net/image.jpg
  $ imaginary width -r 300 http://server.net/image.jpg
  $ imaginary height -r 300 http://server.net/image.jpg
  $ imaginary crop --output test.jpg http://server.net/image.jpg
````

## API

### imaginary(image, [serverUrl])

Constructor of the imaginary client

Reading the image from disk:
```js
var fs = require('fs')
var imaginary = require('imaginary')
var serverUrl = 'http://imaginary.company.net'

imaginary('image.jpg', serverUrl)
  .crop({ widht: 200 })
  .on('error', function (err) {
    console.error('Cannot resize the image:', err)
  })
  .pipe(fs.createWriteStream('out.jpg'))
```

Reading the image from remote:
```js
imaginary('http://server.com/image.jpg')
  .crop({ width: 100 })
  .on('error', function (err) {
    console.error('Cannot resize the image:', err)
  })
  .pipe(fs.createWriteStream('test.jpg'))
```

#### imaginary#crop(params)

Crop any image to a given square thumbnail in pixels. Example: `300x300`

#### imaginary#width(params)

Resize any image to a given width in pixels. Example: `200`

#### imaginary#height(params)

Resize any image to a given height in pixels. Example: `200`

#### imaginary#resizeInBox(params)

The image will be resized to fit the given resolution box (but not cropped). White will be added for the padding, if needed.
Example: `300x200`

### imaginary.VERSION

Get the current module version

## License

[MIT](http://opensource.org/licenses/MIT) © Tomas Aparicio

[travis]: http://travis-ci.org/h2non/node-imaginary
[gemnasium]: https://gemnasium.com/h2non/node-imaginary
[npm]: http://npmjs.org/package/imaginary
