Sure, here is the documentation for the logging package in your Dream.mf framework:


# Dream.mf Logging Package

## Overview

The logging package in Dream.mf provides a standardized way to log various events and errors across your application. It offers functions to log different types of events and configurations to handle these logs in custom ways.

## Interfaces

### LogConfig

```typescript
interface LogConfig {
  debug: Boolean;
  logGeneral: Function | undefined;
  logAuthentication: Function | undefined;
  logException: Function | undefined;
  logPageView: Function | undefined;
  logFetch: Function | undefined;
  logEvent: Function | undefined;
  logFederation: Function | undefined;
}
```

#### Properties

- **debug**: Boolean flag to enable or disable debug mode.
- **logGeneral**: Function invoked when a general log is recorded.
- **logAuthentication**: Function invoked when an authentication log is recorded.
- **logException**: Function invoked when an exception log is recorded.
- **logPageView**: Function invoked when a page view log is recorded.
- **logFetch**: Function invoked when a fetch log is recorded.
- **logEvent**: Function invoked when a generic event log is recorded.
- **logFederation**: Function invoked when a federation log is recorded.

### LogListenerProps

```typescript
interface LogListenerProps {
  config: LogConfig;
}
```

#### Properties

- **config**: Configuration object of type `LogConfig`.

## Constants

### LogLevel

```typescript
const LogLevel = {
  Information: 0,
  Warning: 1,
  Error: 2,
};
```

Enumeration for different log levels (Work in Progress and not used yet).

### LogType

```typescript
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

Enumeration for different types of log events.

## Functions

### DreamMFLogClient

```typescript
const DreamMFLogClient = {
  logGeneral: (detail) => { /* implementation */ },
  logAuthentication: (detail) => { /* implementation */ },
  logException: (detail, exception) => { /* implementation */ },
  logEvent: (detail) => { /* implementation */ },
  logFetch: (detail) => { /* implementation */ },
  logPageView: (detail) => { /* implementation */ },
  logFederation: (url, scope, module) => { /* implementation */ },
  log: (detail, loggerType) => { /* implementation */ },
};
```

#### logGeneral

Logs a general event.

- **Parameters**: 
  - `detail` (any): Details of the event to log.

#### logAuthentication

Logs an authentication event.

- **Parameters**: 
  - `detail` (any): Details of the event to log.

#### logException

Logs an exception event.

- **Parameters**: 
  - `detail` (any): Details of the event to log.
  - `exception` (Error): The exception to log.

#### logEvent

Logs a generic event.

- **Parameters**: 
  - `detail` (any): Details of the event to log.

#### logFetch

Logs a fetch event.

- **Parameters**: 
  - `detail` (any): Details of the event to log.

#### logPageView

Logs a page view event.

- **Parameters**: 
  - `detail` (any): Details of the event to log.

#### logFederation

Logs a federation event.

- **Parameters**: 
  - `url` (string): The URL of the federation.
  - `scope` (string): The scope of the federation.
  - `module` (string): The module of the federation.

#### log

Logs an event of a specified type.

- **Parameters**: 
  - `detail` (any): Details of the event to log.
  - `loggerType` (string): The type of log event.

## Components

### DreamMFLogListener

```typescript
const DreamMFLogListener = ({ config }: LogListenerProps) => { /* implementation */ };
```

#### Props

- **config**: Configuration object of type `LogConfig`.

#### Description

A component that sets up event listeners for log events based on the provided configuration. It automatically registers and unregisters event listeners on mount and unmount.

## Functions (Listener Management)

### RegisterListeners

```typescript
const RegisterListeners = (config: LogConfig) => { /* implementation */ };
```

Registers event listeners based on the provided `LogConfig`.

- **Parameters**:
  - `config` (LogConfig): Configuration object for logging.

### DeregisterListeners

```typescript
const DeregisterListeners = (config: LogConfig) => { /* implementation */ };
```

Deregisters event listeners based on the provided `LogConfig`.

- **Parameters**:
  - `config` (LogConfig): Configuration object for logging.
```

This documentation provides a detailed overview of the logging package, including interface definitions, constants, functions, and their usages.