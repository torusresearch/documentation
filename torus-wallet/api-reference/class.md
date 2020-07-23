---
description: 'create, initialize, and clean up a Torus web3 instance.'
---

# Initialization

## Torus

This is the main class of anything related to Torus

```javascript
const Torus = require("@toruslabs/torus-embed");
```

Using ES6,

```javascript
import Torus from "@toruslabs/torus-embed";
```

Then, create a new instance of Torus.

```javascript
const torus = new Torus(options);
```

The Torus constructor takes an object with `TorusCtorArgs` as input.

**Parameters**

* `options` - `TorusCtorArgs` \(optional\) : The options of the constructor
  * `buttonPosition` - `enum` \(optional\) : The position of the Torus button. Supported values are `top-left` `bottom-left` `top-right` `bottom-right`

**Returns**

* `Object`: The torus instance with all its methods and events.

**Reference**

```javascript
interface TorusCtorArgs {
  buttonPosition?: "top-left" | "top-right" | "bottom-right" | "bottom-left";
}
```

**Examples**

```javascript
const torus = new Torus();
```

```javascript
const torus = new Torus({
  buttonPosition: "top-left" // default: 'bottom-left'
});
```

## init

Initialize the torus object after creation

```javascript
await torus.init(params);
```

**Parameters**

* `params` - `TorusParams` \(optional\) : The parameters passed to initialize Torus object
  * `network` - `NetworkInterface` \(optional\) : The network options. Used for setting a default network
  * `buildEnv` - `enum` \(optional\): The build environment to use. Supported values are `production` `development` `staging` `testing`
  * `enableLogging` - `boolean` \(optional\) : Enables/disables logging. Useful for debugging
  * `showTorusButton` - `boolean` \(optional\) : Shows/Hides the Torus Button
  * `enabledVerifiers` - `VerifierStatus` \(optional\) : Hides certain types of logins \(default is true\)
  * `integrity` - `IntegrityParams` \(optional\) : Enables optional integrity checking \(default is false\)
  * `loginConfig` - Array of login config items. Used to modify the default logins/ add new logins. Read more on [Login Config](class.md#login-config).

**Returns**

* `Promise<void>` : Returns a promise which resolves to void

**Reference**

```typescript
interface TorusParams {
  network?: NetworkInterface;
  buildEnv?: "production" | "development" | "staging" | "testing";
  enableLogging?: boolean;
  showTorusButton?: boolean;
  enabledVerifiers?: VerifierStatus;
  integrity?: IntegrityParams;
  loginConfig?: LoginConfig;
}

interface VerifierStatus {
  google?: boolean;
  facebook?: boolean;
  reddit?: boolean;
  twitch?: boolean;
  discord?: boolean;
}

interface NetworkInterface {
  host:
    | "mainnet"
    | "rinkeby"
    | "ropsten"
    | "kovan"
    | "goerli"
    | "localhost"
    | "matic"
    | string;
  chainId?: number;
  networkName?: string;
}

interface IntegrityParams {
  check: boolean;
  hash?: string;
  version?: string;
}
```

**Examples**

```javascript
await torus.init();
```

```javascript
await torus.init({
  network: {
    host: "rinkeby" // default : 'mainnet'
  }
});
```

```javascript
await torus.init({
  network: {
    host: "https://ethboston1.skalenodes.com:10062", // mandatory
    chainId: 1, // optional
    networkName: "Skale Network" // optional
  }
});
```

```javascript
await torus.init({
  buildEnv: "staging", // uses staging.tor.us
  enableLogging: false, // default : false
  network: {
    host: "kovan" // default : 'mainnet'
  },
  showTorusButton: false, // default: true
  enabledVerifiers: {
    facebook: false // default: true
  }
});
```

```javascript
await torus.init({
  network: {
    host: "matic" // mandatory
  },
  showTorusButton: true // default: true
});
```

## loginConfig

Array of login config items. Used to modify the default logins/ add new logins under `torus.init`.

```javascript
await torus.init({
  loginConfig: {
    [verifier]: loginConfigItem
  }
});
```

**Parameters**

* `loginConfig` - `LoginConfig` \(optional\) : Array of login configuration per verifier
  * `verifier` - Verifier provided by torus as a key or a default verifier used by torus
* `loginConfigItem` - `LoginConfigItem` : parameters per verifier
  * `typeOfLogin` - `LOGIN_TYPE`: The type of login
  * `description` - `string` \(optional\) : Description for button. If provided, it renders as a full length button. else, icon button
  * `clientId` - `string` \(optional\) : Custom client\_id. If not provided, we use the default for torus app
  * `logoHover` - `string` \(optional\) : Logo to be shown on mouse hover. If not provided, we use the default for torus app
  * `logoLight` - `string` \(optional\): Logo to be shown on dark background \(dark theme\). If not provided, we use the default for torus app
  * `logoDark` - `string` \(optional\): Logo to be shown on light background \(light theme\). If not provided, we use the default for torus app
  * `showOnModal` - `boolean` \(optional\): Whether to show the login button on modal or not
  * `jwtParameters` - `JwtParameters` \(optional\): Custom JWT parameters to configure the login. Useful for Auth0 configuration

**Reference**

```typescript
type LOGIN_TYPE =
  | 'google'
  | 'facebook'
  | 'reddit'
  | 'discord'
  | 'twitch'
  | 'apple'
  | 'github'
  | 'linkedin'
  | 'twitter'
  | 'weibo'
  | 'line'
  | 'jwt'
  | 'email-password'
  | 'passwordless'

interface LoginConfig {
}

interface LoginConfigItem {
  typeOfLogin: LOGIN_TYPE
  description?: string
  clientId?: string
  logoHover?: string
  logoLight?: string
  logoDark?: string
  showOnModal?: boolean
  jwtParameters?: JwtParameters
}

interface JwtParameters {
  domain: string;
  client_id?: string;
  redirect_uri?: string;
  leeway?: number;
  verifierIdField?: string;
}
```

**Example**

```javascript
await torus.init({
  loginConfig: {
    'google': {
      description: 'Login with google',
      clientId: 'CLIENT_ID',
      logoHover: 'https://sample.com/google-logo-hover.svg',
      logoLight: 'https://sample.com/google-logo-light.svg',
      logoDark: 'https://sample.com/google-logo-dark.svg',
      showOnModal: true,
    },
  },
})
```

## cleanUp

This cleans up the iframe and buttons created by torus package. If the user is logged in, it logs him out first and then cleans up.

```javascript
await torus.cleanUp();
```

**Returns**

* `Promise<void>` : Returns a promise which resolves to void.

**Examples**

```javascript
await torus.cleanUp();
```

