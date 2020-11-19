# Setting Up Verifiers/Logins

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
Register at [https://register.directauth.io](https://register.directauth.io) to get your verifier spun up today!
{% endhint %}

