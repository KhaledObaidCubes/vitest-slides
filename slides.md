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
layout: two-cols
layoutClass: gap-16
---

# Table of contents

This presentation will walk through the essentials of Vitest, starting with an introduction to the framework and its core features. We’ll then cover configuration options, mocking, and testing strategies for real-world projects. Finally, we’ll look at Vitest’s reporting, coverage tools, and practical use cases, wrapping up with best practices and a summary.

::right::

<Toc text-sm columns=2 minDepth="1" maxDepth="2" />

---

# What is Vitest?

- A unit testing framework built on top of Vite.
- Designed for speed, modern tooling, and seamless DX.
- Think of it as Jest-compatible but faster.
<br><br>
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
---

# Why use Vitest (instead of Jest/Mocha)?

- Speed: Cold start + re-runs are much faster (thanks to Vite).
- Ecosystem Fit: If you’re using Vite for your Vue/React project, Vitest integrates natively.
- Modern Stack: TS, ES modules, and modern imports just work.
- Minimal Config: Works out of the box with Vite plugins (e.g., @vitejs/plugin-vue).
- Better DX: Watch mode is fast, error messages are cleaner, and supports IDE integration.

[Read more](https://vitest.dev/guide/why.html)

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

---
transition: fade-out
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
---

# Installation

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
---

# Configuration

---
transition: slide-up
---

## Configuration (vite)

Vitest uses your existing Vite config, so you don’t need a separate big setup like Jest.
Just add a test section inside `vite.config.ts`:

```js
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";

export default defineConfig({
  plugins: [vue()],
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

## Configuration (vitest)

**Create a separate `vitest.config.ts` file instead of doing vitest configuration on to of vitest config file**

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
transition: fade
level: 2
---

## Configuration -  Coverage

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
transition: fade
level: 2
---

## Configuration - Globals

````md magic-move {lines: true}
```json
globals: true
```
```json
test: {
    coverage: {
      reporter: ["text", "html"],
      enabled: true,
    },
    globals: true,
    // other properties ...
    }
```
Non-code blocks are ignored.

````
 Type: boolean & Default: false

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
```bash
npm run test test:globals
```
Non-code blocks are ignored.

````

---
transition: fade
level: 2
---

## Configuration - Environment

````md magic-move {lines: true}
```json
environment: "jsdom",
```
```json
test: {
    coverage: {
      reporter: ["text", "html"],
      enabled: true,
    },
    globals: true,
    environment: "jsdom",
    // other properties ...
    }
```
Non-code blocks are ignored.
````
<span>Default: <span style="color:crimson;font-weight: bold;"> node</span></span><br>
<span>Am using: <span style="color:cyan;font-weight: bold;"> jsdom</span></span><br>

---
transition: fade
level: 2
---

## Configuration - Include

````md magic-move {lines: true}
```json
include: ["src/**/*.{coca,test,spec}.ts"],
```
```json
test: {
    coverage: {
      reporter: ["text", "html"],
      enabled: true,
    },
    globals: true,
    environment: "jsdom",
    include: ["src/**/*.{coca,test,spec}.ts"],
    // other properties ...
    }
```
Non-code blocks are ignored.
````
<span>Type: <span style="color:crimson;font-weight: bold;"> string&lbrack;&nbsp;&rbrack;</span></span><br>
<span>Default: ``` ['**/*.{test,spec}.?(c|m)[jt]s?(x)']```</span><br>
<span>CLI: ```vitest [...include]```, ```vitest **/*.test.js```</span><br>

---
transition: slide-up
level: 2
---

## Configuration - Reporters

````md magic-move {lines: true}
```json
reporters: ['html','verbose'],
```
```json
test: {
    coverage: {
      reporter: ["text", "html"],
      enabled: true,
    },
    globals: true,
    environment: "jsdom",
    include: ["src/**/*.{coca,test,spec}.ts"],
    reporters: ['html','verbose'],
    // other properties ...
    }
