---
description: >-
  For updates, also checkout the release [QA checklist](http://bit.ly/torusQA)
  for the most real time updates on functionality.
---

# Changelog

## [v1.4.2](https://github.com/torusresearch/torus-website/pull/1093)

The following changes have been made in this release:

* Fix issue with dark mode redirect html

## [v1.4.1](https://github.com/torusresearch/torus-website/pull/1091)

The following changes have been made in this release:

* receive torus widget visibility status from embed
* Fix issues with whitelabel state in popups
* Allow dapp to re-request permission for user info

## [v1.4.0](https://github.com/torusresearch/torus-website/pull/1087)

The last release \(v1.3.5\) must've been a patch release

## [v1.3.5](https://github.com/torusresearch/torus-website/pull/1085)

The following changes have been made in this release:

* Add support for whitelabel solution \( theme, translations, logos etc\)
* Move widget and login modal to iframe
* Fixed issue with gasPrice being set 0 on custom networks
* Fixed issue with custom network support
* Update packages

## [v1.3.4](https://github.com/torusresearch/torus-website/pull/1073)

The following changes have been made in this release:

* Fix localStorage undefined issue for theme

## [v1.3.3](https://github.com/torusresearch/torus-website/pull/1071)

The following changes have been made in this release:

* Fix Issue with twitch api being deprecated

## [v1.3.2](https://github.com/torusresearch/torus-website/pull/1064)

The following changes have been made in this release:

* White label solution
* etherumjs related package updates
* Bug fixes
* Ramp Campaign changes
* Login action refactor

## [v1.3.1](https://github.com/torusresearch/torus-website/pull/1057)

The following changes have been made in this release:

* Xanpool Integration
* v8 changes
* Update packages

## [v1.3.0](https://github.com/torusresearch/torus-website/pull/983)

* Use webpack to build and release \(Fixed [blocknative/onboard\#219](https://github.com/blocknative/onboard/issues/219)\)
* Remove isMetamask=true \([Web3Modal/web3modal\#130](https://github.com/Web3Modal/web3modal/issues/130)\)
* Remove build scripts that are no longer necessary
* Update documentation
* Fixed bugs \([Web3Modal/web3modal\#138](https://github.com/Web3Modal/web3modal/issues/138)\)
* Update packages of fetch-node-details and torus.js
* Clean up scripts related to new torus-embed
* Hide dapp permission
* sendgrid use new email template
* Use browser language by default

## [v1.2.6](https://github.com/torusresearch/torus-website/pull/972)

* Fix issue with gas estimation
* Update packages

## [v1.2.5](https://github.com/torusresearch/torus-website/pull/969)

* CircleCI optimization
* Update packages
* Fix Ci scripts
* Show billboard always
* Fix issue with ramp ERC20 payments
* New Twitch API
* Lint fixes

## [v1.2.4](https://github.com/torusresearch/torus-website/pull/963)

* Refactor
* Billboard changes
* Fix lint
* Updated packages
* Bug fixes

## [v1.2.3](https://github.com/torusresearch/torus-website/pull/954)

* Window container max width
* Moonpay wallet address confirmation screen

## [v1.2.2](https://github.com/torusresearch/torus-website/pull/951)

* Payment provider changes
* ERC20 approve changes

## [v1.2.1](https://github.com/torusresearch/torus-website/pull/947)

* Allow topup API to be called without login
* Billboard changes

## [v1.2.0](https://github.com/torusresearch/torus-website/pull/934)

* Added better linting
* Add Ramp network payment provider
* CI Optimizations
* Bug fixes
* Update packages
* Add more tests
* Add more currencies

## [v1.1.0](https://github.com/torusresearch/torus-website/pull/904)

* Receive site metadata
* Remove Vuex store dependency in popups
* Fix timing issues with service worker popups
* Fix z-index issue with web3Connect
* New UI
* Bug fixes

## [v1.0.0](https://github.com/torusresearch/torus-website/pull/843)

* Launched out of beta

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

