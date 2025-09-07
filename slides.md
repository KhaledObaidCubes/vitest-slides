---
# You can also start simply with 'default'
theme: Default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Vite test lap
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# open graph
seoMeta:
  # By default, Slidev will use ./og-image.png if it exists,
  # or generate one from the first slide if not found.
  ogImage: auto
  # ogImage: https://cover.sli.dev
---

# Vitest for Vue

Faster, Simpler, Smarter Testing

<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
  Ready, Set, Test! <carbon:arrow-right />
</div>

<div class="abs-br m-6 text-xl">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="slidev-icon-btn">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---

# What is Vitest?

- A unit testing framework built on top of Vite.
- Designed for speed, modern tooling, and seamless DX.
- Think of it as Jest-compatible but faster.

Read more about [Why Vitest?](https://vitest.dev/guide/why.html)

# Key Features:

- Blazing fast – powered by Vite’s esbuild for instant startup.
- Jest-compatible API – describe, it/test, expect.
- TypeScript-first – great TS support out of the box.
- Built-in ESM support – no hacks for imports.
- Vue/React/Svelte-friendly – integrates with framework plugins easily.
- Snapshot testing & coverage supported.

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/features/slide-scope-style
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

<!--
Here is another comment.
-->

---

# Why use Vitest (instead of Jest/Mocha)?

- Speed: Cold start + re-runs are much faster (thanks to Vite).
- Ecosystem Fit: If you’re using Vite for your Vue/React project, Vitest integrates natively.
- Modern Stack: TS, ES modules, and modern imports just work.
- Minimal Config: Works out of the box with Vite plugins (e.g., @vitejs/plugin-vue).
- Better DX: Watch mode is fast, error messages are cleaner, and supports IDE integration.

---

# Quick Comparison: Jest vs Vitest

| Feature            | Jest                | Vitest                        |
| ------------------ | ------------------- | ----------------------------- |
| Speed              | Slower              | Faster                        |
| TypeScript support | Needs Babel/ts-jest | Native                        |
| ESM support        | Limited             | Native                        |
| Vue integration    | Extra setup         | Works with @vitejs/plugin-vue |
| Config complexity  | Heavy               | Light                         |

<br>
<br>

_“So in short: Vitest is basically Jest, but built for the Vite era — faster, simpler, and modern. If you’re already using Vite, Vitest is the natural choice.”_

---

## Installation

Since you’re already using Vite + Vue 3, installing Vitest is straightforward:

```bash
# Install Vitest + Vue Testing Utils + Vue plugin
npm install -D vitest @vue/test-utils @vitejs/plugin-vue

```

_(or yarn add -D ... / pnpm add -D ... depending on your package manager)_

---

## Configuration

Vitest uses your existing Vite config, so you don’t need a separate big setup like Jest.
Just add a test section inside vite.config.ts:

```js
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";

export default defineConfig({
  plugins: [vue()],
  test: {
    globals: true, // use Jest-like globals (describe, it, expect)
    environment: "jsdom", // simulate browser environment for Vue components
    coverage: {
      provider: "v8", // built-in coverage with v8
      reporter: ["text", "json", "html"],
    },
  },
});
```

---
