# Register for edX courses on Web3, blockchain, and Polkadot 🧑‍🎓 | Discover Substrate news and resources 💻

Welcome to the November edition of the Substrate Developer newsletter.  Let’s dive right in with a quote from [Buckminster Fuller](https://en.wikipedia.org/wiki/Buckminster_Fuller):

_“You never change things by fighting the existing reality. To change something, build a new model that makes the existing model obsolete.”_

## ❗️TL;DR and important announcements:

* December 19 is the last day to sign up for the free Audit Track of edX's blockchain and Web3 courses. The currently available courses are an [Introduction to Polkadot](https://www.edx.org/course/introduction-to-polkadot) and an [Introduction to Blockchain and Web3](https://www.edx.org/course/introduction-to-blockchain-and-web3) 
* Try out some new tutorials to guide you through [opening HRMP channels](https://hackmd.io/@brunopgalvao/B1PO5yUQo), [launching a testnet with Zombienet](https://hackmd.io/kSFS2ButRESeJ7hu_iKKoA?view), [rolling back parachain state](https://hackmd.io/3BAy3HEzRVO2sBFnUaBVKA) and [adding a custom RPC](https://hackmd.io/JpJCbu0nTa2jym0za1Tggw)
* Learn more details about the Polkadot and Kusama release notes in the [dedicated forum post](https://forum.polkadot.network/t/polkadot-release-analysis/1026/2)

## 🔦 Community highlights

* Substrate Seminar will be streaming on Twitch going forward, on the brand new [PolkadotDev channel](https://www.twitch.tv/polkadotdev) (still in beta for now). Subscribe to stay updated on all the great content we have in the pipeline. You can also easily add all the upcoming seminars to your calendar by subscribing to the [Seminar calendar](https://calendar.google.com/calendar/u/0?cid=Y192cXBsamk3cXY2ajBvcDVrbmdwMGR0cjUzc0Bncm91cC5jYWxlbmRhci5nb29nbGUuY29t).
There are ongoing discussions to rename Substrate Seminar to something more general. Please join the discussion [here](https://github.com/substrate-developer-hub/substrate-seminar/discussions).

* [Anagolay](https://anagolay.network/) has built a [Web3 API Auth Token (WAAT) library](https://github.com/kelp-hq/oss/tree/22f85a75887ddcf65fe411e008f9bc7ba2d3203f/tools/web3-api-auth-token) that can be used for authorising user interactions with dApps or wallets, as well as for verifying data integrity in information exchange. Learn more [here](https://github.com/kelp-hq/oss/tree/22f85a75887ddcf65fe411e008f9bc7ba2d3203f/tools/web3-api-auth-token#why-we-should-use-waat).

* [Helikon Labs](https://helikon.io) have released the alpha version of [ChainSynth](https://alpha.chainsynth.app), a first step in the creation of a generative audio-visual synthesizer that works with real-time blockchain data. The source code and more information can be found in the project [repository](https://github.com/helikon-labs/chainsynth).

* [Read all of last month's updates from ink!](https://use.ink/monthly-update/2022/10), the smart contract language for the Polkadot network. 

* Check out these new tutorials by members of Parity’s support engineering team:
    - [Opening HRMP Channels](https://hackmd.io/@brunopgalvao/B1PO5yUQo)
    - [Setting Up a Local Testnet using Zombienet](https://hackmd.io/kSFS2ButRESeJ7hu_iKKoA?view)
    - [Parachain State Rollback](https://hackmd.io/3BAy3HEzRVO2sBFnUaBVKA)
    - [Adding a Custom RPC](https://hackmd.io/JpJCbu0nTa2jym0za1Tggw)

## 📆 Upcoming events

* Zero Knowledge Validator will host a session discussing Privacy on Moonbeam on December 14th (RSVP [here](https://hopin.com/events/privacy-on-moonbeam-311978ec-1ac3-4f44-9e57-86c3c3712f3b))
* Sub0, the Polkadot Developer Conference, is happening November 28 and 29 in Lisbon (view the program [here](https://sub0.polkadot.network/program/))
 
## ☕️ Technical updates

### General

* Rococo’s runtime has been upgraded to v9310 and is now closer to Kusama’s, offering even more possibilities to builders. The breaking changes involve the reordering of pallet indices which affects the encoding of calls. Make sure to verify that the implementations and tools you’re working with aren’t affected by these changes and read the [PR](https://github.com/paritytech/polkadot/pull/5617) for a detailed overview of the changes
* The Rockmine endpoint (previously `wss://rococo-statemint-rpc.polkadot.io`) has been updated to `wss://rococo-rockmine-rpc.polkadot.io`
* One of the Polkadot core engineers has published a [forum post](https://forum.polkadot.network/t/testing-complex-frame-pallets-discussion-tools/356/1) on the different runtime testing tools available. If you have feedback on any of the mentioned tools or would like to share your own tools and experience, please chime in!

### FRAME

* A new [signed extension](https://docs.substrate.io/reference/transaction-format/#signed-extensions) was added to the [Sudo pallet](https://paritytech.github.io/substrate/master/pallet_sudo/index.html) called `CheckOnlySudoAccount`. It ensures that only transactions signed by the sudo account are accepted by the transaction pool – useful for chains going live that want to avoid transaction spamming ([#12496](https://github.com/paritytech/substrate/pull/12496)).
* A new defensive trait has been added to `frame_support` called `DefensiveTruncateFrom`. It truncates a vec so that it satisfies the bound when passed into a `BoundedVec` ([#12515](https://github.com/paritytech/substrate/pull/12515)).
* A new attribute was added to the pallet macro which enables developers to compile pallets in dev mode. When specified in a pallet using `#[pallet(dev_mode)]`, the macro sets weights to 0 if they aren’t specified and automatically sets a default `MaxEncodedLen` if it isn’t already set. Please note that this feature is meant for development only, production code will not compile with this attribute. This provides a major improvement for the FRAME developer experience ([#12536](https://github.com/paritytech/substrate/pull/12536)).

### Substrate Node

* Updates to the runtime API for querying payment info to make it compatible with runtimes using weights V1 and V2 ([#12633](https://github.com/paritytech/substrate/pull/12633))

## 👀 Releases

Visit [Polkadiff](https://polkadiff.parity.io/) for a full list of merged PRs into Substrate, Polkadot and Cumulus since the last Polkadot release. For more information on the upcoming Polkadot and Kusama releases, check out [this post](https://forum.polkadot.network/t/polkadot-release-analysis/1026/2) from the Polkadot forum.
 
## 📰 Substrate jobs

Have a look at all the open roles in the ecosystem on the [Substrate Job Board](https://careers.substrate.io/jobs).

Got ideas for content you’d like to see in future newsletters? Make a PR to the next edition [here](https://github.com/substrate-developer-hub/newsletter/pulls) – we’d love to include them. ❤️
