---
description: >-
  For updates, also checkout the release [QA checklist](http://bit.ly/torusQA)
  for the most real time updates on functionality.
---

# Changelog

## [v0.2.14](https://github.com/torusresearch/torus-website/pull/831)

* Integrated new inpage provider in torus-embed SDK

## [v0.2.13](https://github.com/torusresearch/torus-website/pull/801)

* DARK MODE EVERYWHERE
  * Now by default, when the user logs in and changes to the dark theme, it will be reflected on all pages viewed by the same user, including the login page as well as the logout pages.
* Language change UI + translations updated
* Re-Fetch provider quote on closing window
* Use new random-id to fix warnings related to build
* Add support for new inpage provider, improves compatibility with Metamask
  * The in-page provider has been upgraded to the latest specifications of EIP1193 to improve the compatibility with Metamask.
* Update packages dependencies affecting CircleCI builds
* Selected address support for payment tx
* USD tx amount fixes
  * Fixed bug where sending via USD bugged the UI
* Add LRC support
* Metamask controller upgrades + fixes
* Moonpay signature support
* Fix service-worker bugs
* Torus Embed button
  * DApps are now able to hide the Torus Embed button correctly should they choose to develop their own native integration of the Torus login. Developers can hide the default Torus button from the user with the following code:

## [v0.2.12](https://github.com/torusresearch/torus-website/pull/758)

* Start using torus.js npm package
* Start using fetch-node-details npm package
* Bug fixes \(transfer, activity pages\)
* Update packages
* Added locales
* New design for torus-embed login selector modal
* Lighthouse audit changes
* Calculations in bignumber.js instead of BN.js
  * And various other floating point fixes
* Store verifier details
* Payment provider updates
  * In previous versions, users could only use our Integrated FIAT On-Ramp Providers to add token funds to their Torus Wallet where they initiated the transaction from. From this version onwards, users are able to specify the ETH address other than their Torus Wallet to top-up with tokens.
  * DApps are now able to get Validations directly from the payment providers based on the limits set by the payment provider. The validations set will warn users who are using our Integrated FIAT On-Ramp Providers if they entered a number range beyond the sanctioned limited.
* Add LRC support \(alpha testnet\)
* Change autofill behaviour
* Tx Page mobile page bugfixes

## [v0.2.11](https://github.com/torusresearch/torus-website/pull/694)

* Service worker fixes
* Bug fixes

## [v0.2.10](https://github.com/torusresearch/torus-website/pull/652)

* Update packages
* Popup unblock
* Tx History table UI cleanup
* Common payment tx apis
* Metamask updates
* UI v8 for settings + history
* Bug fixes

## [v0.2.9](https://github.com/torusresearch/torus-website/pull/625)

* Update packages
* Support for cookies
* CI improvements

For older releases, go to [Github](https://github.com/torusresearch/torus-website/pulls?q=base%3Amaster)