```
Non-code blocks are ignored.
````
<span>Type: <span style="color:crimson;font-weight: bold;"> string&lbrack;&nbsp;&rbrack;</span></span><br>
<span>Default: ```default```</span><br>
<span>CLI: ```vitest [...include]```, ```vitest **/*.test.js```</span><br>

---
transition: fade
level: 2
---

## Configuration
 common reporters table:

| Name                    | Description / Behavior                                                                 |
|-------------------------|-----------------------------------------------------------------------------------------|
| `default`               | The standard output: summary + statuses, etc.                                          |
| `basic`                 | Like `default` but without a summary.                                                  |
| `verbose`               | Like `default` + more detail (shows each individual test, slow test warnings, etc.).   |
| `dot`                   | Minimal output: shows a dot for each test, details only for failed ones.               |

---
transition: fade-out
level: 2
---

## Configuration
 common reporters table:
 | Name                    | Description / Behavior                                                                 |
|-------------------------|-----------------------------------------------------------------------------------------|
| `json`                  | Outputs result in JSON format. Good for CI or tools that parse JSON.                   |
| `junit`                 | Outputs in JUnit format (XML); useful for CI integrations.                             |
| `tap`                   | TAP format (Test Anything Protocol).                                                   |
| `tapFlat`               | A flatter version of TAP (less nested / test-module grouping).                         |
| `HangingProcessReporter`| A reporter that helps detect (or report) when test processes hang.                      |
                    



---
transition: slide-up
level: 2
---

# Configuration Summary
<br>
<p style="opacity:1">&nbsp;&nbsp;&nbsp;&nbsp;Vitest uses a configuration file (usually vitest.config.ts or inside vite.config.ts) to customize how tests run. The config lets you define options such as the test environment (node, jsdom, or happy-dom), coverage settings, reporters, plugins, and path aliases. It also supports advanced features like snapshot handling, test timeouts, globals, and transforming CSS or other assets. Since Vitest is built on top of Vite, it reuses much of Vite’s configuration, making it flexible and efficient for both frontend and backend testing needs.</p>

---
transition: fade
level: 2
---

# Running Tests

```json {all|3|all}
{
  "scripts": {
    "test": "vitest", // run normally testing (will be watched by default)
    "test:noWatcher": "vitest run",//this will prevents watcher on testing
    "test:ui": "vitest --ui" //to open the UI on browser
  }
}
```
<br>
<v-click><h1>Then you can Run</h1>

```bash
npm run test //normally run test watcher by default
```
</v-click>
<v-click>
```bash
npm run test  -u//normally run test without watcher
```

</v-click>

<v-click>
```bash
npm run test --ui //open the UI visualization 
```

By default with run test file with the formats: `*.spec.ts` and/or `*.test.ts`

</v-click>

---

# Required Applications to Run

**To follow along and practice the tests, clone and run two repositories of the following applications:**

| Application   | Purpose                                                                                | Repo                                                                     |     |
| ------------- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ | --- |
| vite-test-lab | Your Person CRUD Vue application – the main app for testing.                           | <v-click>https://github.com/KhaledObaidCubes/vite-test-lab.git</v-click> |
| json-server   | Generates mock API data for vite-test-lab needed to fetch and manipulate persons data. | <v-click>https://github.com/KhaledObaidCubes/json-server.git </v-click>  |

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
       <Arrow x1="150" y1="130" x2="150" y2="200" />
</v-click>
<br><br><br>
<v-click>
vite-test-lab (Vue app fetching data)<br></v-click>
<v-click>
       <Arrow x1="150" y1="230" x2="150" y2="300" />
</v-click>
<br><br><br>
<v-click>
Vitest tests run here
</v-click>

---
transition: slide-up
level: 2
---

<h1>Example: Simple method test <i><strong color="#00a67d">"getFullName()"</strong></i></h1>

```ts
import ListController from "../app/domain/classes/list-controller";

const listController = new ListController();

describe("getFullName", () => {
  it("returns the correct full name", () => {
    const person = { firstName: "Khaled", lastName: "Qad" };
    expect(listController.getFullName(person.firstName, person.lastName)).toBe("Khaled Qad");
  });
});
```

---
transition: slide-up
level: 2
---

## Stateless component test

````md magic-move {at:1, lines: false}
```js {*|1-3|5-7|9-13|15-19}
import { mount } from "@vue/test-utils";
import { createRouter, createWebHashHistory } from "vue-router";
import Navigator from "../app/presentation/components/navigator.vue";

// mock pages
const UsersList = { template: "<div>Users List</div>" };
const CreateUser = { template: "<div>Create User</div>" };

//mock routes
const routes = [
  { path: "/", name: "View Users", component: UsersList },
  { path: "/create-user", name: "New User", component: CreateUser },
];

//create mocked router
const router = createRouter({
  history: createWebHashHistory(),
  routes,
});

```

Non-code blocks in between as ignored, you can put some comments.

```js {*}{lines: false} // [!code hl]
describe("Navigator Component test", () => {
  it("renders the first two routes from router", async () => {
    router.push("/"); // set active route
    await router.isReady();

    const wrapper = mount(Navigator, {
      global: {
        plugins: [router],
      },
    });
```
```js {*}{lines: flase}
// Find menu items
    const items = wrapper.findAll(".menu-item");
    expect(items.length).toBe(2); // only first 2 routes

    // Check route names
    expect(items[0].text()).toContain("View Users");
    expect(items[1].text()).toContain("New User");

  });

```
```js {*}{lines:false}
// Find menu items
    const items = wrapper.findAll(".menu-item");
    expect(items.length).toBe(2); // only first 2 routes

    // Check active/none-active classes
    expect(items[0].classes()).toContain("active-item");
    expect(items[1].classes()).toContain("none-active-item");
```
```ts
it("highlights correct menu item when route changes", async () => {
    router.push("/create-user");
    await router.isReady();

    const wrapper = mount(Navigator, {
      global: {
        plugins: [router],
      },
    });

    const items = wrapper.findAll(".menu-item");
    
    expect(items[0].classes()).not.toContain("none-active-item");
    expect(items[1].classes()).not.toContain("active-item");
  });
```
````

---
transition: slide-right
level: 2
---

## Statefull component test


````md magic-move {lines: false}
```ts
import { mount } from "@vue/test-utils";
import CreateUserForm from "@app/presentation/components/create-user-form/create-user-form.vue";

// Mock router
vi.mock("@root/router", () => ({
  default: {
    push: vi.fn(),
  },
}));

```
```ts {*}{lines:false}
// Mock controller
const mockCreateNewPerson = vi.fn();
vi.mock("@app/domain/classes/create-user-controller", () => {
  return {
    default: vi.fn().mockImplementation(() => ({
      user: {
        firstName: "",
        lastName: "",
        age: 0,
        email: "",
        phone: "",
        address: { street: "", city: "", country: "" },
      },
      isBusy: false,
      createNewPerson: mockCreateNewPerson,
    })),
  };
});
```

```ts {*}{lines: false}
describe("CreateUserForm.vue", () => {
  beforeEach(() => {
    mockCreateNewPerson.mockClear();
  });

  it("renders form with title", () => {
    const wrapper = mount(CreateUserForm, {
      props: { formTitle: "Create new USER" },
    });
    //const h1Tag = wrapper.find("#create-user-form-title");
    //expect(h1Tag.text()).toBe("Create new USER");
    expect(wrapper.text()).toContain("Create new USER");
  });
```
```ts {*}{lines: false}
  it("updates form fields via v-model", async () => {
    const wrapper = mount(CreateUserForm, {
      props: { formTitle: "Test Form" },
    });

    const firstNameInput = wrapper.find("#firstName");
    await firstNameInput.setValue("Khaled");

    const lastNameInput = wrapper.find("#lastName");
    await lastNameInput.setValue("Obaid");

    expect((firstNameInput.element as HTMLInputElement).value).toBe("Khaled");
    expect((lastNameInput.element as HTMLInputElement).value).toBe("Obaid");
  });
```
```ts {*}{lines: false}
  it("calls createNewPerson and navigates on submit", async () => {
    const router = (await import("@root/router")).default;

    const wrapper = mount(CreateUserForm, {
      props: { formTitle: "Submit Test" },
    });

    // Fill inputs
    await wrapper.find("#firstName").setValue("Khaled");
    await wrapper.find("#lastName").setValue("Obaid");
    await wrapper.find("#email").setValue("khaled@example.com");
    await wrapper.find("#age").setValue("30");
    await wrapper.find("#phone").setValue("445778663");

    // Click submit
    await wrapper.find("button").trigger("click");
```
```ts {*}{lines: false}
    // Assert controller called
    expect(mockCreateNewPerson).toHaveBeenCalledTimes(1);
    expect(mockCreateNewPerson).toHaveBeenCalledWith(
      expect.objectContaining({
        firstName: "Khaled",
        lastName: "Obaid",
        email: "khaled@example.com",
        age: 30,
        phone: "445778663",
      })
    );

    // Assert navigation
    expect(router.push).toHaveBeenCalledWith("/");
  });
});

```
````

---
transition: slide-right
level: 2
---

---
transition: slide-right
level: 2
---

---
transition: slide-right
level: 2
---
