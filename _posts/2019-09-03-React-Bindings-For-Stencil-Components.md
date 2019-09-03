---
layout: post
title:  "Generate React Bindings for Stencil Components"
author: pete
categories: [ stencil, react, web components ]
tags: []
image: assets/images/2019_09_03_stencil_react.png
description: "React doesn't have the best support for web components out-of-the-box. stencil-react changes that."
featured: true
hidden: false
comments: false
---

React doesn't have the best support for web components out-of-the-box. Currently, React 16.9.0 is scored at 71% support, according to <a href="https://custom-elements-everywhere.com/">custom-elements-everywhere.com</a>. With the right tooling, we can raise that to 100%.

Introducing <a href="https://github.com/petermikitsh/stencil-react">stencil-react</a>. It generates React components ("bindings") for Stencil Web Components, including support for:

- custom element properties, 
- custom element events, 
- react synthetic events (e.g., `onClick`),
- `aria-*` attributes, and
- TypeScript typings

All through the standard React interface you're familiar with. Suppose we had a `Button` web component in our Stencil project `@anjuna/core`. Here's the React usage:

```jsx
import { Button } from '@anjuna/core-react';

const App = (
  <Button
    context="primary"
    anjBlur={(customBlurEvent) => { debugger; }}
    onClick={(syntheticReactClickEvent) => { debugger; }}
    aria-label="My ARIA Example"
  >
    Hello World
  </Button>
);
```

To generate your own React bindings, install `stencil-react` and make sure your Stencil v1 component library (e.g, `@anjuna/core`) is installed as an npm dependency.

```
npm i stencil-react
stencil-react @anjuna/core
```

For the full scoop, check out [https://github.com/petermikitsh/stencil-react](https://github.com/petermikitsh/stencil-react).
