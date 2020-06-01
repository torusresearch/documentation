---
description: Also called verifiers
---

# Supported Authenticators/Logins

DirectAuth deploys a custom Verifier Script for your application on the Torus Network. Verifier Scripts determine the access structure to your users keys and the set Verifier Scripts chosen determine which logins your application will ultimately use. You can read more about verifiers [here](https://medium.com/toruslabs/key-assignments-resolution-and-retrieval-afb984500612).

Known logins or attestation methods that can be chosen include OAuths and custom logins methods:

| Attestation/Login Method | Lookups |
| :--- | :--- |
| Google OAuth2 | Y |
| Reddit OAuth2 | Y |
| Discord OAuth2 | Y |
| Twitch OAuth2 | N |
| Facebook OAuth2 | N |
| Apple OAuth2 | N |
| Auth0 login | Depends |
| AWS Cognito | Depends |
| Custom JWT logins | Depends |
| Custom ECDSA logins | Depends |

There are some nuances with certain login providers, so don't hesitate to get in touch to get further details.

### Aggregating Logins/Verifiers

It is possible to combine these attestation methods in AND/OR ways. For example you could combine a Google AND Reddit login to access a key. this vice versa can be done for Google OR Reddit. For these aggregate verifiers, its important to note that a user's verifierID must be known ahead of time, as keys in Torus are append only. Meaning to assign to a key to a user with the aggregate verifier Google OR Reddit, I must know the users gmail account and reddit account ahead of time. 

This disadvantage can be subverted if the two attestation methods share the same verifierID. For example, Auth0 generic email logins OR Google logins both use email accounts as the verifierID, as such the verifierID can me shared amonst the two. This is referred to as a Single ID Verifier.

### Using your own custom login provider

You can use your own login provider's with Torus, using one of the custom login schemes \(either via JWTs or ECDSA signatures\). This way, your users can still use your existing login provider, with DirectAuth. As long as your application follows the 

### Can XXXX authenticator/login be supported?

The list isn't comprehensive to all the logins that the Torus system is capable of supporting, if you'd like support for a particular login system do send your query over to hello@tor.us

