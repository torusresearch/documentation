---
description: >-
  Torus streamlines onboarding by allowing users to start using DApps via
  existing social accounts.
---

# Getting Started

## Install Torus

### NPM Package

You can install via a [npm package](https://www.npmjs.com/package/@toruslabs/torus-embed).

* Basic:

```javascript
import Torus from "@toruslabs/torus-embed";
import Web3 from "web3";

const torus = new Torus();
await torus.init();
await torus.login(); // await torus.ethereum.enable()
const web3 = new Web3(torus.provider);
```

* Advanced:

```javascript
import Torus from "@toruslabs/torus-embed";
import Web3 from "web3";

const torus = new Torus({
  buttonPosition: "top-left" // default: bottom-left
});
await torus.init({
  buildEnv: "production", // default: production
  enableLogging: true, // default: false
  network: {
    host: "kovan", // default: mainnet
    chainId: 42, // default: 1
    networkName: "Kovan Test Network" // default: Main Ethereum Network
  },
  showTorusButton: false // default: true
});
await torus.login(); // await torus.ethereum.enable()
const web3 = new Web3(torus.provider);
```

Please refer to the [examples](https://github.com/torusresearch/torus-embed/tree/master/examples) folder for sample implementations or the Class documentation for further init options

### Web3/ether.js

Integrating with Torus gives you a provider, which can be wrapped by the Web3. This instance functions similar to that as Metamask's web3 provider, and we have taken great care to make it compatible with Metamask's [Web3 APIs](https://web3js.readthedocs.io/en/1.0/).

### AngularJS users

**Please include the following NPM packages:**

```bash
process, buffer
```

And add the following code into polyfills.ts.

```javascript
import * as process from 'process';
window['process'] = process;
(window as any).global = window;
(window as any).global.Buffer = (window as any).global.Buffer || require('buffer').Buffer;
```

### Script Tag

The code snippet below sets Torus as the default login method for the DApp, paste the following script to the &lt;body&gt; of index.html.

{% embed url="https://gist.github.com/chaitanyapotti/733405286923fa047af4cb26d167acd4" caption="Torus embed script" %}

The script tag creates a `window.ethereum` web3 provider. This can be wrapped with your desired version of Web3 to create a web3 object. We also provide a `window.web3` object \(v0.20.7\), which allows for backward compatibility with existing DApps that are using Metamask's web3 object.

#### IPFS

For DApps using IPFS, we also have a version of this script hosted on IPFS.

```text
<script src="https://cloudflare-ipfs.com/ipfs/QmcQADhGeYvyRm56xoijAM4gs7ZLBu3WfeotTpc7SdUuMa"
integrity="sha384-PAg4PvuFYzWY4THGynmPbfqGUb0gekmTzumGoo/yhESiri+rsds0O65AJW3eEHMc"
crossorigin="anonymous"></script>
```

### Development Environment

If you are to developing with Torus in a local environment/with ganache, https is necessary to interact with app.tor.us. Checkout [the steps here](https://docs.tor.us/developing-with-torus/ganache) to get started.

