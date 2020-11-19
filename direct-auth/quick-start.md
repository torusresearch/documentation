---
description: Integrate DirectAuth in your web application today
---

# Quick Start

Try our hosted example [here](https://vue-direct.tor.us)

To allow your web app to retrieve keys from the Torus Network, we'll be using the [direct-web-sdk](https://github.com/torusresearch/torus-direct-web-sdk), the repo itself has examples that you can also refer to:

1. Install the package `npm i @toruslabs/torus-direct-web-sdk`
2. Serve [service worker](https://github.com/torusresearch/torus-direct-web-sdk/blob/master/serviceworker/sw.js) from `baseUrl` where baseUrl is the one passed while instantiating `DirectWebSdk` for specific login \(example [http://localhost:3000/serviceworker/](http://localhost:3000/serviceworker/)\). If you're already using a sw, pls ensure to port over the fetch override from [our service worker](https://github.com/torusresearch/torus-direct-web-sdk/blob/master/serviceworker/sw.js)
3. For browsers where service workers are not supported or if you wish to not use service workers, create and serve [redirect page](https://github.com/torusresearch/torus-direct-web-sdk/blob/master/serviceworker/redirect.html) from `baseUrl/redirect` where baseUrl is the one passed while instantiating `DirectWebSdk` for specific login \( example [http://localhost:3000/serviceworker/](http://localhost:3000/serviceworker/)\)
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

 6. Trigger the login

```javascript
const userInfo = await torus.triggerLogin({
  typeOfLogin: "google",
  verifier: "google",
  clientId: "MY CLIENT ID GOOGLE",
});
```

If you're building a chrome extension or electron app, please set `redirectToOpener: true` and modify the origin of postMessage from `"http://localhost:3000"` to your hosted domain in redirect.html and sw.js. \(This allows the popup to redirect to your app if the communication to opener window fails\)

For integration into other mobile, native or other platforms please refer to [Integrating DirectAuth](integrating-directauth/). 

## Registration

Firstly, register your app with OAuth login providers. There are two types of providers which Torus supports. Click on the links to see instructions on how to configure OAuth provider. 

* Native providers allow you to register your app directly with [implicit grant support ](https://oauth.net/2/grant-types/implicit/)and use with Torus. The following are the supported native providers

  * [Google](https://support.google.com/googleapi/answer/6158849)
  * [Facebook](https://developers.facebook.com/docs/apps)
  * [Reddit](https://github.com/reddit-archive/reddit/wiki/oauth2)
  * [Discord](https://discord.com/developers/docs/topics/oauth2)
  * [Twitch](https://dev.twitch.tv/docs/authentication/#registration)

  For native providers, please provide us with the client/app ID registered with the provider.

* Proxy providers require you to register your app on OAuth provider and add some config on their app. Proxy providers enable you to use some non-implicit type logins. \(e.g: Twitter, Apple, GitHub, LinkedIn, Email-Password, Magic link, WeChat etc.\)  Some examples of proxy providers

  * [Auth0](https://auth0.com/docs/connections)
  * [Okta](https://developer.okta.com/docs/concepts/social-login/)
  * [Cognito](https://aws.amazon.com/cognito/getting-started/)
  * or any custom OAuth2 compliant login provider

  For proxy providers, please provide us with the Client ID, Authentication domain provided by the proxy provider.

{% hint style="info" %}
Register at [http://register.directauth.io](http://register.directauth.io) to get your verifier spun up today!
{% endhint %}

