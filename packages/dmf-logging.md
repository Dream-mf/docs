# Dream.mf Logging Package Documentation

The Dream.mf logging package provides logging and log listener functionality that can be used independently in your application or within other Dream.mf packages. This includes a log listener for the host, configured against your log aggregator, and supports multiple aggregators. This allows your remote to use the log client directly with minimal setup.

## Installation

To install the Dream.mf logging package, you should include it as a dependency in your project.

```bash
npm install dream.mf-logging
```

## Log Configuration

The `logConfig` object provides settings and callback functions for the log listener.

### Example

```javascript
import { logConfig } from 'dream.mf-logging';

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
```

## Log Listener

The `DreamMFLogListener` subscribes to global log events and applies your own log aggregator.

### Usage

```javascript
import { DreamMFLogListener } from 'dream.mf-logging';

const App = () => {
  const config = {
    debug: true,
    logGeneral: (event) => console.log("General log: ", event.detail),
    logException: (event) => console.log("Exception log: ", event.detail),
    // Add other log handlers as needed
  };

  return (
    <div>
      <DreamMFLogListener config={config} />
      {/* rest of your app */}
    </div>
  );
};
```

## Log Client

The `DreamMFLogClient` provides function calls for logging specific event types.

### Methods

- `logGeneral(detail)`
- `logAuthentication(detail)`
- `logException(detail, exception)`
- `logEvent(detail)`
- `logFetch(detail)`
- `logPageView(detail)`
- `logFederation(url, scope, module)`
- `log(detail, loggerType)`

### Example

```javascript
import { DreamMFLogClient } from 'dream.mf-logging';

DreamMFLogClient.logGeneral({ message: "This is a general log" });
DreamMFLogClient.logException({ message: "This is an exception log" }, new Error("Exception occurred"));
DreamMFLogClient.logFetch({ url: "/api/data", status: 200 });
```

## Register and Deregister Listeners

Utility functions to register and deregister event listeners for logging.

### Usage

```javascript
import { RegisterListeners, DeregisterListeners } from 'dream.mf-logging';

const config = {
  debug: true,
  logGeneral: (event) => console.log("General log: ", event.detail),
  logException: (event) => console.log("Exception log: ", event.detail),
  // Add other log handlers as needed
};

// Register listeners
RegisterListeners(config);

// Deregister listeners when no longer needed
DeregisterListeners(config);
```

## Constants

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