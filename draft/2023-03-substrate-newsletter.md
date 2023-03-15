## ⭐TL;DR and important announcements
- Don't know where to start with ink!? Check out this ink! 101 [thread]([url](https://twitter.com/dotinsights_xyz/status/1635594705357660161)) by SubWallet & Dotinsights.

## 🔦 Community highlights
- Learn the latest on Aleph Zero through the [101 thread]([url](https://twitter.com/dotinsights_xyz/status/1630886296108556289)) by SubWallet & Dotinsights.
 
## 📆 Upcoming events
 - Make sure you tune in to SubWallet & Dotinsights' [Twitter Space]([url](https://twitter.com/dotinsights_xyz/status/1635293893205065730)) on ink! 4.0 and WASM Smart Contracts Bounty at 2PM UTC on March 16! Featuring speakers from Parity, Astar Network, Aleph Zero, Brushfam and ArtZero.
## ☕️ Technical updates

### From parachain teams

* Join Astar Network’s upcoming Crowdcast for [Astar Tech Talk #007](https://twitter.com/AstarNetwork/status/1632214374990630917), creating Wasm dApps using necessary UI tools such as typescript and contract Ink! code.

* Learn how to use [Astar.js](https://twitter.com/AstarNetwork/status/1620487582634364928)–a powerful dev tool to build dApps on Astar Network.

### From Substrate

The updates highlighted below are PRs that have been merged into Substrate which contain the `B1-note_worthy` label and are likely relevant to most builders. Please have a look at the [full list of PRs on GitHub](https://github.com/paritytech/substrate/pulls?page=1&q=is%3Apr+is%3Aclosed+label%3AB1-note_worthy) to get more details on them and to go through others not included in this section.

* **<span style="text-decoration:underline;">Assets pallet: Giving the asset owner the ability to set minimum balance #13486</span>**: Introduces a new extrinsic set_min_balance which allows the owner of the specific asset to change the min_balance required for an asset.

* **<span style="text-decoration:underline;">Metadata V15: Expose pallet documentation #13452</span>**: This patch captures the pallet documentation declared on the pallet module. The documentation added to this pallet is later on included in the runtime metadata.

* **<span style="text-decoration:underline;">Add defensive_assert! macro #13423</span>**: similar to [`assert!`] but will print an error without `debug_assertions` instead of silently ignoring it.

* **<span style="text-decoration:underline;">Salary pallet #13378</span>**: Introduce a new pallet and associated traits which allows a chain to configure autonomous payments to members of a ranked collective.

* **<span style="text-decoration:underline;">Return account's asset balances #13352</span>**: This method solves the problem of fetching the account's asset balances, now instead of sending 100+ RPC requests it would be possible to send just one.

* **<span style="text-decoration:underline;">pallet-timestamp: Remove ValidAtTimestamp error variant #13346</span>**: The error variant wasn't that useful and it was also used wrongly in the code. In the code we returned this variant when the `timestamp &lt; minimum`. The problem of this is that we waited on the node side some time, but then `set` function rejects the timestamp because of the same check (the timestamp in the block stays the same). We ensure that the timestamp isn't drifting too much in the future, but waiting for the timestamp to be "valid" would open some attack vector. The consensus protocols also compare the slots in the blocks to ensure that there isn't a block from the future and in the runtime we then ensure that `slot = timestamp / slot_duration`. So, we can just remove this variant and replace it with a new variant `TimeBetweenBlocksTooShort` to not even try importing a block which uses a too short delay since the last block.

* **<span style="text-decoration:underline;">Pallet dispatchable+storage doc module. #13341</span>**: The goal of this PR is to make docs for dispatchables and storages on pallets more accessible and discoverable when browsing the generated docs. The PR accomplishes this by adding two auto-generated modules to all pallets: dispatchables and storage_types. These modules are only produced when building docs and otherwise do not exist or interfere with pallets. The storage_types module is auto-populated with documented structs representing each storage type from the parent pallet. The dispatchables module is auto-populated with uncallable auto-generated functions matching the signature of each Call variant. Right now a link to the corresponding Call enum variant is also included, though this may be removed. A note is included specifying that these cannot be called and are doc-only.

* **<span style="text-decoration:underline;">Metadata V15: Expose API to fetch metadata for version #13287</span>**: This PR extends the Metadata API to fetch the metadata at a given provided version. It lays the foundation for keeping the metadata V14 around and exposing the V15 for early adopters before making a major breaking change.

* **<span style="text-decoration:underline;">[NFTs] Offchain mint #13158</span>**: This PR adds a new way of minting NFTs with pre-signed data. As the collection's owner, you can per-sign a mint data and pass the signature to the end-user, who would submit it on-chain. The item's mint and metadata/attributes deposits will be taken from the end user. In the mint data, it's possible to set the metadata and attributes for the item, set the deadline for signature and whitelist the origin.

## 👀 Releases

## 📰 Substrate jobs

Have a look at all the open roles in the ecosystem on the [Substrate Job Board](https://careers.substrate.io/jobs).

Got ideas for content you’d like to see in future newsletters? Make a PR to the next edition [here](https://github.com/substrate-developer-hub/newsletter/pulls) – we’d love to include them. ❤️

_Previous editions of this newsletter are available in the public archive rendered on [this web page](https://substrate-developer-hub.github.io/newsletter/) as well as [on Polkaverse](https://polkaverse.com/10647). Join us there to comment, emote or provide feedback on our newsletters – all using a decentralised social media space built with Substrate and IPFS._
