# Developers

## Private Key

### How is my private key stored?

Torus splits a user’s private keys into shares across a network of nodes, and allows a user to retrieve this using natural login mechanisms like social authentication. You need access to more than half of the shares to reconstruct the private key.

### What is Shamir secret sharing?

2 points make a line right? Draw a straight line and write down the coordinates of 3 points. Erase the line. 

You now need at least 2 out of 3 of the points are required to reconstruct the line.

This is a 2/3 Shamir secret sharing of the original line.

### Should I backup my keys?

Our nodes have managed volumes and snapshot policies to ensure that key shares are not lost. We also have coverage that extends to key loss due to technical failures. 

### Can I get access to a user's private keys?

No...

## Privacy

### Will Torus have access to my contacts related to my OAuth login?

No, the initial login only requests for the minimal public information, which you can see during the OAuth popup screen by the 3rd-party provider. The purpose of the login is only for verification of your identity, not for access to your personal information.

### How long is my login persisted? Can Google/Facebook/Reddit track my activity?

We log you out of your 3rd-party account immediately after your identity is verified. The only information that is accessible to these 3rd-party login providers is that you were logged in \(and logged out\) with Torus.

## Torus

### How do I start using Torus?

For DApp integrations, refer the ["Getting Started"](../getting-started.md) section. To use the wallet, head over to [https://app.tor.us](https://app.tor.us)

### Can I use the Torus wallet outside of a browser context?

There are several restrictions. Some integrations are possible \(eg. native support, Chrome extensions\), whereas others are not \(eg. using Torus wallet in a server context\). Right now, we only have browser based support. 

### How can i become one of the nodes running Torus?

We are currently running the network as a permissioned network, so there is a whitelist process, please reach out at hello@tor.us

## Any other questions?

If you have any questions that are yet to be addressed here, feel free to contact us via email at hello@tor.us or on Telegram at [https://t.me/TorusLabs](https://t.me/TorusLabs).

