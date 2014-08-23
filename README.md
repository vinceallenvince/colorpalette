![Build status](https://travis-ci.org/vinceallenvince/colorpalette.svg?branch=master)

# colorpalette

Randomly select color styles from a range of presets.

I created this module after taking a [Marius Watz](http://mariuswatz.com) Processing workshop. He described a method to create a set of color palettes by creating a pool of colors and randomly selecting from it. This module is my interpretation. I've used it in several projects including [FloraJS](https://github.com/vinceallenvince/FloraJS).

##Install

To include colorpalette as a component in your project, use the node module.

```
npm install colorpalette --save
```

You can also use the [standalone version](https://github.com/vinceallenvince/colorpalette/releases/latest) and reference the js file from your document.

```
<html>
  <head>
    <script src="scripts/colorpalette.min.js" type="text/javascript" charset="utf-8"></script>
  </head>
  ...
```

##Usage

The module exports a colorpalette class. In a nodejs project, you access it via:

```
var ColorPalette = require('colorpalette');
var palette = new ColorPalette();
```

Add colors to your palette via addColor(). Pass the min/max amounts plus the start and end colors. The function adds a random number of colors between your min and max. It also selects a random color space between your start/end colors.

In the example below, you are twice as likely to get a dark red color from the palette. Notice you can also chain your addColor() calls.

```
pal.addColor({
  min: 2,
  max: 8,
  startColor: [255, 0, 0],
  endColor: [200, 0, 0]
}).addColor({
  min: 4,
  max: 16,
  startColor: [30, 0, 0],
  endColor: [60, 0, 0]
});
```

To retrieve a color array from the palette, use getColor().

```
var color = pal.getColor(); // returns an array; ex: [255, 100, 0]
```

In the browser, the module exposes a ColorPalette class.

```
<html>
  <head>
    <script src="scripts/colorpalette.min.js" type="text/javascript" charset="utf-8"></script>
  </head>
  <body>
    <script>
      var pal = new ColorPalette();
      pal.addColor({
        min: 2,
        max: 8,
        startColor: [105, 210, 231],
        endColor: [85, 190, 211]
      }).addColor({
        min: 2,
        max: 8,
        startColor: [167, 219, 216],
        endColor: [147, 199, 196]
      });
      for (var i = 0; i < 150; i++) {
        var color = pal.getColor();
        var obj = document.createElement('div');
        obj.style.cssText = 'width: 100px; height: 100px; display: inline-block';
        obj.style.backgroundColor = 'rgb(' + color[0] + ', ' + color[1] + ', ' + color[2] + ')';
        document.body.appendChild(obj);
      }
    </script>
  </body>
</html>
```

To learn how to use the various colorpalette functions, please review [the docs](http://vinceallenvince.github.io/colorpalette/doc/) or check out the [examples](http://vinceallenvince.github.io/colorpalette/).

##Building this project

This project uses [Grunt](http://gruntjs.com). To build the project first install the node modules.

```
npm install
```

Next, run grunt.

```
grunt
```

To run the tests, run 'npm test'.

```
npm test
```

To check test coverage run 'grunt coverage'.

```
grunt coverage
```

A pre-commit hook is defined in /pre-commit that runs jshint. To use the hook, run the following:

```
ln -s ../../pre-commit .git/hooks/pre-commit
```

A post-commit hook is defined in /post-commit that runs the Plato complexity analysis tools. To use the hook, run the following:

```
ln -s ../../post-commit .git/hooks/post-commit
```

View the [code complexity](http://vinceallenvince.github.io/colorpalette/reports/) report.
