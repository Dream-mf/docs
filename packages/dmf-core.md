# Dream.mf Core Package

The `core` package is a foundational part of the Dream.mf framework. Engineers typically won't use this library directly in their applications, but it is available for those creating plugins for the Dream.mf framework.

This package is responsible for creating the runtime object in the browser called `DreamMF`. This runtime object provides visibility into various details such as the logger and version in use, user profile details, loaded remotes and modules, and much more.

## Table of Contents

- [Installation](#installation)
- [Initialization](#initialization)
- [API](#api)
  - [validateRuntime](#validateruntime)
  - [validateRuntimeProperty](#validateruntimeproperty)
  - [registerRuntimeProperty](#registerruntimeproperty)
  - [registerRuntimePlugin](#registerruntimeplugin)
  - [registerUserProfile](#registeruserprofile)
  - [registerRuntimeRemote](#registerruntimeremote)
- [Types](#types)

## Installation

To install this package, you can use npm or yarn:

```shell
npm install @dream-mf/core
```

or

```shell
yarn add @dream-mf-core
```

## Initialization

To initialize the Dream.mf runtime, call the `init` function. This should be done once, during the startup of your application.

```typescript
import { init } from 'dream-mf-core';

init();
```

This will set up the global `DreamMF` object in the browser.

## API

### `validateRuntime`

Checks if the Dream.mf runtime has been installed and initialized.

```typescript
export const validateRuntime = () => {  
  return window.DreamMF !== undefined;  
};
```

**Sample:**

```typescript
import { validateRuntime } from 'dream-mf-core';

const isRuntimeInitialized = validateRuntime();
console.log(`Runtime initialized: ${isRuntimeInitialized}`);
```

### `validateRuntimeProperty`

Checks if the specified property is already registered in the runtime.

```typescript
export const validateRuntimeProperty = (propertyName: string) => {  
  return window.DreamMF[propertyName] !== undefined;  
};
```

**Sample:**

```typescript
import { validateRuntimeProperty } from 'dream-mf-core';

const hasLogger = validateRuntimeProperty('logger');
console.log(`Logger registered: ${hasLogger}`);
```

### `registerRuntimeProperty`

Registers a property with the Dream.mf runtime.

```typescript
export const registerRuntimeProperty = (propertyName: string, object: object) => {  
  if (!validateRuntimeProperty(propertyName)) {  
    window.DreamMF[propertyName] = object;  
  }  
};
```

**Sample:**

```typescript
import { registerRuntimeProperty } from 'dream-mf-core';

const logger = {
  log: (msg: string) => console.log(`[DreamMF] ${msg}`)
};

registerRuntimeProperty('logger', logger);
```

### `registerRuntimePlugin`

Registers a plugin by name with the supplied configuration.

```typescript
export const registerRuntimePlugin = (pluginName: string, config: object) => {  
  if (!validateRuntimeProperty("plugins")) {  
    window.DreamMF.plugins = new Array<Plugin>();  
  }  
  const exists = window.DreamMF.plugins.some(  
    (item) => item.name === pluginName,  
  );  
  if (!exists) {  
    var record = { name: pluginName, config: config } as Plugin;  
    window.DreamMF.plugins.push(record);  
  }  
};
```

**Sample:**

```typescript
import { registerRuntimePlugin } from 'dream-mf-core';

const pluginConfig = {
  apiUrl: 'https://api.example.com',
  retries: 3
};

registerRuntimePlugin('examplePlugin', pluginConfig);
```

### `registerUserProfile`

Registers the current user details in the runtime for easy lookup.

```typescript
export const registerUserProfile = (userProfile?: any) => {  
  const propName = "profile";  
  if (!validateRuntimeProperty(propName)) {  
    window.DreamMF[propName] = null;  
  }  
  window.DreamMF[propName] = userProfile;  
};
```

**Sample:**

```typescript
import { registerUserProfile } from 'dream-mf-core';

const userProfile = {
  username: 'johndoe',
  email: 'johndoe@example.com'
};

registerUserProfile(userProfile);
```

### `registerRuntimeRemote`

Registers a remote scope and module by URL with the Dream.mf runtime for discovery.

```typescript
export const registerRuntimeRemote = (  
  scope: string,  
  module: string,  
  url: string,  
  loadType?: RemoteLoadType,  
) => {  
  const hasRemotesInit = window.DreamMF["remotes"] !== undefined;  
  if (!hasRemotesInit) {  
    if (!validateRuntimeProperty("remotes")) {  
      window.DreamMF.remotes = new Array<Remotes>();  
    }  
  }  
  const scopeExists = window.DreamMF.remotes.some(  
    (item) => item.scope === scope,  
  );  
  if (!scopeExists) {  
    var record = {  
      scope,  
      modules: module == null ? [] : [module],  
      url,  
      loadType,  
    } as Remotes;  
    window.DreamMF.remotes.push(record);  
  } else {  
    const s = window.DreamMF.remotes.find((sc) => sc.scope === scope);  
    if (module !== null && !s.modules.includes(module)) {  
      s.modules.push(module);  
    }  
  }  
};
```

**Sample:**

```typescript
import { registerRuntimeRemote, RemoteLoadType } from 'dream-mf-core';

registerRuntimeRemote('exampleScope', 'exampleModule', 'https://example.com/module.js', RemoteLoadType.Dynamic);
```

## Types

### `RuntimeName`

The name of the runtime object in the browser.

```typescript
export const RuntimeName = "DreamMF";
```

### `RemoteLoad`

Different load types for remotes.

```typescript
export const RemoteLoad = {  
  Preload: "Preload",  
  Eager: "Eager",  
  Dynamic: "Dynamic",  
};
```

### `RemoteLoadType`

The type definition for remote load.

```typescript
export type RemoteLoadType = (typeof RemoteLoad)[keyof typeof RemoteLoad];
```

### `Remotes`

Interface for remotes.

```typescript
export interface Remotes {  
  url: string;  
  scope: string;  
  modules: string[];  
  loadType?: RemoteLoadType;  
}
```

### `Authentication`

Interface for authentication details.

```typescript
export interface Authentication {  
  provider: string;  
  config?: object;  
}
```

### `Bundler`

Interface for bundler details.

```typescript
export interface Bundler {  
  provider: string;  
  config?: object;  
}
```

### `Logger`

Interface for logger details.

```typescript
export interface Logger {  
  provider: string;  
  config?: object;  
}
```

### `Plugin`

Interface for plugin details.

```typescript
export interface Plugin {  
  name: string;  
  config?: object;  
}
```

### `Metadata`

Interface for any metadata.

```typescript
export interface Metadata {}
```

### `Runtime`

Interface for the Dream.mf runtime object.

```typescript
export interface Runtime {  
  version: string;  
  environment: string;  
  profile?: any;  
  logger?: Logger;  
  bundler?: Bundler;  
  authentication?: Authentication;  
  remotes?: Array<Remotes>;  
  plugins?: Array<Plugin>;  
}
```

### Errors

Error message for when the Dream.mf runtime is not found.

```typescript
export const RuntimeNotFoundError = "Dream.mf Runtime was not detected. Attempting initialization.";
```