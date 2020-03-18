---
description: Distributed Key Generation as a Service
---

# Direct Torus Network Integration

Applications can directly interact with the Torus Network to assign, store and retrieve keys on the network - Distributed Key Generation as a Service. The integration is compatible with both web/native apps, applications get access to the OAuth scopes provided to them \(name/email from Google\) and there are no longer pop-ups - applications literally own the UX.

![](../.gitbook/assets/image%20%282%29.png)

Just as how the Torus Wallet has a verifier script for each of the authentication methods, this integration includes a deployment of a verifier script on the BFT layer that the nodes share for the application specifically. Keys which are generated through the DKG protocol are assigned to the verifier script, which shares are respectively retrieved through successful execution of the script. Whilst most integrations integrate different OAuths, the script is generalisable and can be used to combine multiple OAuths, signatures and other varied forms of attestation for a user.

This integration provides for a lot of flexibility for applications, beyond just simple key management. Applications can further use the key in a lot of different use cases - for example, its possible to put another salt \(user password\) ontop of the key for further "self-custody", as an encryption key for safe messaging and more.

Reach out to hello@tor.us or our [dev chat](https://t.me/torusdev) to get a test-net spun up to play with today

