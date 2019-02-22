<p align="center">
  <img src="https://i.imgur.com/hHXmkvE.png" width="500" alt="goober" />
</p>

🥜 goober, a less than 1KB css-in-js solution.

[![npm version](https://badge.fury.io/js/goober.svg?bust)](https://badge.fury.io/js/goober)
[![Build Status](https://travis-ci.org/cristianbote/goober.svg?branch=master)](https://travis-ci.org/cristianbote/goober)
[![gzip size](http://img.badgesize.io/https://unpkg.com/goober/dist/goober.js?compression=gzip)](https://unpkg.com/goober)

# Motivation
I always wondered, if you can get a working solution for css-in-js with a smaller footprint. I started a project and wanted a to use styled-components. Looking at their sizes, it seems that I would rather not include ~16kB([styled-components](https://github.com/styled-components/styled-components)) or ~11kB([emotion](https://github.com/emotion-js/emotion)) just so I can use the `styled` paradigm. So, I embarked in a mission to create a smaller alternative for these well established apis.

# Usage
The API is inspired by emotion, `styled` function. Meaning, you call it with your `tagName` and returns a vDOM component for that tag.

```jsx
import { styled } from "goober";

const Icon = styled("i")`
  display: flex;
  flex: 1;
  color: red;
`;

const Button = styled("button")`
  background: dodgerblue;
  color: white;
  border: 0;

  &:focus,
  &:hover {
    padding: 1em;
  }

  .otherClass {
    margin: 0;
  }

  ${Icon} {
    color: black;
  }
`;
```

# Examples
* [Vanilla](https://codesandbox.io/s/jlooovjvv5)
* [React](https://codesandbox.io/s/k0mnp40n7v)
* [Preact](https://codesandbox.io/s/r15wj2qm7o)
* [SSR with Preact](https://codesandbox.io/s/7m9zzl6746)

# SSR
You can get the critical CSS for SSR, via `extractCss`. Take a look at this example: [CodeSandbox: SSR with Preact and goober](https://codesandbox.io/s/7m9zzl6746)

# API
As you can see it supports most of the syntaxes of CSS. If you find any issues, please submit a ticket or even a PR with a fix.

`styled(tagName)`
* `@param {String} tagName` The name of the dom element you'd like the styled to be applied to
* `@returns {Function}` Returns the tag template function.

```js
import { styled } from "goober";

const Btn = styled("button")`
  border-radius: 4px;
`;
```

`css` Same as `styled` but without the tagName and vNode generation. In the end the output will be a className.
* `@returns {Function}` Returns the tag template function.

```js
import { css } from "goober";

const BtnClassName = css`
  border-radius: 4px;
`();
// (!) Note the empty param at the end. If you wanna use `props` throughout the syntax this is the place to put them

const btn = document.querySelector("#btn");
btn.classList.add(BtnClassName);
```

`extractCss()`
* `@returns {String}` Returns the `<style>` tag should be rendered in your document `<head>` and clears the cache.
```js
const { extractCss } = require("goober");

// After your app has rendered, just call it:
const styleTag  = extractCss();
```

# Features
- [x] Basic CSS parsing
- [x] Nested rules with pseudo selectors
- [x] Nested styled components
- [x] Media queries (@media)
- [x] Keyframes (@keyframes)
- [x] Smart(lazy) client-side hydration
- [ ] `globalStyle` so one would be able to create global styles
- [ ] Vendor prefixing
- [ ] Vanilla(via `css` function)

# Contributing
Feel free to try it out and checkout the examples. If you wanna fix something feel free to open a issue or a PR.
