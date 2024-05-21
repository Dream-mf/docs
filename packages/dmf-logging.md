Sure, here is the updated documentation with the table of contents section:

# Dream.mf Logging Package Documentation

The Dream.mf logging package provides logging and log listener functionality that can be used independently in your application or within other Dream.mf packages. This includes a log listener for the host, configured against your log aggregator, and supports multiple aggregators. This allows your remote to use the log client directly with minimal setup.

## Table of Contents

- [Installation](#installation)
- [Initialization](#initialization)
- [API](#api)
  - [logGeneral](#loggeneral)
  - [logAuthentication](#logauthentication)
  - [logException](#logexception)
  - [logEvent](#logevent)
  - [logFetch](#logfetch)
  - [logPageView](#logpageview)
  - [logFederation](#logfederation)
  - [log](#log)
- [Types](#types)
  - [LogLevel](#loglevel)
  - [LogType](#logtype)
  - [LogConfig](#logconfig)

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

To initialize the logging functionality, configure the `logConfig` object and instantiate the `DreamMFLogListener`.

### Example

```javascript
import { DreamMFLogListener, logConfig } from 'dream.mf-logging';

const myLogConfig = {
  ...logConfig,
  debug: true,
  logGeneral: (data) => {
    // handle general logs
  },
  logException: (data) => {
    // handle exceptions
  },
  // Add other log handlers as needed
};

const App = () => (
  <div>
    <DreamMFLogListener config={myLogConfig} />
    {/* rest of your app */}
  </div>
);

export default App;
```

## API

### logGeneral

Logs a general message.

```javascript
import { DreamMFLogClient } from 'dream.mf-logging';

DreamMFLogClient.logGeneral({ message: "This is a general log" });
```

### logAuthentication

Logs an authentication-related message.

```javascript
import { DreamMFLogClient } from 'dream.mf-logging';

DreamMFLogClient.logAuthentication({ user: "admin", action: "login" });
```

### logException

Logs an exception message along with the exception object.

```javascript
import { DreamMFLogClient } from 'dream.mf-logging';

DreamMFLogClient.logException({ message: "This is an exception log" }, new Error("Exception occurred"));
```

### logEvent

Logs a custom event message.

```javascript
import { DreamMFLogClient } from 'dream.mf-logging';

DreamMFLogClient.logEvent({ name: "customEvent", data: "eventData" });
```

### logFetch

Logs a fetch operation message.

```javascript
import { DreamMFLogClient } from 'dream.mf-logging';

DreamMFLogClient.logFetch({ url: "/api/data", status: 200 });
```

### logPageView

Logs a page view message.

```javascript
import { DreamMFLogClient } from 'dream.mf-logging';

DreamMFLogClient.logPageView({ page: "/home" });
```

### logFederation

Logs a module federation operation message.

```javascript
import { DreamMFLogClient } from 'dream.mf-logging';

DreamMFLogClient.logFederation("http://example.com/remoteEntry.js", "scopeName", "moduleName");
```

### log

Logs a message of a specified log type.

```javascript
import { DreamMFLogClient, LogType } from 'dream.mf-logging';

DreamMFLogClient.log({ message: "Custom log message" }, LogType.General);
```

## Types

### LogLevel

Defines log levels.

```javascript
const LogLevel = {
  Information: 0,
  Warning: 1,
  Error: 2,
};
```

### LogType

Defines log types used in custom events.

```javascript
const LogType = {
  General: "GENERAL",
  Authentication: "AUTHENTICATION",
  Exception: "EXCEPTION",
  PageView: "PAGE_VIEW",
  Fetch: "FETCH",
  Event: "EVENT",
  Federation: "FEDERATION",
};
```

### LogConfig

Interface for the log listener configuration.

```typescript
interface LogConfig {
  debug: boolean;
  logGeneral?: (data: any) => void;
  logAuthentication?: (data: any) => void;
  logException?: (data: any) => void;
  logPageView?: (data: any) => void;
  logFetch?: (data: any) => void;
  logEvent?: (data: any) => void;
  logFederation?: (data: any) => void;
}
```

### Debug Prefix

Prefix used for debug messages.

```javascript
const debugPrefix = `[DREAM.MF-LOGGER]`;
```

### Example

```javascript
console.log(`${debugPrefix} This is a debug message`);
```

## Summary

The Dream.mf logging package provides a comprehensive logging solution integrated with your module federation setup. By using the out-of-the-box configurations, listener registration, and client logging methods, you can implement a robust logging mechanism with minimal setup.

```javascript
import { logConfig, DreamMFLogListener, DreamMFLogClient } from 'dream.mf-logging';

const logConfiguration = {
  ...logConfig,
  debug: true,
  logGeneral: (data) => console.log("General: ", data),
  logException: (data) => console.log("Exception: ", data),
};

const App = () => (
  <div>
    <DreamMFLogListener config={logConfiguration} />
    {/* Application components here */}
  </div>
);

// Usage Example of Log Client
DreamMFLogClient.logGeneral({ message: "Application started" });
```

This documentation provides an overview and guidelines on how to use the Dream.mf logging package to integrate logging and monitoring capabilities into your applications and federated modules.