$edition
$title

## TL;DR and important announcements

## 🔦 Community highlights

* Substrate Seminar will be streaming on Twitch going forward, under the brand new [PolkadotDev channel](https://www.twitch.tv/polkadotdev). Subscribe so you can stay updated on new content series in the pipeline. There are also ongoing discussions to rename Seminar to something more general. Please join the discussion [here](https://github.com/substrate-developer-hub/substrate-seminar/discussions/31).

* [Anagolay](https://anagolay.network/) has built a [Web3 API Auth Token (WAAT) library](https://github.com/kelp-hq/oss/tree/22f85a75887ddcf65fe411e008f9bc7ba2d3203f/tools/web3-api-auth-token) which allows the secure transmission of information between two parties using a base64Url encoded JSON object.
WAAT can be used for for authorization and informational exchange, learn more [here](https://github.com/kelp-hq/oss/tree/22f85a75887ddcf65fe411e008f9bc7ba2d3203f/tools/web3-api-auth-token#why-we-should-use-waat).

* [Helikon Labs](https://helikon.io) have released the alpha version of [ChainSynth](https://alpha.chainsynth.app), a first step in the creation of a generative audio-visual synthesizer that works with real-time blockchain data. Source code and more information can be found in the project [repository](https://github.com/helikon-labs/chainsynth).
 
 * Check out last month's updates from [ink!](https://use.ink/monthly-update/2022/10)
## 📆 Upcoming events

* Zero Knowledge Validator will host a session on Privacy on Moonbeam December 14th (RSVP [here](https://hopin.com/events/privacy-on-moonbeam-311978ec-1ac3-4f44-9e57-86c3c3712f3b)).
* Sub0 happening November 28 and 29 in Lisbon (view the program [here](https://sub0.polkadot.network/program/))

## ☕️ Technical updates

### General

* Rococo’s runtime has been upgraded and is now closer to Kusama’s runtime, so that it can offer even more possibilities to builders. The breaking changes have to do with the reordering of pallet indices which affects the encoding of calls. Verify that the implementations and tools you’re working with aren’t affected by these changes. Read [the PR](https://github.com/paritytech/polkadot/pull/5617) to learn more about the changes in more detail.

* The Rockmine endpoint (previously wss://rococo-statemint-rpc.polkadot.io) has been updated to wss://rococo-rockmine-rpc.polkadot.io

* Polkadot core engineer writes about the different runtime testing tools available in [this forum post](https://forum.polkadot.network/t/testing-complex-frame-pallets-discussion-tools/356/2). If you have feedback on any of the mentioned tools or ones you’d like to mention, please share!

### FRAME

* A new signed extension was added to the Sudo pallet called `CheckOnlySudoAccount`. It ensures that only transactions signed by the sudo account are accepted by the transaction pool – useful for chains going live that want to avoid transaction spamming ([#12496](https://github.com/paritytech/substrate/pull/12496)).
* A new defensive trait has been added to `frame_support` called `DefensiveTruncateFrom`. It truncates a vec so that it satisfies the bound when passed into a BoundeVec ([#12515](https://github.com/paritytech/substrate/pull/12515)).

* A new attribute is added to the pallet macro which enables developers to compile pallets in dev mode. When specified in a pallet using `#[pallet(dev_mode)]`, the macro sets weights to 0 if they aren’t specified and automatically sets a default `MaxEncodedLen` if it isn’t already set. This provides a major improvement for the FRAME developer experience ([#12536](https://github.com/paritytech/substrate/pull/12536)).

Go to [Polkadiff](https://polkadiff.parity.io/) for a full list of merged PRs into Substrate, Polkadot and Cumulus since the last Polkadot release.

## 👀 Releases

## 📰 Substrate jobs

Have a look at all the open roles in the ecosystem on the [Substrate Job Board](https://careers.substrate.io/jobs).
Got ideas for content you’d like to see in future newsletters? [Contribute](https://github.com/substrate-developer-hub/newsletter/pulls) to the next edition – we’d love to hear them. ❤️
