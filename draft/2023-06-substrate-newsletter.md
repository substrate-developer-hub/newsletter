## Runtime

Here are note-worthy **Runtime** PRs in Substrate repo merged between 2023-05-01 and 2023-06-23.

### [#14417](https://github.com/paritytech/substrate/pull/14417) suppress unused warning in kitchensink example

**Summary**

This PR fixes the unused error for `new_test_ext()` when compiling `cargo test` in the kitchensink node by adding a test that uses it.

### [#14397](https://github.com/paritytech/substrate/pull/14397) Delete 1D weight ctors and set explicit deprecation dates

**Summary**

The code changes involve deleting two functions after a grace period and adding a removal date of July 2023 to various already deprecated items.

---

### [#14375](https://github.com/paritytech/substrate/pull/14375) Restructure macro-related exports into private mods for frame

**Summary**

This code change removes some types from `frame::support::inherent` and suggests importing them from their respective origins instead. It is recommended to wait for the `frame` crate to give them a smooth transition.

---

### [#14326](https://github.com/paritytech/substrate/pull/14326) Frame: Give Referendum `SubmitOrigin` argument

**Summary**

This code change allows for inspection of the track a submission origin is being made for, and updates all type bounders in Substrate to support the `EnsureOriginWithArg` trait as well as the `EnsureOrigin` trait. A macro is introduced to allow `EnsureOrigin` implementors to support `EnsureOriginWithArg`. If using the Referenda pallet and encountering a build error around `SubmitOrigin`, wrap the type with `frame_support::AsEnsureOriginWithArg` to get an `EnsureOriginWithArg` implementation.

---

### [#14309](https://github.com/paritytech/substrate/pull/14309) Move `type Migrations` to `Config`

**Summary**

This PR removes the hardcoded migration sequence from `migrations.rs` in the Contracts pallet and places it within `Config` so it can be configured in the runtime. Developers need to update their runtime configuration with their pending migrations. This is a breaking change as it adds a new type to the `Config`.

---

### [#14261](https://github.com/paritytech/substrate/pull/14261) frame: support for serde added

**Summary**

