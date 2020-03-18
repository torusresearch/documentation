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

### Will Torus have access to a user's contacts from the OAuth login?

No, the initial login only requests for the minimal public information, which you can see during the OAuth popup screen by the 3rd-party provider. The purpose of the login is only for verification of your identity, not for access to your personal information.

### How long is the user login persisted? Can Google/Facebook/Reddit track my activity?

We log you out of your 3rd-party account immediately after your identity is verified. The only information that is accessible to these 3rd-party login providers is that you were logged in \(and logged out\) with Torus.

### Is it possible to allow users to persist their session with the DApp, so that they don't have to login again?

  
It is definitely possible but keeping the user logged in for just that session gives better privacy guarantees for users. There is no easy way for Torus to ensure that users are logged out by the DApp, so we opted to keep user sessions self contained.

Most Oauth providers already solve this problem by auto-approving the login request if the user logged in recently, and it may not even require user interaction. For example, for Facebook login, users do not even need to click anything if they have recently logged in.

## Torus

### How do I start using Torus?

For DApp integrations, refer the ["Getting Started"](../getting-started/) section. To use the wallet, head over to [https://app.tor.us](https://app.tor.us)

### Can I use the Torus wallet outside of a browser context?

There are several restrictions. Some integrations are possible \(eg. native support, Chrome extensions\), whereas others are not \(eg. using Torus wallet in a server context\). Right now, we only have browser based support. 

### What browsers are supported?

Chrome, Edge, Firefox, Brave, Safari and other major browsers. IE and private browsing in Safari are not supported.

### How can i become one of the nodes running Torus?

We are currently running the network as a permissioned network, so there is a whitelist process, please reach out at hello@tor.us

## Any other questions?

If you have any questions that are yet to be addressed here, feel free to contact us via email at hello@tor.us or on Telegram at [https://t.me/TorusLabs](https://t.me/TorusLabs).

