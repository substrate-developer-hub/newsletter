## ⭐TL;DR and important announcements

## 📆 Upcoming events

## 🔦 Community highlights

### Trace APIs from OnFinality

OnFinality adds support for tracing and storage subscription RPC APIs to our Enhanced API service. Trace API is an application programming interface that allows developers to monitor and “trace” the history of what was executed on-chain in a given block. It captures and records vital information otherwise not available through regular RPC methods and extrinsics (such as complete XCM transfer records and complete list of balance changes). This kind of API is required for developers to fully analyse and inspect XCM events on chain.

OnFinality has launched beta support and is rolling this out to all supported parachains (over 40 of them) in the coming days. [Read more here](https://blog.onfinality.io/onfinality-launches-trace-api-for-unprecedented-visibility-into-your-dapps/).

## 🎓 Learning
 
 * Learn how to make your own NFT collection in minutes on Moonbeam using Apillon in this [blog post](https://blog.apillon.io/make-your-own-nft-collection-in-minutes-brought-to-moonbeam-by-apillon-538fdf34fc5)

## ☕️ Technical updates

Here are note-worthy **runtime** PRs in Substrate repo merged between 2023-05-01 and 2023-05-23.

### [#14191](https://github.com/paritytech/substrate/pull/14191) TrieCache: Fine tune the size of the local and node cache

First, we increase the size to 10MiB for the local cache. Second, we give the node cache a bigger max size than the value cache, see the changed comment on why.

In general this should ensure that we are able to cache the `:code` and not directly throw it out of the cache because it is too big (which currently happens when the size of the runtime > 2MiB). In the future this should be improved to ensure that certain values are not removed from the cache at all, like `:code`.




---

### [#14190](https://github.com/paritytech/substrate/pull/14190) WarpSync: Show number of required peers in informant

This makes it for the user more obvious on what we are waiting and not just "waiting for peers".



---

### [#14183](https://github.com/paritytech/substrate/pull/14183) FRAME: Allow message ID to be mutated in `ProcessMessage`

Polkadot Companion: https://github.com/paritytech/polkadot/pull/7262

Minor API change to allow unique message IDs in Polkadot.

---

### [#14182](https://github.com/paritytech/substrate/pull/14182) RevertCmd: Expose database params via CLI

This exposes the database params for the `RevertCmd` via CLI. So, users can use `revert` with ParityDb.

Closes: https://github.com/paritytech/substrate/issues/14046

---

### [#14164](https://github.com/paritytech/substrate/pull/14164) Adds ability to use default hasher in `dev_mode` for explicit key binding

Fixes #14118 

Recently, we added the ability to specify hashers as _ in dev_mode, which are replaced by Blake2_128Concat. This PR allows using a default hasher in dev_mode in case of explicit key binding.

With these changes, a syntax like the below works in `dev_mode` but throws an error otherwise.

```rust
#[pallet::storage]
pub type Baz<T: Config> = StorageMap<Key = T::AccountId, Value = T::Balance>;
```

---

### [#14152](https://github.com/paritytech/substrate/pull/14152) FRAME: Tweak `frame_system::unique` to avoid minor entropy loss



---

### [#14149](https://github.com/paritytech/substrate/pull/14149) Introduce `entropy` function into frame System

This is a stateless function which provides a universally unique datum, suitable for use in XCM to provide each message with an unpredictable-but-unique identifier across the consensus universe. It may have other uses across the ecosystem.

---

### [#14144](https://github.com/paritytech/substrate/pull/14144) Actually respect locks of zero

When using `set_lock` to lock zero funds, it should not be a no-op (unlike `extend_lock`, in which it is).


---

### [#14125](https://github.com/paritytech/substrate/pull/14125) fix broken gensis state doc link

Was going through basic example pallet and noticed this.

Proc macro was expanding to a (now broken) doc link to https://docs.substrate.io/v3/runtime/chain-specs#the-genesis-state

This PR updates it to https://docs.substrate.io/build/genesis-configuration/. Please correct me if this is not the right updated link!

P.S. @kianenigma this might be a good opportunity to use a shortener if that has had any movement ;)

---

### [#14108](https://github.com/paritytech/substrate/pull/14108) frame: Enable GenesisConfig in no_std

This change enables `GenesisConfig` compilation in `no_std` environment.

It also enables `Default` implementation for `GenesisConfig` which will be required for no_std in no-native
runtime world. It must be possible to instantiate default GenesisConfig for pallets and runtime.

Step towards: #13334

---

### [#14106](https://github.com/paritytech/substrate/pull/14106) Timeout only if the referendum is not queued

Right now a referendum is cancelled if the track is so busy that the deciding timeout elapses regardless of whether it is queued or not. This isn't especially sensible. We alter it so that it will only be cancelled if the timeout elapses and it is not queued (i.e. the deciding deposit is not paid).

---

### [#14094](https://github.com/paritytech/substrate/pull/14094) sc-informant: Do not show `Block history` if doing major sync

After warp syncing a node it still downloads the block history. If the node is stopped and then started later while downloading the block history, the node first needs to do a major sync to sync to the tip of the chain. Before informant was showing `Block history` as sync state, while we actually were doing a major sync. This pr is fixing this.



---

### [#14070](https://github.com/paritytech/substrate/pull/14070) Add `Blocked` Account Status to Assets Pallet

Introducing the asset account state of `Blocked`, that is `Frozen` + ineligible to receive funds of the asset.

requires https://github.com/paritytech/substrate/pull/13843

---

### [#14063](https://github.com/paritytech/substrate/pull/14063) Account touch trait

This PR introduces `AccountTouch` trait and its implementation by `pallet-assets` which allows the creation of asset account for some account id with a designated depositor. 

requires https://github.com/paritytech/substrate/pull/13843

---

### [#14039](https://github.com/paritytech/substrate/pull/14039) Staking::{bond, set_controller} to set controllers to stash only.

This PR updates the staking pallet's `set_controller` and `bond` calls to not take the `controller` argument. `set_controller` and `bond` always set the controller to the stash account and signer respectively.

Doing this turns off the taps to new unique stash & controller pairs, aiding in the controller account deprecation and migration to proxy accounts.

- [x] Disallow unique controllers for `set_controller`.
- [x] Disallow unique controllers for `bond`.
- [x] Fix staking tests.
- [x] Fix staking benchmarks.
- [x] Fix fast-unstake tests.
- [x] Fix test-staking-e2e tests.
- [x] Fix root-offences tests.
- [x] Tidy up functions.

---

### [#13999](https://github.com/paritytech/substrate/pull/13999) Manual seal delayed finalize

Solves https://github.com/paritytech/substrate-contracts-node/issues/160
(Before integration to substrate-contract-node, upstream changes in substrate required.)

Adding delayed block finalization for instant block sealing consensus. This is needed for the local development node such as [substrate-contract-node](https://github.com/paritytech/substrate-contracts-node), [swanky-node](https://github.com/AstarNetwork/swanky-node).
Instant finalization causes difficulties for frontend development, it is necessary for them to configure the delayed time for block finalization after blocks are imported.

An integration example for actual node can be found here https://github.com/AstarNetwork/swanky-node/pull/61.

---

### [#13993](https://github.com/paritytech/substrate/pull/13993) BREAKING - Try-runtime: Use proper error types

Updates the return types of:

- [x] `try_state` to `DispatchResult`
- [x] `pre_upgrade` to `Result<_, DispatchError>`
- [x] `post_upgrade` to `DispatchResult`
- [x] `try_on_runtime_upgrade` to `Result<Weight, DispatchError>`

TODO:
- [x] Check for places where some existing error variants can be used.

This PR introduces a new type inside `sp_runtime` called `TryRuntimeError`. This new type is essentially just an alias to the `DispatchError` type. This only improves the readability of the code.

All of the hooks that now have a different error type should no longer use `assert!` or similar. The reason for this is that we don't want the code in these macros to panic, instead in case of an error we want to return the `TryRuntimeError` type. 
Since `TryRuntimeError` is an alias for `DispatchError` it allows us to use some existing error variants, but in case there isn't an existing variant that could convey the error message `&'static str` should be used which will get converted to `TryRuntimeError` during compile time.

Polkadot companion: https://github.com/paritytech/polkadot/pull/7146
Cumulus companion: https://github.com/paritytech/cumulus/pull/2615

Closes: #13736

---

### [#13852](https://github.com/paritytech/substrate/pull/13852) fungible conformance tests: Inspect and Mutate

Partial: https://github.com/paritytech/substrate/issues/13252

Implements conformance tests for `fungible` traits `Inspect` and `Mutate`.

- [x] Pattern for creating a function that accepts something implementing `Inspect + Mutate`
    - ```rust
        pub fn something<T, AccountId, Balance>()
        where
	        T: Mutate<AccountId> + Inspect<AccountId, Balance = Balance>,
	        AccountId: AtLeast8BitUnsigned,
	        Balance: AtLeast8BitUnsigned + Debug,
        {}
        ```

- [x] Implement inspect and mutate conformance tests (`frame/support/src/traits/tokens/fungible/conformance_tests/inspect_mutate.rs`)
- [x] Test conformance tests against `balances` (`frame/balances/src/tests/fungible_conformance_tests.rs`)
     - ```
        cargo test --package pallet-balances -- tests::fungible_conformance_tests:: --nocapture
        ```
- [x] Create a macro to generate test cases wrapped with some logic

---

### [#13843](https://github.com/paritytech/substrate/pull/13843) Allow Creation of Asset Accounts That Don't Exist Yet and Add `Blocked` Status

- Adds new dispatchables `touch_other` and `refund_other`, allowing an asset class's `Freezer` or `Admin` to create an account with zero balance in the asset class by placing a deposit; and to remove/refund. The existence of the account is represented by a new `ExistenceReason::DepositFrom` variant.
- Adds a new trait `AccountTouch` that allows other pallets to `touch` an account into existence for an asset class.
- Adds a new account status of `Blocked` (invoked by the asset class's `Freezer` via the new dispatchable `block`). Unlike `Frozen`, which prevents withdrawals from an account, `Blocked` prevents both withdrawals from and deposits into the blocked account. The account can be returned to its unrestricted (`Liquid`) state via the existing `thaw` function.

Cumulus Companion: https://github.com/paritytech/cumulus/pull/2437

---

### [#13807](https://github.com/paritytech/substrate/pull/13807) contracts: add events to ContractResult

Fix #12412 

It adds an Option `events` to the `ContractResult` struct (`ContractExecResult` and `ContractInstantiateResult`) so that calls to `bare_call` and `bare_instantiate` can return the events collected. This is useful when dry running.

Collecting events though should only be done outside of the runtime block execution, so that the `bare_call` and `bare_instantiate` functions accept a new `debug` parameter of type `DebugInfo` which is an enum. When `debug` is set to `DebugInfo::UnsafeDebug` the events are collected, when set to `DebugInfo::Skip` events return `None`.

Related Cargo Contract [issue](https://github.com/paritytech/cargo-contract/issues/1064)

cumulus companion: https://github.com/paritytech/cumulus/pull/2510


---

### [#13717](https://github.com/paritytech/substrate/pull/13717) Adds integration test for slashed/chilled validator with subsequent validation intention

Adds integration test for case mentioned in https://github.com/paritytech/substrate/issues/13714

---

### [#13705](https://github.com/paritytech/substrate/pull/13705) Deprecate Pallet `decl_*` Macros

It should come at no surprise that we are deprecating: `decl_module`, `decl_storage`, `decl_error` and `decl_event`.  
Any remaining usage should be migrated to use `#[frame_support::pallet]`.

Related https://github.com/paritytech/substrate/issues/12248  
Depends on https://github.com/paritytech/substrate/pull/12445, https://github.com/paritytech/substrate/pull/12401

---

### [#13701](https://github.com/paritytech/substrate/pull/13701) Statement store

This implements https://github.com/paritytech/labs/issues/3
See [README.md](https://github.com/paritytech/substrate/pull/13701/files#diff-ac0906dc65f1bc7b19d1a167dc5192d81cd053e6acdff080b324df0784ed51a3) for more details.

Still left to do (in follow-up PRs):

*  Encryption
*  API for reporting statistics
*  Better prioritizatoin of locally inserted statements w.r.t. storage and propagation. 

Additional changes required after chatting with @gavofyork 

- [x] Calculate statement count/size limit per account, and not just globally. This is based on balance.
- [x] Add a `Channel` field to allow replacing statement. Only each statement with a unique pair `(account, channel)` may exist.
- [x] Reintroduce `Priority` field. This will be used to prioritize statements withing the per-account limit.
- [x] Remove time-based statement expiration

polkadot companion: https://github.com/paritytech/polkadot/pull/6995
cumulus companion: https://github.com/paritytech/cumulus/pull/2423


---

### [#13417](https://github.com/paritytech/substrate/pull/13417) Improve handling of unset `StorageVersion`

When a user is forgetting to set the storage version in a pallet and calls `current_storage_version` to compare it against the `on_chain_storage_version` it will now fail to compile the code. Before the pallet macro just returned `StorageVersion::default()` for `current_storage_version` leading to potential issues with migrations. Besides that it also checks in `post_upgrade` that the pallet storage version was upgraded and thus, no migration was missed.


Closes: https://github.com/paritytech/substrate/issues/13062

# Failing try-runtime tests

After this pr it can happen that `try-runtime` tests are failing, because pallets don't have the proper `StorageVersion` set on chain. This can either mean that a migration was missed or that a pallet was added after genesis and it was missed to set the storage version. To fix the later, it just requires a simple migration that does:

```
fn on_runtime_upgrade() {
    StorageVersion::new(EXPECTED_VERSION).put::<Pallet_That_Is_failing>();
}
```

After that `try-runtime` will be happy and everything should work.

---

### [#13384](https://github.com/paritytech/substrate/pull/13384) rpc server: break legacy CLI options and remove "backward compatible HTTP server"

Close https://github.com/paritytech/substrate/issues/13049 https://github.com/paritytech/substrate/issues/13561

The CLI options that are removed/or renamed are:

1.  --rpc--max--payload (replaced by --rpc--max-request-size and --rpc-max-response-size)
3. --ws--max--out-buffer-capacity
4. --ws-external (replaced by --rpc_external)
5. --unsafe--ws--external (replaced by --unsafe-rpc-external)
6. --ipc--path 
7. --ws-port (replaced by --rpc--port)
8. --ws-max--connections (replaced by --rpc--max--connections)
9. --rpc-http (replaced by --rpc-addr)
10. --rpc-ws (replaced by --rpc-addr)

polkadot companion: https://github.com/paritytech/polkadot/pull/6987

cumulus companion: https://github.com/paritytech/cumulus/pull/2417


---

### [#13373](https://github.com/paritytech/substrate/pull/13373) Create benchmark for the `system::set_code` instrisic

Benchmark `system::set_code` by timing uncompression and setting the *kitchensink* runtime, which is a rather big runtime. So it should be feasible to determine an upper bound.

polkadot companion: https://github.com/paritytech/polkadot/pull/7060
cumulus companion: https://github.com/paritytech/cumulus/pull/2547

fixes #13192

polkadot address: 1ZApdbwrNnT1Hey4xeTAH6SZPDgbA9ZVftNuu9jTRbkc2Bg

---

### [#13027](https://github.com/paritytech/substrate/pull/13027) Add `serde` feature flag to primitives

Adds `serde` feature flag to the primitives. This way, serde (de)serialization can also be used in `no_std` environments.
The following crates now implement the `serde` flag:
- `sp-application-crypto`
- `sp-arithmetic`
- `sp-consensus-babe`
- `sp-consensus-beefy`
- `sp-consensus-grandpa`
- `sp-consensus-slots`
- `sp-core`
- `sp-mmr-primitives`
- `sp-npos-elections`
- `sp-runtime`
- `sp-storage`
- `sp-test-primitives`
- `sp-version`
- `sp-weights`

closes https://github.com/paritytech/substrate/issues/12994

Kusama address: FsnxqJnqWVNMZZgxaQdhaCk9c5sL3WSggRCRqp1qEzk1L2i

---

Here are note-worthy **node** PRs in Substrate repo merged between 2023-05-01 and 2023-05-23.

### [#14191](https://github.com/paritytech/substrate/pull/14191) TrieCache: Fine tune the size of the local and node cache

First, we increase the size to 10MiB for the local cache. Second, we give the node cache a bigger max size than the value cache, see the changed comment on why.

In general this should ensure that we are able to cache the `:code` and not directly throw it out of the cache because it is too big (which currently happens when the size of the runtime > 2MiB). In the future this should be improved to ensure that certain values are not removed from the cache at all, like `:code`.




---

### [#14190](https://github.com/paritytech/substrate/pull/14190) WarpSync: Show number of required peers in informant

This makes it for the user more obvious on what we are waiting and not just "waiting for peers".



---

### [#14184](https://github.com/paritytech/substrate/pull/14184) Executor: Add `create_runtime_from_artifact_bytes`

# PULL REQUEST

## Overview

See title. Also export `WasmtimeRuntime`, returned by the `create_runtime*` functions.

I benchmarked the performance regression out of curiosity: https://github.com/bytecodealliance/wasmtime/pull/6420. But since runtime creation is not at all a bottleneck, it makes sense to always use this new function for the reasons given in the related issue and PR.

## Relevant Issues/PRs

Needed for https://github.com/paritytech/polkadot/pull/7246#discussion_r1199178044
Closes https://github.com/paritytech/substrate/issues/13861

---

### [#14182](https://github.com/paritytech/substrate/pull/14182) RevertCmd: Expose database params via CLI

This exposes the database params for the `RevertCmd` via CLI. So, users can use `revert` with ParityDb.

Closes: https://github.com/paritytech/substrate/issues/14046

---

### [#14164](https://github.com/paritytech/substrate/pull/14164) Adds ability to use default hasher in `dev_mode` for explicit key binding

Fixes #14118 

Recently, we added the ability to specify hashers as _ in dev_mode, which are replaced by Blake2_128Concat. This PR allows using a default hasher in dev_mode in case of explicit key binding.

With these changes, a syntax like the below works in `dev_mode` but throws an error otherwise.

```rust
#[pallet::storage]
pub type Baz<T: Config> = StorageMap<Key = T::AccountId, Value = T::Balance>;
```

---

### [#14149](https://github.com/paritytech/substrate/pull/14149) Introduce `entropy` function into frame System

This is a stateless function which provides a universally unique datum, suitable for use in XCM to provide each message with an unpredictable-but-unique identifier across the consensus universe. It may have other uses across the ecosystem.

---

### [#14144](https://github.com/paritytech/substrate/pull/14144) Actually respect locks of zero

When using `set_lock` to lock zero funds, it should not be a no-op (unlike `extend_lock`, in which it is).


---

### [#14108](https://github.com/paritytech/substrate/pull/14108) frame: Enable GenesisConfig in no_std

This change enables `GenesisConfig` compilation in `no_std` environment.

It also enables `Default` implementation for `GenesisConfig` which will be required for no_std in no-native
runtime world. It must be possible to instantiate default GenesisConfig for pallets and runtime.

Step towards: #13334

---

### [#14106](https://github.com/paritytech/substrate/pull/14106) Timeout only if the referendum is not queued

Right now a referendum is cancelled if the track is so busy that the deciding timeout elapses regardless of whether it is queued or not. This isn't especially sensible. We alter it so that it will only be cancelled if the timeout elapses and it is not queued (i.e. the deciding deposit is not paid).

---

### [#14094](https://github.com/paritytech/substrate/pull/14094) sc-informant: Do not show `Block history` if doing major sync

After warp syncing a node it still downloads the block history. If the node is stopped and then started later while downloading the block history, the node first needs to do a major sync to sync to the tip of the chain. Before informant was showing `Block history` as sync state, while we actually were doing a major sync. This pr is fixing this.



---

### [#14080](https://github.com/paritytech/substrate/pull/14080) Prepare `sc-network` for `ProtocolController`/`NotificationService`

The upcoming notification protocol refactoring requires that protocols are able to communicate with `sc-network` over unique and direct links. This means that `sc-network` side of the link has to be created before `sc-network` is initialized and that it is allowed to consume the object as the receiver half of the link may not implement `Clone`.

Remove request-response and notification protocols from `NetworkConfiguration` and create a new object that contains the configurations of these protocols and which is consumable by `sc-network`. This is needed needed because, e.g., the receiver half of `NotificationService` is not clonable so `sc-network` must consume it when it's initializing the protocols in `Notifications`.

Similar principe applies to `PeerStore`/`ProtocolController`: as per current design, protocols are created before the network so `Protocol` cannot be the one creating the `PeerStore` object. `FullNetworkConfiguration` will be used to store the objects that `sc-network` will use to communicate with protocols and it will also allow protocols to allocate handles so they can directly communicate with `sc-network`.

polkadot companion: https://github.com/paritytech/polkadot/pull/7184
cumulus companion: https://github.com/paritytech/cumulus/pull/2526

---

### [#14070](https://github.com/paritytech/substrate/pull/14070) Add `Blocked` Account Status to Assets Pallet

Introducing the asset account state of `Blocked`, that is `Frozen` + ineligible to receive funds of the asset.

requires https://github.com/paritytech/substrate/pull/13843

---

### [#14069](https://github.com/paritytech/substrate/pull/14069) Backport of #14067 for release 0.9.42

Backport of #14067

---

### [#14067](https://github.com/paritytech/substrate/pull/14067) Only calculate tree route during finalization when there are multiple leaves

Calculation of these tree routes is very expensive. When the finalized block is very far from the best block, it can take multiple seconds to calculate this tree route, blocking the import lock.

If there is only one leave, we can skip this calculation since the best block is guaranteed to be a descendant of the new finalized one.

Closes https://github.com/paritytech/cumulus/issues/2494, https://github.com/paritytech/substrate/issues/13947, 

Could impact the parachain part of https://github.com/paritytech/substrate/issues/14049

~Edit: Do not close the above issues for now, freshly syncing node still has issues.~

---

### [#14039](https://github.com/paritytech/substrate/pull/14039) Staking::{bond, set_controller} to set controllers to stash only.

This PR updates the staking pallet's `set_controller` and `bond` calls to not take the `controller` argument. `set_controller` and `bond` always set the controller to the stash account and signer respectively.

Doing this turns off the taps to new unique stash & controller pairs, aiding in the controller account deprecation and migration to proxy accounts.

- [x] Disallow unique controllers for `set_controller`.
- [x] Disallow unique controllers for `bond`.
- [x] Fix staking tests.
- [x] Fix staking benchmarks.
- [x] Fix fast-unstake tests.
- [x] Fix test-staking-e2e tests.
- [x] Fix root-offences tests.
- [x] Tidy up functions.

---

### [#13999](https://github.com/paritytech/substrate/pull/13999) Manual seal delayed finalize

Solves https://github.com/paritytech/substrate-contracts-node/issues/160
(Before integration to substrate-contract-node, upstream changes in substrate required.)

Adding delayed block finalization for instant block sealing consensus. This is needed for the local development node such as [substrate-contract-node](https://github.com/paritytech/substrate-contracts-node), [swanky-node](https://github.com/AstarNetwork/swanky-node).
Instant finalization causes difficulties for frontend development, it is necessary for them to configure the delayed time for block finalization after blocks are imported.

An integration example for actual node can be found here https://github.com/AstarNetwork/swanky-node/pull/61.

---

### [#13993](https://github.com/paritytech/substrate/pull/13993) BREAKING - Try-runtime: Use proper error types

Updates the return types of:

- [x] `try_state` to `DispatchResult`
- [x] `pre_upgrade` to `Result<_, DispatchError>`
- [x] `post_upgrade` to `DispatchResult`
- [x] `try_on_runtime_upgrade` to `Result<Weight, DispatchError>`

TODO:
- [x] Check for places where some existing error variants can be used.

This PR introduces a new type inside `sp_runtime` called `TryRuntimeError`. This new type is essentially just an alias to the `DispatchError` type. This only improves the readability of the code.

All of the hooks that now have a different error type should no longer use `assert!` or similar. The reason for this is that we don't want the code in these macros to panic, instead in case of an error we want to return the `TryRuntimeError` type. 
Since `TryRuntimeError` is an alias for `DispatchError` it allows us to use some existing error variants, but in case there isn't an existing variant that could convey the error message `&'static str` should be used which will get converted to `TryRuntimeError` during compile time.

Polkadot companion: https://github.com/paritytech/polkadot/pull/7146
Cumulus companion: https://github.com/paritytech/cumulus/pull/2615

Closes: #13736

---

### [#13852](https://github.com/paritytech/substrate/pull/13852) fungible conformance tests: Inspect and Mutate

Partial: https://github.com/paritytech/substrate/issues/13252

Implements conformance tests for `fungible` traits `Inspect` and `Mutate`.

- [x] Pattern for creating a function that accepts something implementing `Inspect + Mutate`
    - ```rust
        pub fn something<T, AccountId, Balance>()
        where
	        T: Mutate<AccountId> + Inspect<AccountId, Balance = Balance>,
	        AccountId: AtLeast8BitUnsigned,
	        Balance: AtLeast8BitUnsigned + Debug,
        {}
        ```

- [x] Implement inspect and mutate conformance tests (`frame/support/src/traits/tokens/fungible/conformance_tests/inspect_mutate.rs`)
- [x] Test conformance tests against `balances` (`frame/balances/src/tests/fungible_conformance_tests.rs`)
     - ```
        cargo test --package pallet-balances -- tests::fungible_conformance_tests:: --nocapture
        ```
- [x] Create a macro to generate test cases wrapped with some logic

---

### [#13843](https://github.com/paritytech/substrate/pull/13843) Allow Creation of Asset Accounts That Don't Exist Yet and Add `Blocked` Status

- Adds new dispatchables `touch_other` and `refund_other`, allowing an asset class's `Freezer` or `Admin` to create an account with zero balance in the asset class by placing a deposit; and to remove/refund. The existence of the account is represented by a new `ExistenceReason::DepositFrom` variant.
- Adds a new trait `AccountTouch` that allows other pallets to `touch` an account into existence for an asset class.
- Adds a new account status of `Blocked` (invoked by the asset class's `Freezer` via the new dispatchable `block`). Unlike `Frozen`, which prevents withdrawals from an account, `Blocked` prevents both withdrawals from and deposits into the blocked account. The account can be returned to its unrestricted (`Liquid`) state via the existing `thaw` function.

Cumulus Companion: https://github.com/paritytech/cumulus/pull/2437

---

### [#13807](https://github.com/paritytech/substrate/pull/13807) contracts: add events to ContractResult

Fix #12412 

It adds an Option `events` to the `ContractResult` struct (`ContractExecResult` and `ContractInstantiateResult`) so that calls to `bare_call` and `bare_instantiate` can return the events collected. This is useful when dry running.

Collecting events though should only be done outside of the runtime block execution, so that the `bare_call` and `bare_instantiate` functions accept a new `debug` parameter of type `DebugInfo` which is an enum. When `debug` is set to `DebugInfo::UnsafeDebug` the events are collected, when set to `DebugInfo::Skip` events return `None`.

Related Cargo Contract [issue](https://github.com/paritytech/cargo-contract/issues/1064)

cumulus companion: https://github.com/paritytech/cumulus/pull/2510


---

### [#13705](https://github.com/paritytech/substrate/pull/13705) Deprecate Pallet `decl_*` Macros

It should come at no surprise that we are deprecating: `decl_module`, `decl_storage`, `decl_error` and `decl_event`.  
Any remaining usage should be migrated to use `#[frame_support::pallet]`.

Related https://github.com/paritytech/substrate/issues/12248  
Depends on https://github.com/paritytech/substrate/pull/12445, https://github.com/paritytech/substrate/pull/12401

---

### [#13701](https://github.com/paritytech/substrate/pull/13701) Statement store

This implements https://github.com/paritytech/labs/issues/3
See [README.md](https://github.com/paritytech/substrate/pull/13701/files#diff-ac0906dc65f1bc7b19d1a167dc5192d81cd053e6acdff080b324df0784ed51a3) for more details.

Still left to do (in follow-up PRs):

*  Encryption
*  API for reporting statistics
*  Better prioritizatoin of locally inserted statements w.r.t. storage and propagation. 

Additional changes required after chatting with @gavofyork 

- [x] Calculate statement count/size limit per account, and not just globally. This is based on balance.
- [x] Add a `Channel` field to allow replacing statement. Only each statement with a unique pair `(account, channel)` may exist.
- [x] Reintroduce `Priority` field. This will be used to prioritize statements withing the per-account limit.
- [x] Remove time-based statement expiration

polkadot companion: https://github.com/paritytech/polkadot/pull/6995
cumulus companion: https://github.com/paritytech/cumulus/pull/2423


---

### [#13417](https://github.com/paritytech/substrate/pull/13417) Improve handling of unset `StorageVersion`

When a user is forgetting to set the storage version in a pallet and calls `current_storage_version` to compare it against the `on_chain_storage_version` it will now fail to compile the code. Before the pallet macro just returned `StorageVersion::default()` for `current_storage_version` leading to potential issues with migrations. Besides that it also checks in `post_upgrade` that the pallet storage version was upgraded and thus, no migration was missed.


Closes: https://github.com/paritytech/substrate/issues/13062

# Failing try-runtime tests

After this pr it can happen that `try-runtime` tests are failing, because pallets don't have the proper `StorageVersion` set on chain. This can either mean that a migration was missed or that a pallet was added after genesis and it was missed to set the storage version. To fix the later, it just requires a simple migration that does:

```
fn on_runtime_upgrade() {
    StorageVersion::new(EXPECTED_VERSION).put::<Pallet_That_Is_failing>();
}
```

After that `try-runtime` will be happy and everything should work.

---

### [#13384](https://github.com/paritytech/substrate/pull/13384) rpc server: break legacy CLI options and remove "backward compatible HTTP server"

Close https://github.com/paritytech/substrate/issues/13049 https://github.com/paritytech/substrate/issues/13561

The CLI options that are removed/or renamed are:

1.  --rpc--max--payload (replaced by --rpc--max-request-size and --rpc-max-response-size)
3. --ws--max--out-buffer-capacity
4. --ws-external (replaced by --rpc_external)
5. --unsafe--ws--external (replaced by --unsafe-rpc-external)
6. --ipc--path 
7. --ws-port (replaced by --rpc--port)
8. --ws-max--connections (replaced by --rpc--max--connections)
9. --rpc-http (replaced by --rpc-addr)
10. --rpc-ws (replaced by --rpc-addr)

polkadot companion: https://github.com/paritytech/polkadot/pull/6987

cumulus companion: https://github.com/paritytech/cumulus/pull/2417


---

### [#13373](https://github.com/paritytech/substrate/pull/13373) Create benchmark for the `system::set_code` instrisic

Benchmark `system::set_code` by timing uncompression and setting the *kitchensink* runtime, which is a rather big runtime. So it should be feasible to determine an upper bound.

polkadot companion: https://github.com/paritytech/polkadot/pull/7060
cumulus companion: https://github.com/paritytech/cumulus/pull/2547

fixes #13192

polkadot address: 1ZApdbwrNnT1Hey4xeTAH6SZPDgbA9ZVftNuu9jTRbkc2Bg

---

### [#13027](https://github.com/paritytech/substrate/pull/13027) Add `serde` feature flag to primitives

Adds `serde` feature flag to the primitives. This way, serde (de)serialization can also be used in `no_std` environments.
The following crates now implement the `serde` flag:
- `sp-application-crypto`
- `sp-arithmetic`
- `sp-consensus-babe`
- `sp-consensus-beefy`
- `sp-consensus-grandpa`
- `sp-consensus-slots`
- `sp-core`
- `sp-mmr-primitives`
- `sp-npos-elections`
- `sp-runtime`
- `sp-storage`
- `sp-test-primitives`
- `sp-version`
- `sp-weights`

closes https://github.com/paritytech/substrate/issues/12994

Kusama address: FsnxqJnqWVNMZZgxaQdhaCk9c5sL3WSggRCRqp1qEzk1L2i

## 👀 Releases

## 📰 Substrate jobs

Have a look at all the open roles in the ecosystem on the [Substrate Job Board](https://careers.substrate.io/jobs).

Got ideas for content you’d like to see in future newsletters? Make a PR to the next edition [here](https://github.com/substrate-developer-hub/newsletter/pulls) – we’d love to include them. ❤️

_Previous editions of this newsletter are available in the public archive rendered on [this web page](https://substrate-developer-hub.github.io/newsletter/) as well as [on Polkaverse](https://polkaverse.com/10647). Join us there to comment, emote or provide feedback on our newsletters – all using a decentralised social media space built with Substrate and IPFS._
