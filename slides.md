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
# favicon, can be a local file path or URL
favicon: "/assets/cubesplatform.ico"
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
  Set, Test, Ready! <carbon:arrow-right />
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
transition: fade-out
level: 2
---

# Why use Vitest (instead of Jest/Mocha)?

- Speed: Cold start + re-runs are much faster (thanks to Vite).
- Ecosystem Fit: If you’re using Vite for your Vue/React project, Vitest integrates natively.
- Modern Stack: TS, ES modules, and modern imports just work.
- Minimal Config: Works out of the box with Vite plugins (e.g., @vitejs/plugin-vue).
- Better DX: Watch mode is fast, error messages are cleaner, and supports IDE integration.

---
transition: fade-out
level: 2
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
transition: slide-up
level: 2
---

## Installation

Since you’re already using Vite + Vue 3, installing Vitest is straightforward:

```bash
# Install Vitest + Vue Testing Utils + Vue plugin
npm install -D vitest @vue/test-utils @vitejs/plugin-vue

```

<v-click>
<i>(or yarn add -D ... / pnpm add -D ... depending on your package manager)</i>
</v-click>

---
transition: slide-up
level: 2
---

## Configuration

Vitest uses your existing Vite config, so you don’t need a separate big setup like Jest.
Just add a test section inside `vite.config.ts`:

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
transition: slide-up
level: 2
---

## Configuration

**Create a separate `vitest.config,ts` file instead of doing vitest configuration on to of vitest config file**

```ts
import { defineConfig } from "vitest/config";
import vue from "@vitejs/plugin-vue";
import dts from "vite-plugin-dts";
import path from "path";
export default defineConfig({
  plugins: [vue(), dts({ include: "src" })],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
      "@app": path.resolve(__dirname, "./src/app")
    },
  },
  test: {
    coverage: {
      reporter: ["text", "html"],
      enabled: true,
    },
    globals: true,
    environment: "jsdom",
    include: ["src/**/*.{coca,test,spec}.ts"],
    css: true,
  },
});
```

---
transition: slide-up
level: 2
---

## Configuration

  1- Test: Coverage 
```ts
coverage: {
  reporter: ["text", "html"],
  enabled: true,
}
```


- reporter → Defines output formats:
   - "text" → shows coverage summary in the terminal
   - "html" → generates a detailed HTML report (coverage/index.html)

- enabled: true → Activates code coverage collection


---
transition: slide-up
level: 2
---

## Configuration
 2- Globals

```ts
globals: true
```
 Type: boolean

 Default: false

 CLI: 

````md magic-move {lines: true}
```ts
npx vitest --globals=false
```

```ts
//package.json
{
  "scripts": {
    "test:globals": "vitest --globals"
  }
}
```



Non-code blocks are ignored.

````
<v-click>
Run

```bash
npm run test test:globals
```
</v-click>



<!--
configuration section
-->

---

# configuration Summary

| Aspect                 | In vite.config.ts | Separate vitest.config.ts |
| ---------------------- | ----------------- | ------------------------- |
| Simplicity             | Easy              | Slightly more setup       |
| Separation of concerns | Mixed             | Clean                     |
| Reusability            | Hard              | Easy                      |
| CI/CD friendly         | Needs vite config | Works independently       |
| Plugin duplication     | None              | Might repeat plugins      |

---

# Running Tests

```json {all|3|all}
{
  "scripts": {
    "test": "vitest",
    "test:ui": "vitest --ui"
  }
}
```

<br><br>
<v-click><h1>Then you can Run</h1>

```bash
npm run test
```

and this will run any test file with the formats: `*.spec.ts` and/or `*.tet.ts`

</v-click>

---

# Required Applications to Run

**To follow along and practice the tests, clone and run two repositories of the following applications:**

| Application   | Purpose                                                                                | Repo                                                                     |     |
| ------------- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ | --- |
| vite-test-lab | Your Person CRUD Vue application – the main app for testing.                           | <v-click>https://github.com/KhaledObaidCubes/vite-test-lab.git</v-click> |
| json-server   | Generates mock API data for vite-test-lab.Needed to fetch and manipulate persons data. | <v-click>https://github.com/KhaledObaidCubes/json-server.git </v-click>  |

<br><br>
<v-click>Note: json-server must run first so vite-test-lab can fetch data from its API. Otherwise, you can mock the API responses in tests.</v-click>

---
transition: slide-up
level: 2
---

# Dependencies diagram:

<v-click>
json-server (mock API)<br></v-click>
<v-click>
       │<br>
       ▼<br>
</v-click>
<v-click>
vite-test-lab (Vue app fetching data)<br></v-click>
<v-click>
       │<br>
       ▼<br>
</v-click>
<v-click>
Vitest tests run here
</v-click>

---
transition: slide-up
level: 2
---

<h1>Example: Testing <i><strong color="#00a67d">"getFullName()"</strong></i> Method</h1>

```ts {1|1-3|4-11|12-17|all}
import ListController from "../app/domain/classes/list-controller";

const listController = new ListController();

describe("getFullName", () => {
  it("returns the correct full name", () => {
    const person = { firstName: "Khaled", lastName: "Qad" };
    expect(listController.getFullName(person.firstName, person.lastName)).toBe(
      "Khaled Qad"
    );
  });
  test("instance the method it self", () => {
    const pool = new ListController();
    const newFunc = pool.getFullName;
    expect(newFunc("Khaled", "Obaid")).toBe("Khaled Obaid");
  });
});
```

---
transition: slide-up
level: 2
---

# Test case

````md magic-move {lines: true}
```ts {*|5|*}
import ListController from "../app/domain/classes/list-controller";

const listController = new ListController();
describe("getFullName", () => {
  it("returns the correct full name", () => {
    const person = { firstName: "Khaled", lastName: "Qad" };
    expect(listController.getFullName(person.firstName, person.lastName)).toBe(
      "Khaled Qad"
    );
  });
});
```

```ts {*|1-2|3-4|3-4,8}
import ListController from "../app/domain/classes/list-controller";

const listController = new ListController();
describe("getFullName", () => {
  test("instance the method it self", () => {
      const pool = new ListController();
      const newFunc = pool.getFullName;
      expect(newFunc("Khaled", "Obaid")).toBe("Khaled Obaid");
    });
  });
```



Non-code blocks are ignored.

````
