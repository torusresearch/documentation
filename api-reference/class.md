---
description: 'create, initialize, and clean up a Torus web3 instance.'
---

# Initialization

## Torus

This is the main class of anything related to Torus

```javascript
const Torus = require("@toruslabs/torus-embed").default;
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

* `params` - `TorusParams` \(optional\) : The parameters passed to initialize torus object
  * `network` - `NetworkInterface` \(optional\) : The network options. Used for setting a default network
  * `buildEnv` - `enum` \(optional\): The build environment to use. Supported values are `production` `development` `staging` `testing`
  * `enableLogging` - `boolean` \(optional\) : Enables/disables logging. Useful for debugging
  * `showTorusButton` - `boolean` \(optional\) : Shows/Hides the Torus Button
  * `enabledVerifiers` - `VerifierStatus` \(optional\) : Hides certain types of logins \(Default is true\)
  * `integrity` - `IntegrityParams` \(optional\) : Enables Optional integrity checking \(Default is false\)

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