The code changes include enabling `serde` features in dependent crates, adding `serde::Serialize` and `serde::Deserialize` implementation for `enum Forcing` in `frame::staking`, providing `Serialize/Deserialize` implementation for `impl_opaque_keys` macro in `primitives::runtime`, adding `serde::Serialize` and `serde::Deserialize` implementation for `enum StakerStatus` in `primitives::staking`, and implementing `serde::Serialize/Deserialize` for pallets `GenesisConfig` in `no-std`. These changes are a step towards issue [#13334](https://github.com/paritytech/substrate/issues/13334) and are also reflected in the Polkadot and Cumulus companions.

---

### [#14260](https://github.com/paritytech/substrate/pull/14260) frame_system::remark: Allow any kind of origin

**Summary**

This PR updates the System pallet to allow any kind of origin to call the `remark` dispatchable.

---

### [#14241](https://github.com/paritytech/substrate/pull/14241) migration(tips): unreserve deposits

**Summary**

This code change adds a migration that unreserves all deposits made by the `tips` pallet. It records the reserves of all accounts with open tips prior to the migration, unreserves all balances locked up in tips, and checks that the reserved balances were reduced by the expected amount.

---

### [#14228](https://github.com/paritytech/substrate/pull/14228) wasm-builder: Enforce `runtime_version` wasm section

**Summary**

This code change enforces the `runtime_version` wasm section in the `wasm-builder` and provides a way to disable the check if needed. This change aims to prevent issues related to missing `RuntimeVersion` in the runtime.

---

### [#14226](https://github.com/paritytech/substrate/pull/14226) migration(democracy): unreserve deposits and clear locks

**Summary**

This code change adds a migration that unreserves all deposits and clears locks held by the democracy pallet. The pre-upgrade collects pre-migration data useful for validating the migration was successful, and also checks the integrity of deposited balances. The on-runtime upgrade unreserves and unlocks the balances. The post-upgrade checks that no more locks exist for the pallet, and reserved balances were reduced by the expected amount.

---

### [#14224](https://github.com/paritytech/substrate/pull/14224) Add a deprecation warning to the old runtime GenesisConfig

**Summary**

The PR adds a deprecation warning for using the runtime level `GenesisConfig`, which has been renamed to `RuntimeGenesisConfig`. It also includes links to related PRs in Cumulus and Polkadot companions.

---

### [#14218](https://github.com/paritytech/substrate/pull/14218) migration(elections-phragmen): unreserve deposits and clear locks

**Summary**

This code change adds a migration that unreserves all deposits and unlocks all stake held by the Elections-phragmen pallet. The migration collects pre-migration data useful for validating the migration was successful, and also checks the integrity of deposited and reserved balances. The on_runtime_upgrade unreserves and unlocks the balances, and post_upgrade checks that all expected locks were removed, and reserved balances were reduced by the expected amount.

---

### [#14214](https://github.com/paritytech/substrate/pull/14214) pallet-merkle-mountain-range: Remove extra `Hash` type

**Summary**

The code change removes the `type Hash` from the `pallet-merkle-mountain-range::Config`.

---

### [#14164](https://github.com/paritytech/substrate/pull/14164) Adds ability to use default hasher in `dev_mode` for explicit key binding

**Summary**

The code change allows using a default hasher in dev_mode in case of explicit key binding, which enables a syntax to work in dev_mode but throws an error otherwise.

---

### [#14149](https://github.com/paritytech/substrate/pull/14149) Introduce `entropy` function into frame System

**Summary**

The code change introduces a stateless function that generates a unique identifier for use in XCM and potentially other areas of the ecosystem.

---

### [#14144](https://github.com/paritytech/substrate/pull/14144) Actually respect locks of zero

**Summary**

This PR updates the `LockableCurrency` trait to ensure `set_lock` is not a no-op when locking zero funds.

---

### [#14108](https://github.com/paritytech/substrate/pull/14108) frame: Enable GenesisConfig in no_std

**Summary**

The code change enables `GenesisConfig` compilation in `no_std` environment and provides a `Default` implementation for `GenesisConfig` required for no_std in no-native runtime world.

---

### [#14106](https://github.com/paritytech/substrate/pull/14106) Timeout only if the referendum is not queued

**Summary**

The code change ensures that a referendum is only cancelled if the deciding deposit is not paid and the timeout elapses, rather than being cancelled regardless of whether it is queued or not.

---

### [#14070](https://github.com/paritytech/substrate/pull/14070) Add `Blocked` Account Status to Assets Pallet

**Description**

This PR adds an asset account state of `Blocked` when it is `Frozen` and unable to receive funds of the asset.

---

### [#14052](https://github.com/paritytech/substrate/pull/14052) add pallet macro kitchensink example/template

**Summary**

The PR adds a new pallet that showcases all `#[pallet::xxx]` macros and their usage.

---

### [#14045](https://github.com/paritytech/substrate/pull/14045) contracts: Multi block migrations

**Summary**

This PR adds a multi-block migration framework for pallet-contracts and fixes an issue. The changes include steps to test migration with try-runtime and zombienet, finding blocks involved in a migration, and steps to make it a generic migration framework. The migration framework currently relies on `MigrationInProgress` storage, which needs to be moved to a library or implemented as a new trait. Once implemented, people can configure their Migration type that they pass to Executive.

---

### [#14039](https://github.com/paritytech/substrate/pull/14039) Staking::{bond, set_controller} to set controllers to stash only.

**Summary**

This PR updates the staking pallet's `set_controller` and `bond` calls to not take the `controller` argument, disallowing unique controllers for these functions. It also fixes staking tests, benchmarks, fast-unstake tests, test-staking-e2e tests, and root-offences tests, and tidies up functions.

---

### [#14024](https://github.com/paritytech/substrate/pull/14024) pallet-aura: Allow multiple blocks per slot

**Summary**

The code change allows sequential blocks to be authored within the same slot, which will be useful for backlog of blocks and future roadmap items like elastic scaling and parallel block production. The update guide suggests setting the new `AllowMultipleBlocksPerSlot` to `false` to maintain current behavior.

---

### [#13993](https://github.com/paritytech/substrate/pull/13993) BREAKING - Try-runtime: Use proper error types

**Summary**

This PR updates the return types of several hooks and introduces a new type called `TryRuntimeError` which is an alias to `DispatchError`. The hooks should no longer use `assert!` and instead return `TryRuntimeError` in case of an error. Existing error variants can be used, but if there isn't one, `&'static str` should be used which will be converted to `TryRuntimeError` during compile time.

---

### [#13958](https://github.com/paritytech/substrate/pull/13958) Take into account proof size for transaction payment and priority

**Summary**

The code changes will now take into account the proof size while adjusting the fee in the Transaction Payment pallet, which will prevent an attacker from filling the block with storage size without paying an appropriate fee. The PR also considers proof size for calculation of transaction priority. Care needs to be taken to set the max PoV size for a chain to ensure optimal block fullness based on each weight dimension.

---

### [#13869](https://github.com/paritytech/substrate/pull/13869) HoldReason: Improve usage

**Summary**

The `HoldReason` attribute was recently switched to use the `composite_enum` attribute, which requires changes to downstream code. This PR adds `RuntimeHoldReason` as type to the Config trait and requires that Currency is uses the same reason. With this update, `HoldReason` needs to be removed from `pallet_nis::Config` and replaced with `RuntimeHoldReason`. For the `pallet_balances::Config` trait you need to change `HoldIdentifier` to `RuntimeHoldReason` and pass the `RuntimeHoldReason` that is being generated by `construct_runtime!`.

---

### [#13852](https://github.com/paritytech/substrate/pull/13852) fungible conformance tests: Inspect and Mutate

**Summary**

The code changes implement conformance tests for `fungible` traits `Inspect` and `Mutate`. It includes a pattern for creating a function that accepts something implementing `Inspect + Mutate`, implementation of inspect and mutate conformance tests, testing conformance tests against `balances`, and creation of a macro to generate test cases wrapped with some logic.

---

### [#13843](https://github.com/paritytech/substrate/pull/13843) Allow Creation of Asset Accounts That Don't Exist Yet and Add `Blocked` Status

**Summary**

The code changes add new dispatchables for creating and refunding accounts with zero balance in an asset class, represented by a new variant. A new trait is added to allow other pallets to create an account. A new account status of "Blocked" is also added, which prevents both withdrawals and deposits, and can be returned to its unrestricted state via the existing "thaw" function.

---

### [#13705](https://github.com/paritytech/substrate/pull/13705) Deprecate Pallet `decl_*` Macros

**Summary**

The code changes involve deprecating `decl_module`, `decl_storage`, `decl_error`, and `decl_event` and migrating any remaining usage to `#[frame_support::pallet]`. There are related issues and pull requests that these changes depend on.

---

### [#13454](https://github.com/paritytech/substrate/pull/13454) [FRAME Core] Default Pallet Config Trait / derive_impl

**Summary**

This PR adds the ability for a pallet to define one or more defaults for its trait Config via `#[pallet::config(with_default)]`. Then, when writing `impl Config for Runtime`, one of these defaults can be used to elide any missing type item via `#[derive_impl(path_to_default_impl)]`. At the moment, this is limited to type items that do not rely on `frame_system::Config`. This PR also adds several attribute proc macros to frame_support, most notably `#[derive_impl(..)]` and `#[register_default_impl(..)]`, which in tandem make it possible to create trait impls that provide sane defaults and dynamically inject the non-colliding trait items from these impls into downstream trait impls that want to use the sane defaults but potentially override some of them.

---

### [#13417](https://github.com/paritytech/substrate/pull/13417) Improve handling of unset `StorageVersion`

**Summary**

This code change ensures that if a user forgets to set the storage version in a pallet and calls `current_storage_version`, it will fail to compile the code. It also checks in `post_upgrade` that the pallet storage version was upgraded and no migration was missed. However, this may cause `try-runtime` tests to fail, which can be fixed by setting the storage version using a simple migration.

---

### [#13373](https://github.com/paritytech/substrate/pull/13373) Create benchmark for the `system::set_code` instrisic

**Summary**

The code changes benchmark `system::set_code` by timing uncompression and setting the *kitchensink* runtime to determine an upper bound.

---

### [#13031](https://github.com/paritytech/substrate/pull/13031) arkworks integration

**Summary**

This PR adds host function calls for elliptic curve arithmetic used by Arkworks to the sp_crypto_ec_utils crate. The host calls are for bls12_381, bls12_377, ed_on_bls12_381, ed_on_bls12_77, bw6_761. The host functions receive their arguments serialized to `Vec<u8>` by ark-scale and return the result as serialized `Result<Vec<u8>, ()>`, which then needs to be deserialized by `ark-scale`. The curves are defined in the https://github.com/paritytech/ark-substrate repo and receive the host functions by dependency injection. Tests are covered by pulling in https://github.com/paritytech/ark-substrate where we instantiate the `ark-substrate` curves, which receive the sp-io host function implementations by dependency injection. The PR could be further optimized by adding more curves and replacing more operations by host function calls.

---

### [#11324](https://github.com/paritytech/substrate/pull/11324) Society v2

**Summary**

The changes to Society pallet include the removal of technical limitations on the number of members, proper use of `BoundedVec`, and the ability for the founder to alter max members and intake size without a runtime upgrade. Members are ranked and voting weight is determined by rank. The candidate voting process is now a two-phase process, and the voting/reward/punishment scheme for candidates and challenged members is completely different.

---

## Node SDK

Here are note-worthy **Node SDK** PRs in Substrate repo merged between 2023-05-01 and 2023-06-23.

### [#14391](https://github.com/paritytech/substrate/pull/14391) expose setting kademlia replication factor through node CLI

**Summary**

The code change exposes the ability to set the Kademlia replication factor through the node's CLI, which is useful in test environments where the default replication factor of 20 may cause issues with `AuthorityDiscovery`.

---

### [#14285](https://github.com/paritytech/substrate/pull/14285) sc-transaction-pool: Always use best block to check if we should skip enactment

**Summary**

The tree route will be calculated against the best block and used to determine if checks should be skipped.

---

### [#14252](https://github.com/paritytech/substrate/pull/14252) sp-api: Set correct where bound in the generated code

**Summary**

The code fix corrects the where bound for the `create_metadata` function by using the where bound declared at the type declaration augmented with the manual where bound.

---

### [#14236](https://github.com/paritytech/substrate/pull/14236) Incorporate `sc-peerset` into `sc-network`

**Summary**

The code changes involve moving `Peerset`, `PeerStore`, and `ProtocolController` from `sc-peerset` to `sc-network` & `sc-network-common` in preparation for [#14170](https://github.com/paritytech/substrate/issues/14170). The `B1-note_worthy` label is added because the `sc-peerset` crate is retired.

---

### [#14230](https://github.com/paritytech/substrate/pull/14230) Make offchain tx pool creation reusable

**Summary**

A new `OffchainTransactionPoolFactory` is introduced to create offchain transaction pools that can be registered in the runtime externalities context, which will simplify the creation of offchain transaction pools in a future PR.

---

### [#14191](https://github.com/paritytech/substrate/pull/14191) TrieCache: Fine tune the size of the local and node cache

**Summary**

The code changes increase the size of the local cache to 10MiB and give the node cache a bigger max size than the value cache to ensure caching of `:code` and prevent it from being thrown out of the cache due to size limitations. Future improvements are planned to prevent certain values, such as `:code`, from being removed from the cache at all.

---

### [#14190](https://github.com/paritytech/substrate/pull/14190) WarpSync: Show number of required peers in informant

**Summary**

The change makes it clearer to the user what the system is waiting for, instead of just saying "waiting for peers".

---

### [#14182](https://github.com/paritytech/substrate/pull/14182) RevertCmd: Expose database params via CLI

**Summary**

The code change exposes database parameters for `RevertCmd` via CLI, allowing users to use `revert` with ParityDb.

---

### [#14094](https://github.com/paritytech/substrate/pull/14094) sc-informant: Do not show `Block history` if doing major sync

**Summary**

This code change fixes an issue where a node would need to do a major sync to sync to the tip of the chain if it was stopped and started while downloading block history, even after warp syncing. The change also updates the sync state displayed by `Informant`.

---

### [#13999](https://github.com/paritytech/substrate/pull/13999) Manual seal delayed finalize

**Summary**

The code changes add delayed block finalization for instant block sealing consensus, which is needed for local development nodes such as substrate-contract-node and swanky-node. Frontend development requires the ability to configure the delayed time for block finalization after blocks are imported. An integration example for an actual node can be found [here](https://github.com/AstarNetwork/swanky-node/pull/61).

---

### [#13800](https://github.com/paritytech/substrate/pull/13800) Remove wasmi backend from sc-executor

**Summary**

This PR removes the `wasmi` backend, making the runtime execution exclusively `wasmtime`.

---

### [#13701](https://github.com/paritytech/substrate/pull/13701) Statement store

**Summary**

This code change implements a feature for calculating statement count/size limit per account, adding a channel field to allow replacing statements, reintroducing a priority field, and removing time-based statement expiration. Encryption and API for reporting statistics are still left to do in follow-up PRs. There are also links to related PRs for polkadot and cumulus companions.

---

### [#13384](https://github.com/paritytech/substrate/pull/13384) rpc server: break legacy CLI options and remove "backward compatible HTTP server"

**Summary**

The code changes involve removing or renaming several CLI options in Substrate, including `--rpc--max--payload`, `--ws--max--out-buffer-capacity`, `--ws-external`, `--unsafe--ws--external`, `--ipc--path`, `--ws-port`, `--ws-max--connections`, `--rpc-http`, and `--rpc-ws`. These changes are reflected in the Polkadot and Cumulus companions.