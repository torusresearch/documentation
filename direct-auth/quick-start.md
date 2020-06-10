---
description: Integrate DirectAuth in your web application today
---

# Quick Start

To allow your web app to retrieve keys from the Torus Network, we'll be using the [direct-web-sdk](https://github.com/torusresearch/torus-direct-web-sdk), the repo itself has examples that you can also refer to:

1. Install the package `npm i @toruslabs/torus-direct-web-sdk`
2. Serve [service worker](https://github.com/torusresearch/torus-direct-web-sdk/blob/master/public/sw.js) from `baseUrl` where baseUrl is the one passed while instantiating `DirectWebSdk` for specific login \(example [http://localhost:3000/serviceworker/](http://localhost:3000/serviceworker/)\). If you're already using a sw, pls ensure to port over the fetch override from [our service worker](https://github.com/torusresearch/torus-direct-web-sdk/blob/master/public/sw.js)
3. For browsers where service workers are not supported or if you wish to not use service workers, create and serve [redirect page](https://github.com/torusresearch/torus-direct-web-sdk/blob/master/public/redirect.html) from `baseUrl/redirect` where baseUrl is the one passed while instantiating `DirectWebSdk` for specific login \( example [http://localhost:3000/serviceworker/](http://localhost:3000/serviceworker/)\)
4. At verifier's interface \(where you obtain client id\), please use `baseUrl/redirect` \(eg: [http://localhost:3000/serviceworker/redirect](http://localhost:3000/serviceworker/redirect)\) as the redirect\_uri where baseUrl is the one passed while instantiating `DirectWebSdk`
5. Instantiate the package with your own specific client-id

```javascript
const torus = new DirectWebSdk({
  baseUrl: "http://localhost:3000/serviceworker/",
  proxyContractAddress: "0x4023d2a0D330bF11426B12C6144Cfb96B7fa6183", // details for test net
  network: "ropsten", // details for test net
});
await torus.init();
```

1. Trigger the login

```javascript
const userInfo = await torus.triggerLogin({
  typeOfLogin: "google",
  verifier: "google",
  clientId: "MY CLIENT ID GOOGLE",
});
```

{% hint style="info" %}
Reach out to [hello@tor.us](mailto:hello@tor.us) to get your verifier spun up on the testnet today!
{% endhint %}

For integration into other mobile, native or other platforms please refer to [Integrating DirectAuth](integrating-directauth/). 

