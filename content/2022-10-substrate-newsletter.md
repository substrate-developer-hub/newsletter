# Last day to register for Sub0 📝  | Polkadot Fellowship Manifesto released 📘

[Sub0, the Polkadot Developer Conference](https://sub0.polkadot.network/) is almost here! You can now [check out the full program](https://sub0.polkadot.network/program/) and find out exactly what to expect in Lisbon on November 28-29. Besides interesting keynotes, panel discussions, and interactive workshops, this year’s edition of Sub0 also offers attendees a variety of ways to get personally involved, including:

* A Demo Area, where you can showcase your current projects and products to the Sub0 audience. Designated tables for this will be granted on a first come, first serve basis upon check-in at the event.

* Barcamp Talks, allowing you to put your ideas forward for open forum discussions in a designated networking space. Submissions will be voted on by attendees, with the winners invited on stage to chair the discussions.  

**Registration closes today, so make sure you [apply as soon as possible](https://sub0.polkadot.network/register/).**

Before diving in to the rest of our updates, let’s kick things off with a quote from the legendary Edsger W. Dijkstra: 

_“The purpose of abstracting is not to be vague, but to create a new semantic level in which one can be absolutely precise.”_

## ❗️TL;DR and important announcements:

* You can now [contribute](https://github.com/substrate-developer-hub/newsletter) to future editions of the Substrate Developer Newsletter.

* **The [Polkadot Fellowship manifesto](https://github.com/polkadot-fellows/manifesto/blob/main/manifesto.pdf) has been released**, along with an open call for Polkadot core developers to join the fellowship. Learn how to get involved [here](https://forum.polkadot.network/t/calling-polkadot-core-developers/506).

* There have been several notable renaming improvements in Substrate’s codebase and steady progress is being made towards using weights V2.

## 🔦 Community highlights

* We want to start including news that you may have to share, so we’re opening up the Substrate Developer’s Newsletter for contributions. Check out [the repository](https://github.com/substrate-developer-hub/newsletter) to learn how you can propose content for future editions.

* Interested in joining the next [Polkadot Devcamp](https://medium.com/polkadot-network/polkadot-devcamp-intake-2-ddebc5fb9096)? [Apply](https://airtable.com/shrx5D6x050LJKHzD) before October 23rd.

* Moonbeam has introduced the [XCM SDK](https://moonbeam.network/announcements/xcm-sdk/), a tool that makes cross-chain interoperability more accessible to developers on Moonbeam and other parachains on Kusama and Polkadot.

* Check out this new [Patricia merkle trie verifier in Rust](https://github.com/ComposableFi/patricia-merkle-trie) that supports `no_std`. It allows you to verify Ethereum style merkle patricia proofs as specified in [this document](https://ethereum.github.io/execution-specs/autoapi/ethereum/frontier/trie/index.html).
The Integritee SDK has been released. Use it to build out your TEE applications on Polkadot.
Read updates from the ink! newsletter here.

## 📆 Upcoming events

* [Polkadot Meetup Slovenia](https://www.meetup.com/polkadot-ljubljana/events/288769487/) (Thursday, Oct. 13th, Ljubljana)

* [Dot in Vietnam](https://docs.google.com/forms/d/e/1FAIpQLSeclczNvMal-T6MKBJqXhG1duQTOjkAqEpaaaQQtEqu28Jmgg/viewform), read the full announcement [here](https://blog.subwallet.app/press-release-first-polkadot-meetup-taking-place-in-hanoi-on-october-18-bb8a3ab11d80). (Tuesday, Oct. 18th, Hanoi). 

* [Astar Tech Talk: Using Covalent to analyze on-chain data](https://www.crowdcast.io/e/astar-tech-talk-001-covalent) (Tuesday, Oct. 18, Online)

* [Beyond the chain: Breaking into blockchain](https://www.eventbrite.com/e/beyond-the-chain-getting-a-job-in-web3-tickets-435604363377) (Thursday, Oct. 20th, Berlin)

* [Beyond the Chain: Getting a job in Web3](https://www.eventbrite.com/e/beyond-the-chain-getting-a-job-in-web3-tickets-435604363377) (Thursday, Oct. 20th, London) 
Polkadot Summit (Thursday, Nov. 3rd, San Francisco)
 
## ☕️ Technical updates

* Benchmarking for XCM on Statemine/t will significantly bring down fees (approx. 10x cheaper)

* Renaming PRs for `RuntimeOrigin`, `RuntimeCall` and `RuntimeEvent` have been merged ([#12258](https://github.com/paritytech/substrate/pull/12258), [#11981](https://github.com/paritytech/substrate/pull/11981))

* Anonymous proxy has been rename to pure proxy ([#12283](https://github.com/paritytech/substrate/pull/12283))

* Migration is required after adding the ability to do fixed point math on balances for making storage deposits resistant against changing deposit prices ([#12083](https://github.com/paritytech/substrate/pull/12083))

* A new `pay_tips` method has been added to the Uniques pallet ([#12168](https://github.com/paritytech/substrate/pull/12168))

* A new `sp-weights` crate ([#12219](https://github.com/paritytech/substrate/pull/12219)) and a storage size component ([#12277](https://github.com/paritytech/substrate/pull/12277)) have been added as part of the preparations for rolling out Weights V2

* Go to [Polkadiff](https://polkadiff.parity.io/) for a full list of merged PRs since the last Polkadot release.

## 👀 Releases

* Polkadot ([v0.9.29](https://github.com/paritytech/polkadot/releases/tag/v0.9.29)): no major changes.

* TxWrapper Core ([v4.0.1](https://github.com/paritytech/txwrapper-core/releases/tag/v4.0.1)): minor bug fix.

* Substrate Sidecar API ([v14.0.0](https://github.com/paritytech/substrate-api-sidecar/releases/tag/v14.0.0)): now supports NStorageMaps 

* Subxt ([v24.0.0](https://github.com/paritytech/subxt/releases/tag/v0.24.0)): jsonrpsee can be an optional dependency, which opens the door to integrating Subxt into light clients. A "runtime upgrade" API is exposed, giving more visibility into when node updates happen in case your application needs to handle them.

* Polkadot JS API ([v9.5.1](https://github.com/polkadot-js/api/releases/tag/v9.5.1)): new changes and additions to adapt to Weight V2.

## 📰 Substrate jobs

Check out all the open roles in the ecosystem on the [Substrate Job Board](https://careers.substrate.io/jobs).

Got ideas for content you’d like to see in future newsletters? Make a PR for the next edition [here](https://github.com/substrate-developer-hub/newsletter/pulls) – we’d love to include them. ❤️