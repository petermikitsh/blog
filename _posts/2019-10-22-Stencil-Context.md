---
layout: post
title: "Announcing stencil-context"
author: pete
categories: [ stencil, web components ]
tags: []
image: assets/images/2019_10_22_stencil_context.png
description: "stencil-context provides a React-like Context API for Stencil."
featured: true
hidden: false
comments: false
---

`stencil-context` is a new option for Stencil.js users looking to apply more advanced use cases of context in their projects.

**Project link: [https://github.com/petermikitsh/stencil-context](https://github.com/petermikitsh/stencil-context)**

Today, most Stencil.js users looking to tunnel state deep into the component tree might use [@stencil/state-tunnel](https://github.com/ionic-team/stencil-state-tunnel) today.

As discussed in [#8](https://github.com/ionic-team/stencil-state-tunnel/issues/8), there is community interest in being able to override context at deeper points in the component tree. `stencil-context` supports this use case.

In addition to supporting these more advanced use cases, I've revisited the API to make it more React-like, and simpler to use.

```jsx
import { Component, h } from '@stencil/core';
import { createContext } from 'stencil-context';

const defaultValue = {foo: 'bar'};
const { Provider, Consumer } = createContext(defaultValue);

@Component({
  tag: 'my-app',
})
export class MyApp {
  render() {
    return (
      <Provider>
        <Consumer>
          {({ foo }) => (
            <div>{foo}</div>
          )}
        </Consumer>
      </Provider>
    )
  }
}
```

Here's a more complex use case, with nested `Provider` and `Consumer`:

```jsx
import { Component, h } from '@stencil/core';
import { createContext } from 'stencil-context';

const defaultValue = {foo: 'foo'};
const { Provider, Consumer } = createContext(defaultValue);

@Component({
  tag: 'my-app',
})
export class MyApp {
  render() {
    return (
      <Provider value={ {foo: 'foo1'} }>
        <Consumer>
          {({ foo }) => (
            [
              <div>{foo}</div>,
              <Provider value={ {foo: 'foo2'} }>
                <Consumer>
                  {({ foo: foo2 }) => (
                    <div>{foo2}</div>
                  )}
                </Consumer>
              </Provider>
            ]
          )}
        </Consumer>
      </Provider>
    )
  }
}
```
Check it out at [https://github.com/petermikitsh/stencil-context](https://github.com/petermikitsh/stencil-context).
