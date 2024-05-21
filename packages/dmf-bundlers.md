Sure! Below is the documentation for the `bundler` package of your `Dream.mf` framework in Markdown format.

---

# Dream.mf Bundler Package Documentation

The `bundler` package contains a base configuration of Webpack or Rspack which will help you get your microfrontend off the ground. All configurations are extendable using spread operators and you are free to override any of the defaults provided. Out of the box, it offers basic static React functionality with `react-oidc-context`, `react-router`, `react-query`, and CSS/SASS/CSS-Modules support. It also uses `esbuild` as the default loader with JSX and TSX support.

You can use either Rspack or Webpack, with planned support for Vite in the future.

## Table of Contents

- [Installation](#installation)
- [Initialization](#initialization)
- [API](#api)
  - [withBaseWebpack](#withbasewebpack)
  - [withBaseRSPack](#withbaserpack)
- [Types](#types)

## Installation

To install the `bundler` package, use the following command:

```bash
npm install @dream.mf/bundlers
```

## Initialization

Initialize your project with the default Webpack or Rspack configuration by using the respective methods.

### With Webpack

To use Webpack, create a `webpack.config.js` file in the root of your project:

```javascript
const { withBaseWebpack } = require("@dream.mf/bundlers");

module.exports = withBaseWebpack({
    devServer: { port: 3000 },
    federationConfig: { name: 'container' },
}, true);
```

### With Rspack

To use Rspack, create a `rspack.config.js` file in the root of your project:

```javascript
const { withBaseRSPack } = require("@dream.mf/bundlers");

const config = withBaseRSPack({
    devServer: { port: 3000 },
    federationConfig: { name: 'container' },
}, true);

module.exports = config;
```

## API

### `withBaseWebpack`

#### Description

The `withBaseWebpack` function provides a base Webpack configuration.

#### Usage

For a host application with Webpack:

```javascript
const { withBaseWebpack } = require("@dream.mf/bundlers");

module.exports = withBaseWebpack({
    devServer: { port: 3000 },
    federationConfig: { name: 'container' },
}, true);
```

For a remote application with Webpack:

```javascript
const { withBaseWebpack } = require("@dream.mf/bundlers");

const config = withBaseWebpack({
    devServer: { port: 3001 },
    federationConfig: {
        name: "remote_home",
        exposes: {
            "./Application": "./src/_app",
            "./Health": "./src/_health",
        },
    },
}, true);

module.exports = config;
```

### `withBaseRSPack`

#### Description

The `withBaseRSPack` function provides a base Rspack configuration.

#### Usage

For a host application with Rspack:

```javascript
const { withBaseRSPack } = require("@dream.mf/bundlers");

const config = withBaseRSPack({
    devServer: { port: 3000 },
    federationConfig: { name: 'container' },
}, true);

module.exports = config;
```

For a remote application with Rspack:

```javascript
const { withBaseRSPack } = require("@dream.mf/bundlers");

const config = withBaseRSPack({
    devServer: { port: 3001 },
    federationConfig: {
        name: "remote_home",
        exposes: {
            "./Application": "./src/_app",
            "./Health": "./src/_health",
        },
    },
}, true);

module.exports = config;
```

## Types

Currently, this documentation does not cover specific TypeScript types. Please refer to the TypeScript definitions within the source code for detailed type information.

---

This should give you a comprehensive guide on how to use the `bundler` package within your `Dream.mf` framework, covering both Webpack and Rspack configurations for both host and remote applications.