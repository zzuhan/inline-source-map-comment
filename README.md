# inline-source-map-comment

[![Build Status](https://travis-ci.org/shinnn/inline-source-map-comment.svg?branch=master)](https://travis-ci.org/shinnn/inline-source-map-comment)
[![Build status](https://ci.appveyor.com/api/projects/status/57fmdhy41qainu8g)](https://ci.appveyor.com/project/ShinnosukeWatanabe/inline-source-map-comment)
[![Coverage Status](https://img.shields.io/coveralls/shinnn/inline-source-map-comment.svg)](https://coveralls.io/r/shinnn/inline-source-map-comment)
[![devDependency Status](https://david-dm.org/shinnn/inline-source-map-comment/dev-status.svg)](https://david-dm.org/shinnn/inline-source-map-comment#info=devDependencies)

Create an inline source map comment from a source map object or string

```javascript
var inlineSourceMapComment = require('inline-source-map-comment');

var fixture = {
  version:3,
  file: 'output.js.map',
  sources: ['input.js'],
  names: [],
  mappings: 'AAAA'
};

inlineSourceMapComment(fixture); //=> "//# sourceMappingURL=data:application/json;base64,eyJ2ZXJzaW9uIjozLCJmaWxlIjoib3V0cHV0LmpzLm1hcCIsInNvdXJjZXMiOlsiaW5wdXQuanMiXSwibmFtZXMiOltdLCJtYXBwaW5ncyI6IkFBQUEifQ=="
```

## Installation

### Package managers

#### [npm](https://www.npmjs.org/) [![NPM version](https://badge.fury.io/js/inline-source-map-comment.svg)](https://www.npmjs.org/package/inline-source-map-comment)

```
npm install inline-source-map-comment
```

#### [bower](http://bower.io/) [![Bower version](https://badge.fury.io/bo/inline-source-map-comment.svg)](https://github.com/shinnn/inline-source-map-comment/releases)

```
bower install inline-source-map-comment
```

#### [Duo](http://duojs.org/)

```javascript
var inlineSourceMapComment = require('shinnn/inline-source-map-comment');
```

### Standalone

[Download the script file directly.](https://raw.githubusercontent.com/shinnn/inline-source-map-comment/master/inline-source-map-comment.js)

## API

### inlineSourceMapComment.js(*sourceMap*)

alias: `inlineSourceMapComment`

*sourceMap*: `String` or `Object`  
Return: `String`

It returns a line comment of base64-encoded source map.

Argument can be an object of source map or a JSON string.

```javascript
var map = '{"version":3,"file":"foo.js.map","sources":["bar.js"],"names":[],"mappings":"AAAA"}';

inlineSourceMapComment.js(map); //=> "//# sourceMappingURL=data:application/json;base64,eyJ2ZXJzaW9uIjozLCJmaWxlIjoiZm9vLmpzLm1hcCIsInNvdXJjZXMiOlsiYmFyLmpzIl0sIm5hbWVzIjpbXSwibWFwcGluZ3MiOiJBQUFBIn0="

inlineSourceMapComment.js(JSON.parse(map)); //=> (Same as `inlineSourceMapComment.js(map)`)

// Just an alias
inlineSourceMapComment(map); //=> (Same as `inlineSourceMapComment.js(map)`)
```

### inlineSourceMapComment.css(*sourceMap*)

It is almost the same as `inlineSourceMapComment.js`, but it returns a block comment instead of line comment. Therefore, it can be used for creating an inline source map of CSS.

```javascript
var map = '{"version":3,"file":"foo.css.map","sources":["bar.js"], ...';

inlineSourceMapComment.css(map) //=> "/* sourceMappingURL=data:application/json;base64,eyJ2ZXJ ... */"
```

## CLI

You can use this module as a CLI tool by installing it [globally](https://www.npmjs.org/doc/files/npm-folders.html#global-installation).

```
npm install -g inline-source-map-comment
```

### Usage

```
inline-source-map-comment v1.0.0
Create an inline source map comment from a source map

Usage1: inline-source-map-comment <source map string>
Usage2: inline-source-map-comment --in <source map file>
Usage3: cat <source map file> | inline-source-map-comment

Options:
--css, --block, -c, -b  Print a block comment for CSS, instead of line comment
--in, --input,  -i      Use a JSON file as a source
--help,         -h      Print usage information
--version,      -v      Print version
```

## License

Copyright (c) 2014 [Shinnosuke Watanabe](https://github.com/shinnn)

Licensed under [the MIT License](./LICENSE).
