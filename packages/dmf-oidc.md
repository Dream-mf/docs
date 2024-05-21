# Dream.mf OIDC Authentication Package

The Dream.mf OIDC authentication package simplifies integrating OpenID Connect (OIDC) for secure and robust user authentication in your application. It offers out-of-the-box components and hooks to manage authentication state, redirect users, and protect routes effortlessly. This package works seamlessly with other Dream.mf packages, ensuring a cohesive development experience. With its flexible configuration, it supports various identity providers and custom authentication flows. Enhance your application's security with minimal setup using Dream.mf's OIDC authentication package.

## Table of Contents

- [Installation](#installation)
- [Initialization](#initialization)
- [API](#api)
  - [DreamMFContextGuard](#dreammfcontextguard)
  - [HandleAuthRoute](#handleauthroute)
  - [DreamMFAuthProvider](#dreammfauthprovider)
  - [useDreamAuth](#usedreamauth)
- [Types](#types)
  - [DreamMFAuthConfig](#dreammfauthconfig)
  - [DreamMFRequestInit](#dreammfrequestinit)
- [Usage Examples](#usage-examples)

## Installation

```bash
npm install @dream.mf/oidc
```

## Initialization

To initialize the OIDC authentication in your Dream.mf project, you need to wrap your application with `DreamMFAuthProvider`.

```tsx
import { DreamMFAuthProvider, BaseAuthConfig } from '@dream.mf/oidc';

const authConfig = {
  ...BaseAuthConfig,
  authority: 'YOUR_AUTHORITY_URL',
  client_id: 'YOUR_CLIENT_ID',
  client_secret: 'YOUR_CLIENT_SECRET',
  redirect_uri: 'YOUR_REDIRECT_URI',
  scope: 'YOUR_SCOPE',
  post_logout_redirect_uri: 'YOUR_POST_LOGOUT_REDIRECT_URI',
  useFetchInterceptor: true,
};

const App = () => (
  <DreamMFAuthProvider config={authConfig}>
    <YourRoutes />
  </DreamMFAuthProvider>
);
```

## API

### DreamMFContextGuard

A component to protect routes or components based on authentication state.

#### Usage

```tsx
import { DreamMFContextGuard } from '@dream.mf/oidc';

const ProtectedComponent = () => (
  <DreamMFContextGuard fallback={<div>You need to log in to access this component.</div>}>
    <div>Protected Content</div>
  </DreamMFContextGuard>
);
```

### HandleAuthRoute

A component to handle authentication routes and redirect users after successful login.

#### Usage

```tsx
import { HandleAuthRoute } from '@dream.mf/oidc';
import { Routes, Route } from 'react-router-dom';

const AppRoutes = () => (
  <Routes>
    <Route path="/auth" element={<HandleAuthRoute />} />
  </Routes>
);
```

### DreamMFAuthProvider

A provider to initialize authentication settings using OIDC.

#### Usage

```tsx
import { DreamMFAuthProvider, BaseAuthConfig } from '@dream.mf/oidc';

const authConfig = {
  ...BaseAuthConfig,
  authority: 'YOUR_AUTHORITY_URL',
  client_id: 'YOUR_CLIENT_ID',
  client_secret: 'YOUR_CLIENT_SECRET',
  redirect_uri: 'YOUR_REDIRECT_URI',
  scope: 'YOUR_SCOPE',
  post_logout_redirect_uri: 'YOUR_POST_LOGOUT_REDIRECT_URI',
  useFetchInterceptor: true,
};

const App = () => (
  <DreamMFAuthProvider config={authConfig}>
    <YourRoutes />
  </DreamMFAuthProvider>
);
```

### useDreamAuth

A hook to access authentication state and utilities.

#### Usage

```tsx
import { useDreamAuth } from '@dream.mf/oidc';

const AuthenticatedComponent = () => {
  const auth = useDreamAuth();

  if (auth.isAuthenticated) {
    return <div>Welcome, {auth.user?.profile?.name}</div>;
  }

  return <div>Please log in.</div>;
};
```

## Types

### DreamMFAuthConfig

Configuration type for the authentication provider.

```ts
import { UserManagerSettings, WebStorageStateStore } from 'oidc-client-ts';

export type DreamMFAuthConfig = UserManagerSettings & {
  useFetchInterceptor: boolean;
  useAxiosInterceptor: boolean;
};

export const BaseAuthConfig: DreamMFAuthConfig = {
  authority: '',
  client_id: '',
  client_secret: '',
  redirect_uri: '',
  scope: '',
  post_logout_redirect_uri: '',
  response_type: 'code',
  useFetchInterceptor: false,
  useAxiosInterceptor: false,
  userStore: new WebStorageStateStore({ store: window.localStorage }),
};
```

### DreamMFRequestInit

Extension type for fetch options.

```ts
export interface DreamMFRequestInit extends RequestInit {
  useAuthentication?: boolean;
}
```

## Usage Examples

### Example 1: Integrating Authentication with Host and Routing

```tsx
import React from 'react';
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import { DreamMFAuthProvider, BaseAuthConfig, HandleAuthRoute, DreamMFContextGuard } from '@dream.mf/oidc';

const authConfig = {
  ...BaseAuthConfig,
  authority: 'YOUR_AUTHORITY_URL',
  client_id: 'YOUR_CLIENT_ID',
  client_secret: 'YOUR_CLIENT_SECRET',
  redirect_uri: 'YOUR_REDIRECT_URI',
  scope: 'YOUR_SCOPE',
  post_logout_redirect_uri: 'YOUR_POST_LOGOUT_REDIRECT_URI',
  useFetchInterceptor: true,
};

const Host = () => (
  <DreamMFAuthProvider config={authConfig}>
    <BrowserRouter>
      <Routing />
    </BrowserRouter>
  </DreamMFAuthProvider>
);

const Routing = () => (
  <Routes>
    <Route path="/" element={<Index />} />
    <Route path="/sample/:id" element={<Sample />} />
    <Route path="/home" element={<Home />} />
    <Route path="/auth" element={<HandleAuthRoute />} />
    <Route path="/logout" element={<Logout />} />
    <Route path="*" element={<NotFound />} />
  </Routes>
);

const Index = () => <div>Index Page</div>;
const Sample = () => <div>Sample Page</div>;
const Home = () => <div>Home Page</div>;
const Logout = () => <div>Logout Page</div>;
const NotFound = () => <div>404 Not Found</div>;

const App = () => <Host />;
export default App;
```

### Example 2: Protecting Components with DreamMFContextGuard

```tsx
import React from 'react';
import { DreamMFContextGuard } from '@dream.mf/oidc';
import Layout from './Layout';

const ProfilePage = () => (
  <Layout>
    <DreamMFContextGuard fallback={<div>Loading...</div>}>
      <ProfileRemote />
    </DreamMFContextGuard>
  </Layout>
);

const ProfileRemote = () => <div>Profile Content</div>;

export default ProfilePage;
```

---

This should provide a comprehensive guide on how to use the OIDC authentication package in Dream.mf. Feel free to adjust according to your specific needs!