# ansi-colors-es6 [![NPM version](https://img.shields.io/npm/v/ansi-colors-es6.svg?style=flat)](https://www.npmjs.com/package/ansi-colors-es6) [![NPM monthly downloads](https://img.shields.io/npm/dm/ansi-colors-es6.svg?style=flat)](https://npmjs.org/package/ansi-colors-es6) [![NPM total downloads](https://img.shields.io/npm/dt/ansi-colors-es6.svg?style=flat)](https://npmjs.org/package/ansi-colors-es6) 

> Easily add ANSI colors to your node terminal or browser console. A faster drop-in replacement for chalk, colors, kleur and turbocolor (without the dependencies and rendering bugs). And a lighter ES6 implementation of `ansi-colors` that works everywhere ES6+ works without the need for transpiling, unless you want to.

## Install

Install with [npm](https://www.npmjs.com/):

```sh
$ npm install --save ansi-colors-es6
```

![image](https://user-images.githubusercontent.com/383994/39635445-8a98a3a6-4f8b-11e8-89c1-068c45d4fff8.png)

![node terminal color examples](https://raw.githubusercontent.com/RIAEvangelist/ansi-colors/master/img/vanilla-test-node-report.PNG)

## Why use this?

ansi-colors-es6 is _the fastest Node.js library for terminal and browser console styling_. A more performant drop-in replacement for chalk, colors and ansi-colors with no dependencies.

* _Works in the browser as well as the terminal!_
* _Blazing fast_ - Fastest terminal styling library in node.js, and the browser!
* _No dependencies_ 
* _Safe_ - Does not modify the `String.prototype` like others.
* Supports [nested colors](#nested-colors), **and does not have the [nested styling bug](#nested-styling-bug) that is present in [colorette](https://github.com/jorgebucaran/colorette), [chalk](https://github.com/chalk/chalk), and [kleur](https://github.com/lukeed/kleur)**.
* Supports [chained colors](#chained-colors).
* [Toggle color support](#toggle-color-support) on or off.

#### Chrome 
![chrome terminal color examples](https://raw.githubusercontent.com/RIAEvangelist/ansi-colors/master/img/vanilla-test-chrome-report.PNG)

#### Edge
![edge terminal color examples](https://raw.githubusercontent.com/RIAEvangelist/ansi-colors/master/img/vanilla-test-edge-report.PNG)

## Usage

```js
//use relative paths to allow code sharing with browsers
//this way the same exact files will work in all locations
import ansi from './node_modules/ansi-colors-es6/index.js';

console.log(ansi.red('This is a red string!'));
console.log(ansi.green('This is a red string!'));
console.log(ansi.cyan('This is a cyan string!'));
console.log(ansi.yellow('This is a yellow string!'));
```

![image](https://user-images.githubusercontent.com/383994/39653848-a38e67da-4fc0-11e8-89ae-98c65ebe9dcf.png)

## Chained colors

```js
//use relative paths to allow code sharing with browsers
//this way the same exact files will work in all locations
import ansi from './node_modules/ansi-colors-es6/index.js';

console.log(ansi.bold.red('this is a bold red message'));
console.log(ansi.bold.yellow.italic('this is a bold yellow italicized message'));
console.log(ansi.green.bold.underline('this is a bold green underlined message'));
```

![image](https://user-images.githubusercontent.com/383994/39635780-7617246a-4f8c-11e8-89e9-05216cc54e38.png)

## Nested colors

```js
//use relative paths to allow code sharing with browsers
//this way the same exact files will work in all locations
import ansi from './node_modules/ansi-colors-es6/index.js';

console.log(ansi.yellow(`foo ${ansi.red.bold('red')} bar ${ansi.cyan('cyan')} baz`));
```

![image](https://user-images.githubusercontent.com/383994/39635817-8ed93d44-4f8c-11e8-8afd-8c3ea35f5fbe.png)


## Toggle color support

Easily enable/disable colors.

```js
//use relative paths to allow code sharing with browsers
//this way the same exact files will work in all locations
import ansi from './node_modules/ansi-colors-es6/index.js';

// disable colors manually
ansi.enabled = false;

// or use a library to automatically detect support
ansi.enabled = require('color-support').hasBasic;

console.log(ansi.red('I will only be colored red if the terminal supports colors'));
```

## Strip ANSI codes

Use the `.unstyle` method to strip ANSI codes from a string.

```js
console.log(ansi.unstyle(ansi.blue.bold('foo bar baz')));
//=> 'foo bar baz'
```

## Available styles

**Note** that bright and bright-background colors are not always supported.

| Colors  | Background Colors | Bright Colors | Bright Background Colors |
| ------- | ----------------- | ------------- | ------------------------ |
| black   | bgBlack           | blackBright   | bgBlackBright            |
| red     | bgRed             | redBright     | bgRedBright              |
| green   | bgGreen           | greenBright   | bgGreenBright            |
| yellow  | bgYellow          | yellowBright  | bgYellowBright           |
| blue    | bgBlue            | blueBright    | bgBlueBright             |
| magenta | bgMagenta         | magentaBright | bgMagentaBright          |
| cyan    | bgCyan            | cyanBright    | bgCyanBright             |
| white   | bgWhite           | whiteBright   | bgWhiteBright            |
| gray    |                   |               |                          |
| grey    |                   |               |                          |

_(`gray` is the U.S. spelling, `grey` is more commonly used in the Canada and U.K.)_

### Style modifiers

* dim
* **bold**

* hidden
* _italic_

* underline
* inverse
* ~~strikethrough~~

* reset

## Aliases

Create custom aliases for styles.

```js
//use relative paths to allow code sharing with browsers
//this way the same exact files will work in all locations
import ansi from './node_modules/ansi-colors-es6/index.js';

ansi.alias('primary', ansi.yellow);
ansi.alias('secondary', ansi.bold);

console.log(ansi.primary.secondary('Foo'));
```

## Themes

A theme is an object of custom aliases.

```js
//use relative paths to allow code sharing with browsers
//this way the same exact files will work in all locations
import ansi from './node_modules/ansi-colors-es6/index.js';

ansi.theme({
  danger: ansi.red,
  dark: ansi.dim.gray,
  disabled: ansi.gray,
  em: ansi.italic,
  heading: ansi.bold.underline,
  info: ansi.cyan,
  muted: ansi.dim,
  primary: ansi.blue,
  strong: ansi.bold,
  success: ansi.green,
  underline: ansi.underline,
  warning: ansi.yellow
});

// Now, we can use our custom styles alongside the built-in styles!
console.log(ansi.danger.strong.em('Error!'));
console.log(ansi.warning('Heads up!'));
console.log(ansi.info('Did you know...'));
console.log(ansi.success.bold('It worked!'));
```

### Contributors

| **Commits** | **Contributor** |  
| --- | --- |  
| 48 | [jonschlinkert](https://github.com/jonschlinkert) |  
| 42 | [doowb](https://github.com/doowb) |  
| 8  | [RIAEvangelist](https://github.com/RIAEvangelist) |
| 6  | [lukeed](https://github.com/lukeed) | 
| 2  | [Silic0nS0ldier](https://github.com/Silic0nS0ldier) |  
| 1  | [dwieeb](https://github.com/dwieeb) |  
| 1  | [jorgebucaran](https://github.com/jorgebucaran) |  
| 1  | [madhavarshney](https://github.com/madhavarshney) |  
| 1  | [chapterjason](https://github.com/chapterjason) |  
