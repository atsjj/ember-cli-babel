# ember-cli-babel [![Build Status](https://travis-ci.org/babel/ember-cli-babel.svg?branch=master)](https://travis-ci.org/babel/ember-cli-babel)

This Ember-CLI plugin uses [Babel](https://babeljs.io/) to allow you to use ES6 syntax with your
Ember-CLI project.

## Installation

```
npm install --save-dev ember-cli-babel
```

## Usage

This plugin should work without any configuration after installing. By default it will take every `.js` file
in your project and run it through the Babel transpiler to convert the ES6 code to ES5. Running existing ES5 code
through the transpiler shouldn't change the code at all (likely just a format change if it does).

If you need to customize the way that Babel transforms your code, you can do it by passing in any of the options
found [here](https://babeljs.io/docs/usage/options/). Example:

```js
// Brocfile.js

var app = new EmberApp({
  babel: {
    // disable comments
    comments: false
  }
});
```

### Polyfill

Babel comes with a polyfill that includes a custom [regenerator runtime](https://github.com/facebook/regenerator/blob/master/runtime.js)
and [core.js](https://github.com/zloirock/core-js). Many transformations will work without it, but for full support you
must include the polyfill in your app. The [Babel feature tour](https://babeljs.io/docs/tour/) includes a note for
features that require the polyfill to work.

To include it in your app, pass `includePolyfill: true` in your `babel` options.

### About Modules

Ember-CLI uses its own ES6 module transpiler for the custom Ember resolver that it uses. Because of that,
this plugin disables Babel module compilation by blacklisting that transform. If you find that you want to use
the Babel module transform instead of the Ember-CLI one, you'll have to explicitly set `compileModules` to `true`
in your configuration. If `compileModules` is anything other than `true`, this plugin will leave the module
syntax compilation up to Ember-CLI.
