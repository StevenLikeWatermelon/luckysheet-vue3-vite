# Stevenysheet + Vue 3 + Vite

  [![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/hjwforever/stevenysheet-vue3-vite)

English | [简体中文](./README-zh.md)

## Introduction
This is a simple project that shows the use of [Stevenysheet](https://github.com/mengshukeji/Stevenysheet/) and [Stevenyexcel](https://github.com/mengshukeji/Stevenyexcel) in [Vue3](https://vuejs.org/) project with [Vite](https://vitejs.dev/).

## Live Demo
> Tips： There may be some problems with exporting files in the demo website, but running the project locally can export files normally
  1. [Live Demo](https://stevenysheet.vercel.app/)
  2. [![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/hjwforever/stevenysheet-vue3-vite)

## Note
  1. In addition to the need to install the dependencies of [stevenyexcel](https://www.npmjs.com/package/stevenyexcel), you also need to introduce the style files and js files of `StevenySheet`.
   - import `StevenySheet` globally: Import related files directly from the cdn source in [index.html](./index.html).
   - For more importing solutions, please refer to the [official documentation](https://mengshukeji.github.io/StevenysheetDocs/guide/#steps-for-usage).
  2. The core code is in [src/components/StevenySheet.vue](./src/components/StevenySheet.vue)

## Development
  You can choose one of three package managers: `npm`, `yarn`, `pnpm`.

<details>
  <summary><code>npm</code></summary>

  <h5>Installation</h5>
  <pre><code>
  npm install
  </code></pre>
  <h5>Run</h5>
  <pre><code>
  npm run dev
  </code></pre>
  <h5>Build</h5>
  <pre><code>
  npm run build
  </code></pre>
</details>

<details>
  <summary><code>yarn</code></summary>

  <h5>Installation</h5>
  <pre><code>
  yarn install
  </code></pre>
  <h5>Run</h5>
  <pre><code>
  yarn run dev
  </code></pre>
  <h5>Build</h5>
  <pre><code>
  yarn run build
  </code></pre>
</details>

<details>
  <summary><code>pnpm</code></summary>

  <h5>Installation</h5>
  <pre><code>
  pnpm install
  </code></pre>
  <h5>Run</h5>
  <pre><code>
  pnpm run dev
  </code></pre>
  <h5>Build</h5>
  <pre><code>
  pnpm run build
  </code></pre>
</details>

## Resources
- [Stevenysheet](https://github.com/mengshukeji/Stevenysheet)
- [Stevenyexcel](https://github.com/mengshukeji/Stevenyexcel)
- [Vue3](https://vuejs.org/)
- [Vite](https://vitejs.dev/)

## License
[MIT](http://opensource.org/licenses/MIT)
