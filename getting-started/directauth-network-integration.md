---
description: Distributed Key Generation as a Service
---

# DirectAuth Integration

Applications can directly interact with the Torus Network to assign, store and retrieve keys on the network - Distributed Key Generation as a Service. The integration is compatible with both web/native apps, applications get access to the OAuth scopes provided to them \(name/email from Google\) and there are no longer pop-ups - applications literally own the UX.

![](../.gitbook/assets/image%20%282%29.png)

Just as how the Torus Wallet has a verifier script for each of the authentication methods, this integration includes a deployment of a verifier script on the BFT layer that the nodes share for the application specifically. Keys which are generated through the DKG protocol are assigned to the verifier script, which shares are respectively retrieved through successful execution of the script. Whilst most integrations integrate different OAuths, the script is generalisable and can be used to combine multiple OAuths, signatures and other varied forms of attestation for a user.

## What does this mean for my application?

Using DirectAuth allows you to manage an app-specific private key for your users, while storing it in the distributed Torus Network. It allows you to control the user experience and interface for all user interactions, without having to rely on the Torus Wallet interface for user confirmations via popups.

Reach out to hello@tor.us or our [dev chat](https://t.me/torusdev) to get a test-net spun up to play with today

