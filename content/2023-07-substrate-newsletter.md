This page contains summaries of the merged PRs into Substrate organized in two sections: "Runtime" (using the `B1-note_worthy` + `T1-runtime` labels) and "Node SDK" (using the `B1-note_worthy` + `T0-node` labels).
Read more about how Substrate uses labels [here](https://github.com/paritytech/substrate/blob/master/docs/CONTRIBUTING.adoc#merge-process).

## Runtime

Here are note-worthy **Runtime** PRs in Substrate repo merged between 2023-06-23 and 2023-07-25.

### [#14586](https://github.com/paritytech/substrate/pull/14586) `WeightMeter`: more consistent naming

**Summary**

The code changes recommended by @gavofyork involve more consistent naming for the `WeightMeter`. The changes include deprecating certain methods and introducing new ones with different names. Additionally, the `consumed` and `limit` variables are privatized and new getter methods `consumed()` and `limit()` are added.

---

### [#14546](https://github.com/paritytech/substrate/pull/14546) Run `integrity_test` in Externalities

**Summary**

This code change includes a change to always run the `integrity_test` in test externalities.

---

### [#14481](https://github.com/paritytech/substrate/pull/14481) Stabilize V15 Metadata

**Summary**

This PR stabilizes the V15 metadata by making several changes. It exposes APIs to easily update the metadata in the future, collects type information about the runtime API functions, adds overarching enums to the metadata to ease decoding, modifies the extrinsic metadata to include type information for certain types, and adds support for custom types without breaking changes. These changes aim to improve the stability and functionality of metadata for Substrate chains.

---

### [#14437](https://github.com/paritytech/substrate/pull/14437) Moves `Block` to `frame_system` instead of `construct_runtime` and removes `Header` and `BlockNumber`

**Summary**

This code change fixes an issue related to defining parameters in `construct_runtime!`. It allows for a simplified syntax and adds types as part of `frame_system`. Additionally, it removes `BlockNumber` and `Header` from `frame_system::Config` and instead uses `Block` to retrieve them. This is a breaking change, but it is backwards compatible with a warning issued for the older syntax.

---

### [#14411](https://github.com/paritytech/substrate/pull/14411) fix(test-externalities): include memory db reference counts in snapshots

**Summary**

This code change includes memory database reference counts when the test-externalities storage is backed up and restored from snapshots.

---

### [#14318](https://github.com/paritytech/substrate/pull/14318) `pallet-message-queue`: add queue pausing

**Summary**

This code change introduces a `QueuePausedQuery` hook into the Message Queue pallet that allows for dynamically pausing queues before they start servicing. It reduces complexity and improves efficiency compared to using `Yield` or implementing `ProcessMessage` for pausing. Additionally, explicit suspension via a bool flag in `BookState` is implemented, although it is not well usable for the specific context of the code change. The changes include adding the `QueuePausedQuery` to the Message Queue pallet config, adding a new trait, and extending error types.

---

### [#14311](https://github.com/paritytech/substrate/pull/14311) migrations: `VersionedRuntimeUpgrade`

**Summary**

This code change makes it easier to write versioned runtime upgrades. It introduces a struct called `VersionedRuntimeUpgrade` that handles version handling and allows developers to write migrations without worrying about checking and setting storage versions. The struct takes five type parameters and when its `on_runtime_upgrade` method is called, it compares the on-chain version of the pallet to the version being upgraded from. If they match, the `Inner::on_runtime_upgrade` method is called and the on-chain version is set to the version being upgraded to. Otherwise, a warning is logged. The code change also includes an example and discusses the decision to keep `#[pallet::storage_version]` and use `From` and `To` instead of just `Version`. There are also some TODOs listed.

---

### [#14306](https://github.com/paritytech/substrate/pull/14306) `GenesisBuild<T,I>` deprecated. `BuildGenesisConfig` added.

**Summary**

The PR deprecates the `BuildGenesis<T,I>` trait and introduces a new non-generic trait called `BuildGenesisConfig`. The new trait is implemented for pallet's and runtime's `GenesisConfig`s and provides a single `build` function to put initial values of the genesis config into the storage. The `BuildStorage` trait is now responsible for storage building and assimilating. Some pallets were affected by this change and required the addition of `_instance` and/or `_config: PhantomData<T>` fields. The `genesis_build` macro supports both `GenesisBuild<T>` and `BuildGenesisConfig`. The `BuildStorage` trait is implemented by the `pallet` macro for each pallet's `GenesisConfig`. The `BuildGenesisConfig` is implemented for `RuntimeGenesisConfig` by the `construct_runtime` macro. Additionally, the unused `BuildModuleGenesisStorage` was deprecated and removed from macros.

---

### [#14290](https://github.com/paritytech/substrate/pull/14290) Replace system config `Index` for `Nonce`

**Summary**

This code change renames `frame_system::Config::Index` to `frame_system::Config::Nonce`. It is a breaking change that requires developers to update the implementation of `frame_system::Config` for their `Runtime`.

---

### [#14143](https://github.com/paritytech/substrate/pull/14143) Metadata V15: Expose types for the overarching Call, Event, Error enums

**Summary**

This PR introduces changes to expose the overarching types for `RuntimeEvent`, `RuntimeCall`, and `RuntimeError` for the V15 metadata. The code that generates `RuntimeEvent` is extended to also generate the `RuntimeError` enum. The construction of the runtime is changed to ensure that the `Error` enum is propagated to the metadata for each pallet that declares one. The `construct_runtime` transitioned from an implicit to an explicit state, and a new state `explicit expanded` is introduced. The `tt_extra_parts` is added to each pallet definition to create a token stream of expanded pallet parts. The PR also includes links to related PRs and issues.

---

### [#14131](https://github.com/paritytech/substrate/pull/14131) `GenesisBuilder` runtime API

**Summary**

This is a proposal for a new Runtime API called `GenesisBuilder` that allows for creating and serializing a default `GenesisConfig` to JSON, as well as deserializing and storing a `GenesisConfig` from a JSON blob. This change is related to issue [#13334](https://github.com/paritytech/substrate/issues/13334), a step towards getting rid of the native runtime.

---

### [#14123](https://github.com/paritytech/substrate/pull/14123) Metadata V15: Enrich extrinsic type info for decoding

**Summary**

Extrinsic metadata fields have been enriched to provide users with additional types for decoding extrinsics. This includes the `Address`, `Call`, `Signature`, and `Extra` types. The availability of these fields eliminates the need for manual parsing and allows for easier decoding of extrinsics. Additionally, there have been updates to the UncheckedExtrinsic type to handle cases where the runtime may have different or missing types. Subxt testing has also been implemented to ensure that the type IDs match the extrinsic type parameters.

---

### [#14120](https://github.com/paritytech/substrate/pull/14120) Introduce Pallet `paged-list`

**Summary**

Introduces a pallet called `pallet-paged-list` that provides a linked list data structure. The elements are aggregated into pages to reduce memory footprint. The API includes methods for iterating over elements, draining elements, and appending elements. Fuzzer tests are in place to test random sequences of appending and removal of elements.

---

### [#14084](https://github.com/paritytech/substrate/pull/14084) contracts: switch to wasmi gas metering

**Summary**

This code change involves several modifications:

1. The removal of uploaded Wasm blob instrumentation.
2. The elimination of storing instrumented code.
3. The removal of Wasm instruction weights in the Schedule, except for the `i64.const` instruction.
4. The removal of code caching and re-instrumentation logic.
5. The removal of the `gas` host function and the restriction on importing a function with this name in the Wasm module of a contract.
6. The addition of fuel synchronizations between the host and execution engine.
7. The inclusion of a migration process.

The fuel syncs involve two separate fuel meters, one for measuring `Weight` burn during host function execution and another for measuring Fuel burn during Wasm instruction execution. The `i64.const` instruction weight is used for conversion between the two units of measurement.

The migration process involves removing `CodeStorage` and renaming `OwnerInfo` to `CodeInfo`. It also refunds deposits attached to the freed-up storage.

The effects of this change include improved storage usage efficiency and performance, resulting in cost savings for contract authors and users.

---

### [#13950](https://github.com/paritytech/substrate/pull/13950) [FRAME Core] Adds ability to split a pallet across multiple files

**Summary**

This PR adds the ability to split components of a pallet and includes an example to demonstrate this functionality.

---

## Node SDK

Here are note-worthy **Node SDK** PRs in Substrate repo merged between 2023-06-23 and 2023-07-25.

### [#14511](https://github.com/paritytech/substrate/pull/14511) sc-cli: Remove `SubstrateCli::native_runtime_version` function

**Summary**

The native runtime will be removed, so the `native_runtime_version` function will no longer be needed. Downstream users should remove `native_runtime_version` from their implementation of the `SubstrateCli` trait.

---

### [#14508](https://github.com/paritytech/substrate/pull/14508) WasmExecutor flag to ignore onchain heappages value

**Summary**

This PR adds `ignore_onchain_heap_pages` flag to `WasmExecutorBuilder` to ignore the on-chain value of heap pages and use the default one.

---

### [#14490](https://github.com/paritytech/substrate/pull/14490) wasm-builder: Make `hash` and `date` optional

**Summary**

The code change makes the `hash` and `date` optional in certain installations.

---

### [#14474](https://github.com/paritytech/substrate/pull/14474) frame-benchmarking-cli: Remove native dispatch requirement

**Summary**

The code change removes the need to pass a generic parameter and instead allows for passing host functions directly.

---

### [#14455](https://github.com/paritytech/substrate/pull/14455) sc-network: Improve invalid boot node reporting

**Summary**

This code change improves the reporting of invalid boot nodes by only reporting each boot node once as invalid and only reporting addresses that were added as startup, not addresses learned from other nodes.

---

### [#14447](https://github.com/paritytech/substrate/pull/14447) sp-api: Support nested transactions

**Summary**

This code change adds support for nested transactions in `sp-api` by using `execute_in_transaction`. It was previously working but was unintentional. This change brings back the support for nested transactions and includes a test to ensure it does not break.

---

### [#14398](https://github.com/paritytech/substrate/pull/14398) sp-api: Put `frame-metadata` behind some feature

**Summary**

This PR put's `frame-metadata` behind a feature flag to allow for building non-FRAME runtimes that require `sp-api` without needing to build the FRAME crates.

---

### [#14387](https://github.com/paritytech/substrate/pull/14387) Removal of execution strategies

**Summary**

This PR removes the execution strategies and prepares for making `sp-api` not compile time dependent on the native runtime. It also introduces behavior changes to the runtime API, removes the `build_offchain_workers` function, and makes changes to the Grandpa and BABE client crates. Additionally, several CLI args are deprecated.

---

### [#13317](https://github.com/paritytech/substrate/pull/13317) Update Reference Hardware Specs

**Summary**

The code changes involve updating to new hardware specifications, with a slower CPU but faster disk. The benchmark results show the relative changes in performance for different operations. The disk speed values were rounded down for consistency.