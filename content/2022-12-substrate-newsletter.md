# sub0 recap ⏪ | Polkadot & Kusama Ecosystem Map Released 🗺️

This year’s edition of sub0, the first edition back in-person since the pandemic, was a huge success. Hundreds of new and veteran developers from the Polkadot developer community came together to connect, collaborate, and learn from more than 55 speakers. Throughout the conference, this quote from Bertrand Russell kept coming to mind:

_“The only thing that will redeem mankind is cooperation.”_

While we wait for the recordings of the sub0 talks to be released, make sure to check out the recaps on Twitter ([Day 1](https://twitter.com/Polkadot/status/1597317004905828352?utm_campaign=Parity%20Newsletter&utm_medium=email&_hsmi=237189384&_hsenc=p2ANqtz--luRdFgQNmf9lHCQCftRJ4h-pXxtrT07wTNJ3Z3gLuoRqQ2aQpxUp5Pt6LltsgRPIrpDM46MfaK9USc-ThwrGdveRQMg&utm_content=237189384&utm_source=hs_email), [Day 2](https://twitter.com/Polkadot/status/1597675261415526400?utm_campaign=Parity%20Newsletter&utm_medium=email&_hsmi=237189384&_hsenc=p2ANqtz-_7q46TWNg02sVi685yuBV1FN01Ftq3RObQbZnE-MHjSvJHH2atuU677JyBZF9WsIyNvTrHlDGzxjqREBRn9JVl8rJo8Q&utm_content=237189384&utm_source=hs_email)) and YouTube ([Day 1](https://www.youtube.com/watch?v=2MnrABFLxik&themeRefresh=1), [Day 2](https://www.youtube.com/watch?v=nk6qix6Br_k)).

## TL;DR and important announcements

* A new interactive Polkadot & Kusama Ecosystem Map made by SubWallet with support from Parity Technologies is now available at [Dotinsights](https://dotinsights.xyz), and features 540+ projects spanning 27 categories! Read the highlights in this [Twitter thread](https://twitter.com/dotinsights_xyz/status/1592489287773458432).

## 🔦 Community highlights

**Ecosystem builders** 

* t3rn, a smart contract hosting platform for fail-safe multichain executions, just released their [docs](https://docs.t3rn.io/intro)
* Astar Network has introduced dApp Staking Portal V2, which improves the user experience, staking information, and portal functionality, encouraging users to support developers through staking. [Read more here](https://medium.com/astar-network/our-dapp-staking-portal-v2-is-live-d4a1eba0563a).
* [Notifi launched on Acala](https://medium.com/acalanetwork/notifi-launches-on-acala-bringing-push-notifications-to-polkadot-defi-users-and-developers-b8d41d763319) bringing push notifications to Polkadot DeFi users and developers

**Polkadot Forum Digest**

* [Polkadot v0-9-33 release updates](https://forum.polkadot.network/t/polkadot-release-analysis-v0-9-33/1287) 
* [Meta: Convention Creation over Standardization](https://forum.polkadot.network/t/meta-convention-creation-over-standardization/1356/2)
* [Thoughts on governance security and configs for parachains](https://forum.polkadot.network/t/thoughts-on-governance-security-and-configs-for-parachains/1166)
* [Generalized multichain monitoring solution](https://forum.polkadot.network/t/generalized-multichain-monitoring-solution/1297/1)
* [Oracles for Polkadot](https://forum.polkadot.network/t/oracles-for-polkadot/1286)
* [Community suggestions and requests for the OpenGov model on Kusama](https://forum.polkadot.network/t/community-suggestions-and-requests-for-the-opengov-model-on-kusama/1179)
* [Multichain friendly account abstraction](https://forum.polkadot.network/t/multichain-friendly-account-abstraction/1298)
* [Generalized Storage Proofs](https://forum.polkadot.network/t/generalized-storage-proofs/1315)
* [ePBF contracts hackathon](https://forum.polkadot.network/t/ebpf-contracts-hackathon/1084)

**Learning**

* New material has been published in the Substrate docs:
    * [Transfer Assets with XCM](https://docs.substrate.io/tutorials/connect-relay-and-parachains/transfer-assets-with-xcm/) (tutorial)
    * [Open message passing channels](https://docs.substrate.io/tutorials/connect-relay-and-parachains/open-message-passing-channels/) (tutorial)
    * [Cross-consensus communication](https://docs.substrate.io/fundamentals/xcm-communication/) (doc)
* [Demystifying FRAME Macro Magic - Substrate Seminar](https://www.youtube.com/watch?v=aEWbZxNCH0A) (watch the full livestream)

If there’s anything you’d like to hear or learn about on Substrate Seminar, please [propose or request a topic](https://github.com/substrate-developer-hub/substrate-seminar/issues/new/choose), as we’re working on updating our calendar for the new year.

**📆 Upcoming events**

* Twitter space discussing the proposed DEX on Statemint ([December 14th](https://twitter.com/rphmeier/status/1600142343088222210))

## ☕️ Technical updates

**FRAME**

* Major improvements to the Uniques pallet, adding smart attributes to NFTs ([#12702](https://github.com/paritytech/substrate/pull/12702) and [#12736](https://github.com/paritytech/substrate/pull/12736))
* Added `with_weight` extrinsic to the Utility pallet to allow a root origin to specify the weight of the call ([#12848](https://github.com/paritytech/substrate/pull/12848))
* A major re-work of the Gilts pallet to now become NIS (non-interactive staking) pallet ([#12610](https://github.com/paritytech/substrate/pull/12610))
* Functionality added to allow other pallets to check asset ids ([#12666](https://github.com/paritytech/substrate/pull/12666))
* Added `EnsureWithSuccess` to FRAME system ([#12775](https://github.com/paritytech/substrate/pull/12775))
* Added `EnsureOriginOrHigherPrivilege `([#12844](https://github.com/paritytech/substrate/pull/12844))

## 👀 Releases

* [ink! 4.0-beta has been released](https://github.com/paritytech/ink/releases). It includes a stable ABI which will be used for ink! 4.0. Note that between now and the stable releases there will still be breaking code changes, but because of the stable ABI, deployed contracts will still be able to interact with each other. Start testing it and submit an issue if you encounter any problems! Read the [November ink! newsletter](https://use.ink/monthly-update/2022/11) for more updates
* New [node template](https://github.com/substrate-developer-hub/substrate-node-template) release, tagged to polkadot-v0.9.34

Visit [Polkadiff](https://polkadiff.parity.io/) for a full list of merged PRs into Substrate, Polkadot, and Cumulus since the last Polkadot release.

## 📰 Substrate jobs

Have a look at all the open roles in the ecosystem on the[Substrate Job Board](https://careers.substrate.io/jobs).

Got ideas for content you’d like to see in future newsletters? Make a PR to the next edition [here](https://github.com/substrate-developer-hub/newsletter/pulls) – we’d love to include them. ❤️