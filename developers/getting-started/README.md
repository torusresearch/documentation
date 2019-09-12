---
description: >-
  Torus streamlines all DApp login processes, and allows users log in to your
  DApp with Google OAuth Login accounts without the need for any complicated
  tools.
---

# Getting Started

## Install Torus

Integrating Torus with your DApp is as seamless as using it. Let us start by first installing Torus onto your DApp website.

### Integrate Torus onto your Website via Script Tag

The code snippet below sets Torus as the default login method for the DApp, paste the following script to the &lt;body&gt; of index.html.

{% embed url="https://gist.github.com/chaitanyapotti/733405286923fa047af4cb26d167acd4" caption="Torus embed script" %}

### OR

### Install Torus with a NPM Package

You can install via a [npm package](https://www.npmjs.com/package/@toruslabs/torus-embed).

```javascript
  import Torus from "@toruslabs/torus-embed";
  import Web3 from "web3";
  
  const torus = new Torus();
  await torus.init();
  await torus.login(); // await torus.ethereum.enable()
  const web3 = new Web3(torus.provider);
```

Please refer to the [examples](https://github.com/torusresearch/torus-embed/tree/master/examples) folder for sample implementations

### Test Torus with your DApp

Test if Torus works with your DApp with the code snippet from below:

```javascript
// Start using web3 in your dapp
$ web3.eth.accounts[0]
> "0x05B53A73B...150C005e21"
```

### 

