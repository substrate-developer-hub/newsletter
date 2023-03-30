# ETHDenver Talks Published 📺 | Learn ink! 4.0 tools  🦑| FRAME pallet highlights 🖼 

Welcome to the March edition of the Substrate developer newsletter - the best place to discover the latest news from the Substrate and Polkadot community. We cover everything, from upcoming events and newly released learning material to technical updates for developers building with Substrate and FRAME. 

Don’t forget, the newsletter is open to community contributions, so if there’s any news you’d like to see featured, don’t hesitate: make a PR to the next edition here.

## ⭐TL;DR and important announcements

- The Call for Proposals for Polkadot Decoded 2023 is open until March 29. Don’t miss out on the chance to present your ideas, tech, or live project to an audience of thousands of Polkadot community members, industry professionals, and blockchain enthusiasts. Submit your proposal [here](https://eventreg.polkadot.network/decoded2023/proposals/Start).
- The Substrate documentation team is looking for your input. Please take a second to fill out [this survey](https://forms.gle/UXmM6XnoDSQxKK8L8) to help improve our documentation portal.
- Check out the recently published [Polkadot Staking Review: Impressive Stats, What’s New & What’s Coming](https://polkadot.network/blog/polkadot-staking-review-impressive-stats-whats-new-whats-coming).
- Don't know where to start with ink!? Check out this [ink! 101 thread](https://twitter.com/dotinsights_xyz/status/1635594705357660161) by SubWallet & Dotinsights.

## 📆 Upcoming events

 - Make sure you tune in to SubWallet & Dotinsights' [Twitter Space](https://twitter.com/dotinsights_xyz/status/1635293893205065730) on ink! 4.0 and WASM Smart Contracts Bounty at 2PM UTC on March 16! Featuring speakers from Parity, Astar Network, Aleph Zero, Brushfam and ArtZero.
 - DotSafari (Kenya, March 30 - April 1st): a bootcamp, hackathon and conference organized by SafariDAO. More details on [their website](https://dotsafari.xyz/).
 - ink! Berlin Community Meetup (Berlin, March 30th) hosted by Parity Technologies & Scio Labs. Rsvp [here](https://www.meetup.com/parity/events/292157078/).
- Build with Polkadot (Hong Kong, April 11th) hosted by Polkaworld, Parity Technologies and One Block. Learn more [here](https://twitter.com/polkaworld_org/status/1636272941825671173).
- Polkadot Bled Mini-Conference: Unraveling the Future of Web3 (Bled, Slovenia, April 29) hosted by PolkadotBled. RSVP [here](https://www.meetup.com/subwork/events/292274713/).

## 🔦 Community highlights

**Learn about what’s being built and discover new educational material from the Substrate and Polkadot community. Working on something you’d like to share here? This newsletter is [open for contributions](https://github.com/substrate-developer-hub/newsletter#-prs-for-next-issue-are-now-being-accepted) – make a PR to the next edition of the newsletter.**

- Learn the latest on Aleph Zero in this 101 thread by SubWallet & Dotinsights
- Polkadot Now has just been announced, taking place April 1 - 2, 2023 in Bangalore, India. Get the latest updates here.
* Catch Shawn Tabrizi's talk at ETHDenver 2023 on [What is Shared Security?](https://www.youtube.com/watch?v=uKQOSPfM-W0)
- Catch Polkadot founder Robert Habermeier’s [talk about Polkadot Blockspace](https://www.youtube.com/watch?v=KRAU2MyWhao) at ETHDenver 2023
- Watch the replay of [Astar Network’s Astar Tech Talk #007](https://www.crowdcast.io/c/mx8d7yw0629i), on creating Wasm dApps using UI tools and contract ink! Code.
- Learn about Astar.js - the UI developer tool for Wasm contract developers – [in this Twitter thread](https://twitter.com/AstarNetwork/status/1620487582634364928).

## 🎓 Learning

 - Read a [blog post](https://brightinventions.pl/blog/zk-snarks-in-substrate-part-1/) about ZK-Snarks in Substrate.
 - Make sure to check out the [latest Deep Dives](https://www.youtube.com/watch?v=7DZwVXzi9x0&list=PLOyWqupZ-WGsfnlpkk0KWX3uS4yg6ZztG) covering everything you need to know about launching a parachain.
- Learn about developing a dapp in ink! 4.0 using Brushfam in the [latest Substrate Seminar](https://www.youtube.com/watch?v=lCToPcLCQgQ&list=PLOyWqupZ-WGsfgxkwTdMOwnbRW4nx_T-i&index=3). 
- Read [this blog](https://polkaworld.medium.com/xcm-v3-is-coming-soon-what-new-possibilities-will-it-bring-to-polkadot-ecosystem-c4ed740b1fff) post to learn about what new possibilities XCM v3 can bring to the ecosystem 
- Robert Habemeier shared his slides from the Shared Security Summit [as a tweet thread](https://twitter.com/rphmeier/status/1631467728555974658?s=51&t=Yb-S2fsBC8Vtd0t5dn3XTQ), covering blockspace fundamentals, trade-offs in different architectures, and some roadmap items for Polkadot based off of this mental model.

As always, a reminder to [propose or request a topic](https://github.com/substrate-developer-hub/substrate-seminar/issues/new/choose) you’d like to see on Substrate Seminar and chime in to [this forum post to request a Deep Dive release](https://forum.polkadot.network/t/polkadot-deep-dives-series/1708).📺

## ☕️ Technical updates

***In this edition, we’re experimenting with a new way to provide a digest of the latest updates to Substrate. If you have any feedback, please let us know by [opening an issue](https://github.com/substrate-developer-hub/newsletter/issues) – we welcome your input.***

The updates highlighted below are PRs that have been merged into Substrate which contain the **B1-note_worthy** label and are likely relevant to most builders. Please have a look at the [full list of PRs on GitHub](https://github.com/paritytech/substrate/pulls?page=1&q=is%3Apr+is%3Aclosed+label%3AB1-note_worthy) to get more details on them and to go through others not included in this section.

**FRAME: Fix the Referenda confirming alarm #13704**

We were doing a straight `mul` to get the block number from a `Perbill`, which will round down if the fractional part is half or less. We should always be rounding up, though, to ensure that when the alarm goes off the confirmation period is definitely ready to begin.

**Assets pallet: Giving the asset owner the ability to set minimum balance #13486**

Introduces a new extrinsic `set_min_balance` which allows the owner of the specific asset to change the `min_balance` required for an asset.

**Metadata V15: Expose pallet documentation #13452**

This patch captures the pallet documentation declared on the pallet module.
The documentation added to this pallet is later on included in the runtime metadata.

**Add `defensive_assert!` macro #13423**

Similar to [`assert!`] but will print an error without `debug_assertions` instead of silently ignoring it. 

**Salary pallet #13378**

Introduce a new pallet and associated traits which allows a chain to configure autonomous payments to members of a ranked collective.

**Return account's asset balances #13352**

This method solves the problem of fetching the account's asset balances. Now, instead of sending 100+ RPC requests it would be possible to send just one.

**Pallet dispatchable+storage doc module. #13341**

The goal of this PR is to make docs for dispatchables and storages on pallets more accessible and discoverable when browsing the generated docs. The PR accomplishes this by adding two auto-generated modules to all pallets: dispatchables and `storage_types`. These modules are only produced when building docs and otherwise do not exist or interfere with pallets. The `storage_types` module is auto-populated with documented structs representing each storage type from the parent pallet. The dispatchables module is auto-populated with uncallable auto-generated functions matching the signature of each `Call` variant. Right now a link to the corresponding `Call` enum variant is also included, though this may be removed. A note is included specifying that these cannot be called and are doc-only.

**Metadata V15: Expose API to fetch metadata for version #13287**

This PR extends the Metadata API to fetch the metadata at a given provided version.

It lays the foundation for keeping the metadata V14 around and exposing the V15 for early adopters before making a major breaking change.

**[NFTs] Offchain mint #13158**

This PR adds a new way of minting NFTs with pre-signed data.

As the collection's owner, you can pre-sign a mint data and pass the signature to the end-user, who would submit it on-chain. The item's mint and metadata/attributes deposits will be taken from the end user.

In the mint data, it's possible to set the metadata and attributes for the item, set the deadline for signature and whitelist the origin.

## **👀 Releases**

Go to [Polkadiff](https://polkadiff.parity.io/) for a full list of merged PRs into Substrate and Polkadot since the last Polkadot release and be sure to read the last Polkadot Release Analysis reports [on the Polkadot forum](https://forum.polkadot.network/tag/release-analysis). In this section, we go over updates to various core tools developed by Parity for the ecosystem.


### **Subxt ([v0.27.1](https://github.com/paritytech/subxt/releases/tag/v0.27.1)) 📫**

_A Rust library to submit extrinsics (transactions) to a Substrate node via RPC._

Notable updates includes adding find_last for block types events.


### **Sidecar ([v14.5.0](https://github.com/paritytech/substrate-api-sidecar/releases/tag/v14.5.0)) 🚗**

_Sidecar is a REST service that makes it easy to interact with blockchain nodes built using Substrate's FRAME framework._

Notable features added in this release include adding endpoints for pallets/dispatchables and pallets/consts.


### **Zombienet ([v1.3.4](https://github.com/paritytech/zombienet/releases/tag/v1.3.40)) 🧟**

_Currently under active development, Zombienet is a CLI tool to easily spawn ephemeral parachain networks and perform tests against them._

Make sure to update to this latest version if you want to use the newest features.

## 📰 Substrate jobs

Have a look at all the open roles in the ecosystem on the [Substrate Job Board](https://careers.substrate.io/jobs).

Got ideas for content you’d like to see in future newsletters? Make a PR to the next edition [here](https://github.com/substrate-developer-hub/newsletter/pulls) – we’d love to include them. ❤️

_Previous editions of this newsletter are available in the public archive rendered on [this web page](https://substrate-developer-hub.github.io/newsletter/) as well as [on Polkaverse](https://polkaverse.com/10647). Join us there to comment, emote or provide feedback on our newsletters – all using a decentralised social media space built with Substrate and IPFS._
