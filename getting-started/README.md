---
description: Torus streamlines onboarding by allowing users to start using DApps
---

# Getting Started

Depending on your applications needs Torus can be integrated in either via the [iFrame wallet](torus-wallet-integration.md), or through interacting [directly with the Torus Network](directauth-network-integration.md). 

### iFrame wallet integration via NPM

The iFrame wallet allows any application to seamlessly support their user's interactions with Ethereum\(and other chains\). OAuth logins, fiat-to-crypto and much more listed in the features section. You can install via a [npm package](https://www.npmjs.com/package/@toruslabs/torus-embed) or [ipfs](torus-wallet-integration.md#ipfs). or [jsdelivr](https://cdn.jsdelivr.net/npm/@toruslabs/torus-embed) or [unpkg](https://unpkg.com/@toruslabs/torus-embed) More [details](torus-wallet-integration.md)

```javascript
npm i @toruslabs/torus-embed
```

```javascript
import Torus from "@toruslabs/torus-embed";
import Web3 from "web3";

const torus = new Torus();
await torus.init();
await torus.login(); // await torus.ethereum.enable()
const web3 = new Web3(torus.provider);
```

### Direct Torus Network integration

Applications can directly interact with the Torus Network to assign, store and retrieve keys on the network - Distributed Key Generation as a Service. The integration is compatible with both web/native apps, applications get access to the OAuth scopes provided to them \(name/email from Google\) and there are no longer pop-ups - applications literally own the UX. Proceed here for more [information](directauth-network-integration.md) 

