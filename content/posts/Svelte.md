+++
title = "svelte"
draft = "true"
+++


### Summary
Svelte is a Javascript framework that functions slightly different to others. It compiles Svelte code into plain Javascript that mainpulates the DOM directly, other frameworks function as libraries that run in the browser.
Svelte applications are built with **components**, self-contained blocks of code that encapsulate HTML, CSS and Javascript.
- It is pretty fast
- Fairy easy
- 



### lol
- A reactive declaration is made by using "$:" instead of "let" this lets the variable update whenever it's value changes
- {#if}{/if} is used to make an if statement and {:else} for else
- forEach is #each items as item
- {#await promise}
- <input bind:value={}>

A typical SvelteKit project looks like this:

```
my-project/
├ src/
│ ├ lib/
│ │ ├ server/
│ │ │ └ [your server-only lib files]
│ │ └ [your lib files]
│ ├ params/
│ │ └ [your param matchers]
│ ├ routes/
│ │ └ [your routes]
│ ├ app.html
│ ├ error.html
│ ├ hooks.client.js
│ ├ hooks.server.js
│ └ service-worker.js
├ static/
│ └ [your static assets]
├ tests/
│ └ [your tests]
├ package.json
├ svelte.config.js
├ tsconfig.json
└ vite.config.js
```
