This page contains summaries of the merged PRs into Substrate organized in two sections: "Runtime" (using the `B1-note_worthy` + `T1-runtime` labels) and "Node SDK" (using the `B1-note_worthy` + `T0-node` labels).
Read more about how Substrate uses labels [here](https://github.com/paritytech/substrate/blob/master/docs/CONTRIBUTING.adoc#merge-process).

## Runtime

Here are note-worthy **Runtime** PRs in Substrate repo merged between 2023-07-26 and 2023-08-21.

### [#14793](https://github.com/paritytech/substrate/pull/14793) fix: `try_on_runtime_upgrade` for `Tuple` weight summation 

**Summary**

Updates the `try_on_runtime_upgrade` implementation to increment the cumulative weights.

---

### [#14773](https://github.com/paritytech/substrate/pull/14773) Improve `storage_alias` and make `UnlockAndUnreserveAllFunds` independent of the pallet

**Summary**

This pull request improves the `storage_alias` by making it more generic over the prefix to use. It also makes `pallet_democracy::UnlockAndUnreserveAllFunds` independent of the presence of the `pallet-democracy` pallet. Additionally, it puts some tests in `frame-support` into their own file to clean up the `lib.rs`.

---

### [#14740](https://github.com/paritytech/substrate/pull/14740) Update Scheduler Pallet Documentation

**Summary**

This code change updates the documentation of the Scheduler Pallet and adds a warning section to inform users of anti-patterns when scheduling runtime calls.

---

### [#14706](https://github.com/paritytech/substrate/pull/14706) Remove deprecated old weight items

**Summary**

The PR removes the deprecated weight implementation.

---

### [#14685](https://github.com/paritytech/substrate/pull/14685) [FRAME] Remove V1 Module Syntax

**Summary**

The changes include removing the `decl_` macro syntax and moving `no_bound` derives to their own folder.

---

### [#14678](https://github.com/paritytech/substrate/pull/14678) Cross-contract calling: simple debugger

**Summary**

This code change aims to provide insights into the internals of the contracts pallet by adding breakpoints before and after an `Executable` object is invoked. The intention is to achieve a more interactive debugging experience, particularly in environments where there is direct access to the runtime. The plan is to add more breakpoints in the future to provide additional information.

---

### [#14589](https://github.com/paritytech/substrate/pull/14589) Contracts remove deposit accounts

**Summary**

This PR removes deposit accounts in the Contracts pallet and updates the migrations to be backwards compatible. A new migration is added to move the balance from the deposit accounts back to the contract accounts.

---

### [#14538](https://github.com/paritytech/substrate/pull/14538) Pallets: Treasury deprecate `propose_spend` dispatchable

**Summary**

This PR deprecates the `propose_spend` dispatchable and its dependent dispatchables, `reject_proposal` and `approve_proposal`, in favor of using the `spend` dispatchable.

---

### [#14453](https://github.com/paritytech/substrate/pull/14453) add `frame_system::DefaultConfig` to individual pallet `DefaultConfigs`

**Summary**

This code change modifies the `DeriveImpl` experimental feature to generate a trait that extends `frame_system::DefaultConfig` if the `trait Config` is bound by `frame_system::Config` and provides examples of its use in the test files of the Proxy and Multisig pallets. This update allows types reliant on `frame_system::Config` to have defaults if they are present in `frame_system::DefaultConfig`.

---

### [#14079](https://github.com/paritytech/substrate/pull/14079) Contracts: Add deposit for dependencies

**Summary**

This code change introduces two new runtime functions, `add_delegate_dependency` and `remove_delegate_dependency`, to prevent a contract from being removed when invoked via `delegate_call`. It also adds new configuration fields, `MaxDelegateDependencies` and `CodeHashLockupDepositPercent`, to control the maximum number of delegate dependencies and the percentage of the storage deposit required for using a code hash.

---

### [#14020](https://github.com/paritytech/substrate/pull/14020) Contracts: migrate to fungible traits

**Summary**

The `Currency` and `ReservableCurrency` traits are deprecated in favor of the `fungible` traits. The `ReservableCurrency::reserve` and `ReservableCurrency::unreserve` functions are replaced with `fungible::hold::Mutate::hold` and `fungible::hold::Mutate::release`, respectively. Holds are now explicitly designed to be infallibly slashed and require a provider reference. They also require an identifier that is configurable and expected to be an enum aggregated across all pallet instances of the runtime. Some events have been changed due to the changes from `reserve/unreserve` to `hold/release`. The `ExistenceRequirement` enum is replaced by `Preservation`. The `Currency::transfer()` function no longer performs the sanity check it used to, so the sanity check is now addressed before calling `Currency::transfer()`. The `pallet_contracts::Config` trait now requires a new type `RuntimeHoldReason`. The `construct_runtime` macro needs `pallet_contracts::HoldReason`. Some migrations require a generic `OldCurrency` that implements the traits that the previous `T::Currency` implemented. After this PR, deposit accounts are no longer needed as the new "held" balance does not contribute to the ED. This PR does not alter the deposit accounts and its functionality.

---

### [#12970](https://github.com/paritytech/substrate/pull/12970) [NPoS] Implements dynamic number of nominators

**Summary**

This PR refactors the implementation of the `ElectionDataProvider` bounds and implements a dynamic nomination quota per voter. It introduces a new trait `NominationsQuota` and a struct `FixedNominationsQuota` to set the maximum number of nominations per nominator. The PR also introduces an `ElectionSizeTracker` to keep track of the size of the snapshot and ensures that it is bounded. The `ElectionBounds` struct replaces `MaxElectableTargets` and `TargetsBound` to define the count and size limits of voters and targets for an election. The `ElectionDataProvider` interface is modified to take an instance of `DataProviderBounds` as input. New events and a runtime API are also added.

---

### [#10621](https://github.com/paritytech/substrate/pull/10621) CountedNMap implementation

**Summary**

A new implementation called `CountedStorageNMap` is added for `StorageNMap`, similar to what `CountedStorageMap` is to `StorageMap`.

---

## Node SDK

Here are note-worthy **Node SDK** PRs in Substrate repo merged between 2023-07-26 and 2023-08-21.

### [#14731](https://github.com/paritytech/substrate/pull/14731) deprecate `try-runtime` subcommand and direct users to standalone cli

**Summary**

The `try-runtime` subcommand has been migrated to a standalone CLI. Tests have been removed to reduce load on the CI and have been migrated to the new repository.

---

### [#14612](https://github.com/paritytech/substrate/pull/14612) Set `StateBackend::Transaction` to `PrefixedMemoryDB`

**Summary**

This pull request removes the `Transaction` associated type from `sp_state_machine::Backend` and fixes it to `PrefixedMemoryDB`. It also moves the "storage transaction cache" into `OverlayedChanges` to simplify the code. Downstream code changes include removing references to `TransactionFor` and `StateBackend::Transaction`, and changing `BlockImportParams` and `DefaultImportQueue` to only take one generic argument.

---

### [#14412](https://github.com/paritytech/substrate/pull/14412) Bandersnatch VRF

**Summary**

This PR introduces a new kind of VRF called _bandersnatch-vrfs_, which can operate as a classical VRF or as a ring VRF. The code has been partially extracted from the Sassafras PR and is still an experimental feature. There are open points regarding dependencies on bandersnatch-vrfs, fflonk, and ring-proof.

---

### [#14337](https://github.com/paritytech/substrate/pull/14337) Get rid of `Peerset` compatibility layer

**Summary**

The code changes eliminate `Peerset` and instead give handles to `PeerStore` and `ProtocolController` to the components that need them. This resolves an issue with peer counting in `Protocol` and clarifies that `self.peers` only contains peers on the default protocol.