# April updates for Substrate and Polkadot devs ⚪️

Welcome to the April edition of the Substrate developer newsletter - the best place to discover the latest news from the Substrate and Polkadot community. We cover everything, from upcoming events and newly released learning material to technical updates for developers building with Substrate and FRAME. 

Don’t forget, the newsletter is open to community contributions, so if there’s any news you’d like to see featured, don’t hesitate: make a PR to the next edition [here](https://github.com/substrate-developer-hub/newsletter/pulls).

## ⭐TL;DR and important announcements

- Data collected by SubWallet & Dotinsights showed that Polkadot nomination pools [surpassed 3M DOT](https://twitter.com/dotinsights_xyz/status/1643240360578281472) in total stake with 8K+ pool members.
- The Web3 Foundation Grants Program achieved its [500 project milestone](https://twitter.com/dotinsights_xyz/status/1644281591727022080) by the end of Q1 2023.
- For a panoramic view of growth trends within the Polkadot ecosystem, check out [Polkadot Deep Dive Report Q1 2023](https://dotinsights.subwallet.app/polkadot-report-q1-2023-en/).
- Get your ink! Projects funded with [ink!ubator](https://use.ink/ubator/) which just launched this month.

## 📆 Upcoming events

- May 8-11: [Blockchain Week Rome](https://blockchainweekrome.com/polkadot-sponsor/) (ambassador-organised Polkadot side event)
- May 5: [Polkadot Bogotá Meetup](https://www.meetup.com/polkadot-and-kusama-bogota/events/292634750)
- May 11: [Polkadot Budapest Meetup](https://www.meetup.com/polkadot-hungary/events/292958136)
- May 17: [Polkadot Prague Meetup](https://www.meetup.com/polkadot-and-kusama-prague/events/293027585/)

## 🔦 Community highlights

- Co-organized by Parity & SubWallet as part of the DOTinVietnam event series with the participation of Moonbeam, Litentry, ArtZero, Gafi Network, MoonFit, StellaSwap, InvArch & Polkadot Insider - Beyond The Chain Vietnam 2023 has concluded successfully with 100+ builders & developers attending to learn Polkadot & Substrate. Check out the [highlight thread](https://twitter.com/dotinvietnam/status/1645351053116964864) & [highlight video](https://www.youtube.com/watch?v=kEm42m8vDJs). 

### ink!ubator launched this month!

<img src="https://use.ink/img/twitter/inkubator-twitter.png" />

* ink!ubator is an initiative funded by the Polkadot Treasury's Bounty Program. It is designed to kickstart the ink! ecosystem in the areas of developer growth, security audits, infrastructure, and high profile product launches. It offers grants, technical support from core developers, contract security audits, and much more. You can [apply to ink!ubator here](https://use.ink/ubator/) and follow updates on [Twitter](https://twitter.com/ink_lang).

### Blogs

* [XCM v3: Breaking New Ground for Web3 Interoperability](https://polkadot.network/blog/xcm-v3-breaking-new-ground-for-web3-interoperability/)
* [Polkadot Update: Q1 2023](https://polkadot.network/blog/polkadot-update-q1-2023/)
* [Saturn: The Future of Multi-Party Ownership](https://invarch.medium.com/saturn-the-future-of-multi-party-ownership-ac7190f86a7b)


## 🎓 Learning

- Watch the last Substrate Seminar: [Tuxedo: a UTXO alternative to FRAME](https://www.youtube.com/watch?v=6AY5VqXIAcM&list=PLOyWqupZ-WGsfgxkwTdMOwnbRW4nx_T-i&index=4) 
- Watch the latest [Polkadot Deep Dives](https://www.youtube.com/watch?v=6OduyxOwuxg&list=PLOyWqupZ-WGsfnlpkk0KWX3uS4yg6ZztG&index=1). This past month there’ve been deep dives about the Identity and Nicks pallets, FRAME Benchmarking, the Atomic Swap and Gilt pallets.
- Learn how to use ChatGPT to write and debug Smart Contracts on Moonbeam [in this video](https://www.youtube.com/watch?v=3_p2FCHTF3w).
- Learn about public credentials and AssetDIDs for NFTs on Kilt [video link](https://www.youtube.com/watch?v=ExVX9t9-EXU)
- RMRK's two EIPs have officially become ERC-5773 and ERC-6059, bringing standards to next generation NFTs in Web3. What is the new ERC-5773? Read [this thread](https://twitter.com/RmrkApp/status/1649796934821986305) by the RMRK team who developed it.

## ☕️ Technical updates

***In this edition, we’re experimenting with a new way to provide a digest of the latest updates to Substrate. If you have any feedback, please let us know by [opening an issue](https://github.com/substrate-developer-hub/newsletter/issues) – we welcome your input.***

_Here are note-worthy **runtime** PRs in the Substrate repo merged between 2023-04-01 and 2023-04-30._

### [#13851](https://github.com/paritytech/substrate/pull/13851) Fix fungible and fungibles set_balance return value

This PR fixes a bug in the calculation of the return value of the `fungible` and `fungibles` `set_balance` default implementation.

### [#13835](https://github.com/paritytech/substrate/pull/13835) `RemovePallet` migration utility struct

This PR adds a migration utility struct that allows easily removing pallet storage on the next runtime upgrade, useful for things like removing Gov V1 pallet storage after the switch to OpenGov.

### [#13798](https://github.com/paritytech/substrate/pull/13798) Uniform pallet warnings

This PR introduces [proc-macro-warning](https://github.com/ggwpez/proc-macro-warning) to emit a warning when using a hard-coded weight on a non-dev-mode pallet (https://github.com/paritytech/substrate/pull/13774).  
In cases where `dev` mode is not possible and you explicitly want to ignore this warning; wrap it in curly brackets like `{1}`.

### [#13779](https://github.com/paritytech/substrate/pull/13779) Add Freeze/Thaw events and tests

This PR adds a `Freeze` and `Thaw` event to the Balances pallet. Each respective event is emitted whenever some balance is frozen or thawed.

### [#13724](https://github.com/paritytech/substrate/pull/13724) Contracts: add sr25519_verify

This PR adds the ability to do sr25519 (schnorrkel) signature verification as part of the Contract pallet's core API.

### [#13722](https://github.com/paritytech/substrate/pull/13722) Implement #[pallet::composite_enum]

This PR adds a couple of new pallet parts: `FreezeReason`, `HoldReason`, `LockId` and `SlashReason`. The corresponding aggregate enums `RuntimeFreezeReason`, `RuntimeHoldReason`, `RuntimeLockId` and `RuntimeSlashReason` are also generated by `construct_runtime`. This is primarily used in pallets that wish to provide a reason for freezing funds, holding funds, locking funds and/or slashing funds in them. `#[pallet::composite_enum]` is also added as an attribute to put on top of an enum declared in a pallet module.

### [#13699](https://github.com/paritytech/substrate/pull/13699) Deprecate V1 Weights

This PR is part of the first round of cleanups to get completely rid of 1D weights.

### [#13610](https://github.com/paritytech/substrate/pull/13610) Refactor: inconsistent BalanceConversion fn

Fixes an inconsistent function naming for `BalanceConversion` trait: The `fn to_asset_balance` does not align with generics `InBalance` and `OutBalance` as `to_asset_balance` implies `OutBalance` to never be the native one.

### [#13302](https://github.com/paritytech/substrate/pull/13302) Metadata V15: Add Runtime API metadata

This PR collects the runtime API information for the metadata V15 and exposes the metadata under `metadata_at_version(u32::MAX)`. 

---

_Here are note-worthy **node** PRs in the Substrate repo merged between 2023-04-01 and 2023-04-30._

### [#13925](https://github.com/paritytech/substrate/pull/13925) sc-allocator: Do not panic on invalid header pointer

We should not panic on an invalid header pointer and instead return an error. It is possible that the application modifies the header pointer illegally, but then we should return an error instead of panicking.

### [#13824](https://github.com/paritytech/substrate/pull/13824) Make blocks per request configurable

Resolves https://github.com/paritytech/substrate/issues/10130

### [#13799](https://github.com/paritytech/substrate/pull/13799) Remove deprecated batch verification

This removes the deprecated batch verification. This was actually never really activated. Nevertheless, we need to keep the host functions around to support old runtimes which may import these host functions. However, we do not give access to these functions anymore. This means that any new runtime can not call them anymore. The host function implementations we keep will not do batch verification and will instead fall back to the always existing option of directly verifying the passed signature. `finish_batch_verification` will return the combined result of all the batch verify calls.

### [#13794](https://github.com/paritytech/substrate/pull/13794) Fix `try-runtime follow-chain`, try-runtime upgrade tuple tests, cli test utils

This PR fixes a bug with `follow-chain` and refactors existing node CLI test utility functions so that they may be used by other packages. 

### [#13769](https://github.com/paritytech/substrate/pull/13769) ProofRecorder: Implement transactional support

This implements transactional support for `ProofRecorder`. A transaction can be started with `start_transaction` and then later committed or rolled back. This is important for block producers to not include data from transactions that didn't make it to the block, because they e.g. panicked or similar. 

### [#13740](https://github.com/paritytech/substrate/pull/13740) Refactor(sc-executor): use wasm executor builder instead of old apis

This PR adds the `builder` style apis to create runtime executor and deprecates the old `new` api for executor.

## 👀 Releases

Go to [Polkadiff](https://polkadiff.parity.io/) for a full list of merged PRs into Substrate and Polkadot since the last Polkadot release and be sure to read the last Polkadot Release Analysis reports [on the Polkadot forum](https://forum.polkadot.network/tag/release-analysis). In this section, we go over updates to various core tools developed by Parity for the ecosystem.


### **Subxt ([v0.28.0](https://github.com/paritytech/subxt/releases/tag/v0.28.0)) 📫**

_A Rust library to submit extrinsics (transactions) to a Substrate node via RPC._

This release contains significant changes including: unifying the encoding and decoding of static and dynamic types, new CLI functionality and improvements to `DispatchError`.

### **Sidecar ([v15.0.0](https://github.com/paritytech/substrate-api-sidecar/releases)) 🚗**

_Sidecar is a REST service that makes it easy to interact with blockchain nodes built using Substrate's FRAME framework._

Notable changes include fixes for updates to Polkadot-JS and a bug fix related to `/blocks/head`.

## 📰 Substrate jobs

Have a look at all the open roles in the ecosystem on the [Substrate Job Board](https://careers.substrate.io/jobs).

Got ideas for content you’d like to see in future newsletters? Make a PR to the next edition [here](https://github.com/substrate-developer-hub/newsletter/pulls) – we’d love to include them. ❤️

_Previous editions of this newsletter are available in the public archive rendered on [this web page](https://substrate-developer-hub.github.io/newsletter/) as well as [on Polkaverse](https://polkaverse.com/10647). Join us there to comment, emote or provide feedback on our newsletters – all using a decentralised social media space built with Substrate and IPFS._
