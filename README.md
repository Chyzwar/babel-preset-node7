# Babel 6.x presets for Node 7.x (updated regularly!)

Node 7.x brings ~99% [native ES6/ES2015 coverage](http://node.green/).

This preset for Babel 6 attempts to bridge the gap for the remaining 1%.

## Motivation

Babel 6.x is awesome, but simply including the [ES2015 preset](https://www.npmjs.com/package/babel-preset-es2015) means you're transpiling features
that your Node 5.x installation can already do faster and natively, replacing them with inferior / old code.

This preset complements existing V8-native functionality - it doesn't work _around_ it.

The end result is nearly always a faster build and script execution time.

## Key features:
* Removes trailing commas from function calls (via [babel-plugin-syntax-trailing-function-commas](https://www.npmjs.com/package/babel-plugin-syntax-trailing-function-commas))
* CommonJS import/export module syntax ([babel-plugin-transform-es2015-modules-commonjs](https://www.npmjs.com/package/babel-plugin-transform-es2015-modules-commonjs))
* ES7 class properties ([babel-plugin-transform-class-properties](https://www.npmjs.com/package/babel-plugin-transform-class-properties))
* Object rest spread ([babel-plugin-transform-object-rest-spread](https://www.npmjs.com/package/babel-plugin-transform-object-rest-spread))
* Async/await **syntax**. Note: This is *syntax recognition only*. It prevents babel from complaining when it encounters unfamiliar 'async' or 'await' keywords in your code. This does **not** transpile async/await into working functions. Instead, use the `--harmony-async-await` flag on Node start-up.

## Usage instructions

## Installation

Install via NPM the usual way:

`npm i babel-preset-node7`

## Usage

### Via `.babelrc` (recommended)

Create a `.babelrc` file in your project root, and include 'node7' in your preset path:

```js
{
  "presets": [
    "node7"
  ]
}
```

Now whenever you run `babel-node`, it will polyfill your app with the ES2015 features that Node is missing.

### Via CLI
`$ babel script.js --presets node7`

### Via Node API

If you don't want to use a project-wide `.babelrc` file (as above):

```js
require("babel-core").transform("code", {
  presets: ["node7"]
});
```

And if you _do_, and you want to use vanilla `node` instead of `babel-node` as your CLI, you can create an entry script that references your pre-transpiled code like so:

```js
require('babel-register');
require('path/to/es6/script');
```

... which will then run everywhere Node can.

Of course, make sure to `npm i -S babel-core` or `npm i -S babel-register` respectively, to grab the NPM packages you'll need to transpile on-the-fly.

### Webpack, Gulp, Browserify, etc

Follow vendor instructions and include `node7` in your babel "preset" list.

## How to add React support

Babel has a ready-made preset for React, and you now need to install it separately.

Just grab it via NPM:

`npm i babel-preset-react`

And then add it to your "presets" list in `.babelrc`:

```js
{
  "presets": [
    "node7",
    "react"
  ]
}
```

## How to use async/await

This preset does *not* ship with async/await transforms, because Node 7.x now supports them natively.

Simply pass the `--harmony-async-await` flag to Node on start-up.
