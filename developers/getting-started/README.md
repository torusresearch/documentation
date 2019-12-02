---
description: >-
  Torus streamlines all DApp login processes and allows users to log in to your DApp with Google OAuth Login accounts without the need for any complicated tools. Integrating Torus with your DApp is as seamless as using it. Let us start by first installing Torus onto your DApp website.
---

# Getting Started

## Enviornment requirements

To ensure an efficient implementation process, we highly encourage you to configure the environment to the requirements below :

- NodeJS: 10.x

## Install Torus

Integrating Torus with your DApp is as seamless as using it. Let us start by first installing Torus onto your DApp website.

### Install Torus with a NPM Package

You can install via a [npm package](https://www.npmjs.com/package/@toruslabs/torus-embed).

- Basic:

  ```javascript
  import Torus from "@toruslabs/torus-embed";
  import Web3 from "web3";

  const torus = new Torus();
  await torus.init();
  await torus.login(); // await torus.ethereum.enable()
  const web3 = new Web3(torus.provider);
  ```

- Advanced:

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

Please refer to the [examples](https://github.com/torusresearch/torus-embed/tree/master/examples) folder for sample implementations

### OR

### Integrate Torus onto your Website via Script Tag

The code snippet below sets Torus as the default login method for the DApp, paste the following script to the &lt;body&gt; of index.html.

{% embed url="https://gist.github.com/chaitanyapotti/733405286923fa047af4cb26d167acd4" caption="Torus embed script" %}

<!--

### Test Torus with your DApp

Test if Torus works with your DApp with the code snippet from below:

```javascript
// Start using web3 in your dapp
$ web3.eth.accounts[0]
> "0x05B53A73B...150C005e21"
``` -->
