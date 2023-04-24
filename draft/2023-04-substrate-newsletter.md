## ⭐TL;DR and important announcements

- Data collected by SubWallet & Dotinsights showed that Polkadot nomination pools [surpassed 3M DOT](https://twitter.com/dotinsights_xyz/status/1643240360578281472) in total stake with 8K+ pool members, and Web3 Foundation Grants Program achieved [the 500 project milestone](https://twitter.com/dotinsights_xyz/status/1644281591727022080) by the end of Q1 2023.

## 📆 Upcoming events

## 🔦 Community highlights

- Co-organized by Parity & SubWallet as part of DOTinVietnam event series with the participation of Moonbeam, Litentry, ArtZero, Gafi Network, MoonFit, StellaSwap, InvArch & Polkadot Insider, Beyond The Chain Vietnam 2023 has concluded successfully with 100+ builders & developers attending to learn Polkadot & Substrate. Check out the [highlight thread](https://twitter.com/dotinvietnam/status/1645351053116964864) & [highlight video](https://www.youtube.com/watch?v=kEm42m8vDJs). 

### ink!ubator launched this month!

<img src="https://use.ink/img/twitter/inkubator-twitter.png" />

* ink!ubator is an initiative funded by the Polkadot Treasury's Bounty Program. It is designed to kickstart the ink! ecosystem  in the areas of developer growth, security audits, infrastructure, and high profile product launches. It offers grants, technical support from core developers, contract security audits, and much more. You can [apply to ink!ubator here](https://use.ink/ubator/) and follow updates on [Twitter](https://twitter.com/ink_lang).

### Blogs

* [XCM v3: Breaking New Ground for Web3 Interoperability](https://polkadot.network/blog/xcm-v3-breaking-new-ground-for-web3-interoperability/)
* [Polkadot Update: Q1 2023](https://polkadot.network/blog/polkadot-update-q1-2023/)


## 🎓 Learning

## ☕️ Technical updates

Here are note-worthy **runtime** PRs in Substrate repo merged between 2023-04-01 and 2023-04-30.

---

### [#13851](https://github.com/paritytech/substrate/pull/13851) Fix fungible and fungibles set_balance return value

There is a bug in the calculation of the return value of the `fungible` and `fungibles` `set_balance` default implementation.

The doc comment says it should return the new balance, but instead it returns `requested_balance +/- balance_change`. 

I have tests in [this PR](https://github.com/paritytech/substrate/pull/13852) that show the incorrect return value.

This test
```
cargo test --package pallet-balances -- tests::fungible_conformance_tests::set_balance_mint_success --nocapture
```

shows
```
initial_balance: 11
set_balance_amount: 16
expected_set_balance_return_value: 16
actual_set_balance_return_value: 21
```

and this test
```
cargo test --package pallet-balances -- tests::fungible_conformance_tests::set_balance_burn_success --nocapture
```

shows
```
initial_balance: 11
set_balance_amount: 6
expected_set_balance_return_value: 6
actual_set_balance_return_value: 1
```

Luckily (and I guess why this was not caught earlier), I couldn't find anywhere in Substrate or Polkadot that the return value for `set_balance` is used, so unless there is concern about ecosystem projects relying on the incorrect behavior I think this is safe to merge. 

---

### [#13835](https://github.com/paritytech/substrate/pull/13835) `RemovePallet` migration utility struct

Migration utility struct that allows easily removing pallet storage on the next runtime upgrade. 

Useful for things like removing Gov V1 pallet storage after the switch to OpenGov.

Related: https://github.com/paritytech/polkadot/issues/6749, https://github.com/paritytech/polkadot/pull/6977

---

### [#13798](https://github.com/paritytech/substrate/pull/13798) Uniform pallet warnings

Cleaning up the code a bit by using [proc-macro-warning](https://github.com/ggwpez/proc-macro-warning) and emitting a warning when using a hard-coded weight on a non-dev-mode pallet (https://github.com/paritytech/substrate/pull/13774).  
In cases where `dev` mode is not possible and you explicitly want to ignore this warning; wrap it in curly brackets like `{1}`.

This enforces consistent formatting and grammar across different warnings for enhanced developer experience.

```pre
warning: use of deprecated constant `pallet::warnings::ImplicitCallIndex::_w`: 
                 It is deprecated to use implicit call indices.
                 Please instead ensure that all calls have the `pallet::call_index` attribute or that the `dev-mode` of the pallet is enabled.
         
                 For more info see:
                     <https://github.com/paritytech/substrate/pull/12891>
                     <https://github.com/paritytech/substrate/pull/11381>
    --> frame/nomination-pools/src/lib.rs:2621:10
     |
2621 |         pub fn claim_commission(origin: OriginFor<T>, pool_id: PoolId) -> DispatchResult {
     |                ^^^^^^^^^^^^^^^^
     |
```
and
```pre
warning: use of deprecated constant `pallet::warnings::ConstantWeight::_w`: 
                 It is deprecated to use hard-coded constant as call weight.
                 Please instead benchmark all calls or put the pallet into `dev` mode.
         
                 For more info see:
                     <https://github.com/paritytech/substrate/pull/13798>
    --> frame/nomination-pools/src/lib.rs:2620:20
     |
2620 |         #[pallet::weight(0)]
     |                          
```

TODO:
- [x] Update and add UI tests

We could also think about a registry of known warnings / errors and have shortened links to them like `parity.link/frame-err-123` to explain how to resolve them.

---

### [#13779](https://github.com/paritytech/substrate/pull/13779) Add Freeze/Thaw events and tests

This PR adds a `Freeze` and `Thaw` event. The respective event is emitted whenever some balance is frozen or thawed. This is a continuation of https://github.com/paritytech/substrate/pull/12287. I decided to split PRs to maintain transparency and to not invalidate the previous audit, see https://github.com/paritytech/substrate/pull/12287#issuecomment-1483054087 for more information.

The logic remained the same as in https://github.com/paritytech/substrate/pull/12287, however two new events `Freeze` and `Thaw` were added that cover the case that `update_freezes` is invoked instead of the deprecated `update_locks`. The tests are also equal, except that the calls were adjusted to the `freeze` case. Those are the test scenarios:

```rust
Freezes = []        --> [10]      // emits Frozen(..., amount=10)
Freezes = [10]      --> [15]      // emits Frozen(..., amount=5)
Freezes = [15]      --> [15, 20]  // emits Frozen(..., amount=5)
Freezes = [15, 20]  --> [17, 20]  // emits nothing
Freezes = [17, 20]  --> [17, 15]  // emits Thawed(..., amount=3)
Freezes = [17, 15]  --> [15]      // emits Thawed(..., amount=2)
Freezes = [15]      --> []        // emits Thawed(..., amount=15)
```


I decided to follow the approach of adding new events for functionality added in the `Fungible` implementation. Now a `Lock` and `Unlock` event exists for calls into the deprecated `update_locks`, whereas `Freeze` and `Thaw` also exist to cover calls into the new `update_freezey` function. Should we move forward with that approach?


---

### [#13724](https://github.com/paritytech/substrate/pull/13724) contracts: add sr25519_verify

fix https://github.com/paritytech/substrate/issues/13703


---

### [#13722](https://github.com/paritytech/substrate/pull/13722) Implement #[pallet::composite_enum]

Partial #12918.

This PR adds a couple of new pallet parts: `FreezeReason`, `HoldReason`, `LockId` and `SlashReason`. The corresponding aggregate enums `RuntimeFreezeReason`, `RuntimeHoldReason`, `RuntimeLockId` and `RuntimeSlashReason` are also generated by `construct_runtime`. This is primarily used in pallets that wish to provide a reason for freezing funds, holding funds, locking funds and/or slashing funds in them.

`#[pallet::composite_enum]` is also added as an attribute to put on top of an enum declared in a pallet module. It now only accepts `FreezeReason`, `HoldReason`, `LockId` and `SlashReason` as identifiers for the enum; any other identifier gets rejected during pallet attribute parsing. If there are no `#[derive]` attributes marked for the enum, the code would then automatically add derives for the `Copy, Clone, Eq, PartialEq, Ord, PartialOrd, Decode, Encode, MaxEncodedLen, RuntimeDebug, TypeInfo` traits.

---

### [#13699](https://github.com/paritytech/substrate/pull/13699) Deprecate V1 Weights

First round of cleanups to get completely rid of 1D weights. The struct will be removed soon.

:rotating_light: Changes:
- Remove calls `alliance::close_old_weight` and `collective::close_old_weight`.
- Deprecate the `OldWeight` struct. Only exception is the contracts pallet where a copy of it resides.
- Remove legacy runtime API call `query_info_before_version_2`.

Polkadot companion: https://github.com/paritytech/polkadot/pull/7003  
Cumulus companion: https://github.com/paritytech/cumulus/pull/2431

---

### [#13610](https://github.com/paritytech/substrate/pull/13610) refactor: inconsistent BalanceConversion fn

Related: https://github.com/paritytech/substrate/pull/13608

## Description

Fixes an inconsistent function naming for `BalanceConversion` trait: The `fn to_asset_balance` does not align with generics `InBalance` and `OutBalance` as `to_asset_balance` implies `OutBalance` to never be the native one.

~~By fixing this, we enable to use `BalanceConversion` truly flexibly as desired, see [#13608](https://github.com/paritytech/substrate/pull/13608/files#diff-d3f111178cf5e2e266b3f267b8c6a43f808adb4237960f0241850d756b749236R165)~~

**UPDATE**: As a result of @bkchr's [remark](https://github.com/paritytech/substrate/pull/13610#discussion_r1150461400), renamed `BalanceConversion` to `ConversionToAssetBalance` and added an opposite trait `ConversionFromAssetBalance` which will be used in #13608. Basically, this applies Option B, see below.

## Alternative solutions

In case `to_asset_balance` API should not be broken, I see two alternatives:

### Option A

Add `from_asset_balance` to `BalanceConversion`:

```diff
pub trait BalanceConversion<InBalance, AssetId, OutBalance> {
	type Error;
	fn to_asset_balance(balance: InBalance, asset_id: AssetId) -> Result<OutBalance, Self::Error>;
+	fn from_asset_balance(balance: OutBalance, asset_id: AssetId) -> Result<InBalance, Self::Error>;
}
```

The downside would be that this forces the [only current implementor](https://github.com/paritytech/substrate/blob/ae83a672f2bbe6a4f7391f6a5b2b6fd7ad4f8651/frame/assets/src/types.rs#L230) of `BalanceConversion`, which is `BalanceToAssetBalance`, to implement a function which it will never use.

### Option B

* Use existing `BalanceConversion` for true `BalanceToAssetBalance` conversion and rename
* Add mirroring trait for `AssetBalanceToBalance` conversion

```diff
- pub trait BalanceConversion<InBalance, AssetId, OutBalance> {
+ pub trait BalanceToAssetBalance<InBalance, AssetId, OutBalance> {
	// snip
}

+ pub trait AssetBalanceToBalance<InBalance, AssetId, OutBalance> {
+	fn from_asset_balance(balance: InBalance, asset_id: AssetId) -> Result<OutBalance, Self::Error>;
+ }
```

The downside here is that we reduce the flexibility of this trait and create more noise.

cumulus companion: https://github.com/paritytech/cumulus/pull/2408

---

### [#13302](https://github.com/paritytech/substrate/pull/13302) Metadata V15: Add Runtime API metadata

This PR collects the runtime API information for the metadata V15 and 
exposes the metadata under `metadata_at_version(u32::MAX)`.

Considering both `sp-api` and `frame-support` crates need access to the
metadata_ir (an intermediate representation of the metadata that can be converted
into multiple metadata versions), and `frame-support` depends on `sp-api`, the
metadata_ir has been moved to `sp-api`.  

## Implementation Details

### decl_runtime_apis

Collects the runtime metadata of each declared trait using the metadata IR
and exposes the `runtime_metadata`.  The collection of the metadata happens
at this stage because it preserves trait and method documentation, as well as
method parameter names.

```rust
mod runtime_decl_for_core {
	// Metadata collected for the `Core` trait. 
	pub fn runtime_metadata<Block, ...>() -> RuntimeApiMetadataIR {
		...
	}
}
```

### impl_runtime_apis

This is the stage at which we definitely know which runtime traits are implemented for
the given Runtime. The macro collects all the `RuntimeApiMetadataIR` by calling
`runtime_metadata` of each trait. 
The `runtime_metadata` function is exposed using the `InternalImplRuntimeApis` trait. 

```rust
trait InternalImplRuntimeApis {
	fn runtime_metadata(&self) -> vec<RuntimeApiMetadataIR> {
		...
	}
}
impl InternalImplRuntimeApis for Runtime {}
```

### InternalImplRuntimeApis and InternalConstructRuntime

There are many tests that use independently just the `impl_runtime_apis` or just `construct_runtime`.
However, only the `impl_runtime_apis` has access to the runtime metadata API. 

To avoid a breaking change, the following behavior is desired:
- when only `construct_runtime` is used a `runtime_metadata` method should return an empty runtime metadata API
- when `construct_runtime` and `impl_runtime_apis` are used together, the `runtime_metadata` method should be deduced from the `impl_runtime_apis` macro

This is indeed the behavior exposed by rust unstable specialization: https://github.com/rust-lang/rust/issues/31844 feature.

One way of circumventing this is by introducing 2 traits 


```rust
trait InternalImplRuntimeApis {
	fn runtime_metadata(&self) -> vec<RuntimeApiMetadataIR> {
                actual_metadata 
	}
}

trait InternalConstructRuntime {
	fn runtime_metadata(&self) -> vec<RuntimeApiMetadataIR> {
                vec![ ]
	}
}

```
`impl_runtime_apis` implements `InternalImplRuntimeApis` on the `Runtime` itself (strongest pick by the compiler for `runtime_metadata()` fn). While `construct_runtime` implements `InternalConstructRuntime` on the `& Runtime`. 

Using the `Deref` guarantees, if we are only using `construct_runtime`: the runtime will return an empty runtime metadata (avoid breaking change). Otherwise, when implementing both traits the `runtime_metadata` is deduced to be part of the `InternalImplRuntimeApis` that contains the complete runtime metadata API.

### construct_runtime

This macro puts together the metadata IR and implements the `InternalConstructRuntime` for avoiding breaking changes.

```rust
trait InternalConstructRuntime {
	#[inline(always)]
	fn runtime_metadata(&self) ->vec<TraitMetadata> {
		...
	}
}

// Implemented for &Runtime - lower priority than InternalImplRuntimeApis
impl InternalConstructRuntime for & Runtime {}
```

```rust
let rt = Runtime;
let runtime_md = (&rt).runtime_metadata();
```

Part of: https://github.com/paritytech/substrate/issues/12939.

### Testing Done

Frame-metadata PR: https://github.com/paritytech/frame-metadata/pull/48
Subxt PoC branch for generating the runtime interface [subxt/lexnv/metadata_v15](https://github.com/paritytech/subxt/tree/lexnv/md_v15_bk), example from [subxt/lexnv/runtime_calls](https://github.com/paritytech/subxt/blob/lexnv/md_v15_bk/examples/examples/runtime_calls.rs)

```rust
    // Subxt PoC
    
    // Build payload
    let api_tx = polkadot::runtime_api::Metadata::metadata_versions();
    // Submit payload
    let bytes = api.runtime_api().at(None).await?.call(api_tx).await?;
    println!("Metadata::metadata_versions: {:?}", bytes);

    // Build payload
    let alice = AccountKeyring::Alice.to_account_id().into();
    let api_tx = polkadot::runtime_api::AccountNonceApi::account_nonce(alice);
    // Submit payload
    let bytes = api.runtime_api().at(None).await?.call(api_tx).await?;
    println!("AccountNonceApi::account_nonce: {:?}", bytes);
```


Runtime API metadata extracted from substrate for the `Metadata` trait: 

```bash
RuntimeApiMetadata {
    name: "Metadata",
    methods: [
        RuntimeApiMethodMetadata {
            name: "metadata",
            inputs: [],
            output: UntrackedSymbol {
                id: 782,
                marker: PhantomData<fn() -> core::any::TypeId>,
            },
            docs: [
                " Returns the metadata of a runtime.",
            ],
        },
        RuntimeApiMethodMetadata {
            name: "metadata_at_version",
            inputs: [
                RuntimeApiMethodParamMetadata {
                    name: "version",
                    ty: UntrackedSymbol {
                        id: 4,
                        marker: PhantomData<fn() -> core::any::TypeId>,
                    },
                },
            ],
            output: UntrackedSymbol {
                id: 783,
                marker: PhantomData<fn() -> core::any::TypeId>,
            },
            docs: [
                " Returns the metadata at a given version.",
                "",
                " If the given `version` isn't supported, this will return `None`.",
                " Use [`Self::metadata_versions`] to find out about supported metadata version of the runtime.",
            ],
        },
        RuntimeApiMethodMetadata {
            name: "metadata_versions",
            inputs: [],
            output: UntrackedSymbol {
                id: 105,
                marker: PhantomData<fn() -> core::any::TypeId>,
            },
            docs: [
                " Returns the supported metadata versions.",
                "",
                " This can be used to call `metadata_at_version`.",
            ],
        },
    ],
    docs: [
        " The `Metadata` api trait that returns metadata for the runtime.",
    ],
}

```


### Next Steps
* [x] Expose documentation under `docs` flag similar to frame
* [x] Adjust and add testing for the new metadata
* [x] Construct runtime metadata entirely in `decl_runtime_api` ([poc commit](https://github.com/paritytech/substrate/commit/78dcb673e164481df2026197b0063969a1bcac61))
* [x] Avoid breaking changes by abusing Deref ([poc commit](https://github.com/paritytech/substrate/commit/3ce25e1c013d7ea75306cd865ec925e03caa99a3))


cumulus companion: https://github.com/paritytech/cumulus/pull/2357

cc @paritytech/subxt-team 

---

Here are note-worthy **node** PRs in Substrate repo merged between 2023-04-01 and 2023-04-30.

---

### [#13925](https://github.com/paritytech/substrate/pull/13925) sc-allocator: Do not panic on invalid header pointer

We should not panic on an invalid header pointer and instead return an error. It is possible that the application modifies the header pointer illegally, but then we should return an error instead of panicking.

Closes: https://github.com/paritytech/substrate/issues/13924



---

### [#13918](https://github.com/paritytech/substrate/pull/13918) Unqueue invalid transactions when skipping

The check was intially added by: https://github.com/paritytech/substrate/pull/5121

But a later pr fixed it properly: https://github.com/paritytech/substrate/pull/9789

TLDR: We don't need to check for skipped anymore, as we already remove all transactions that are being unlocked by an invalid transactions and thus, we will not tag them as invalid directly because the nonce for example is incorrect.

Fixes: https://github.com/paritytech/substrate/issues/13911




---

### [#13917](https://github.com/paritytech/substrate/pull/13917) Drain all the pending messages in the channel when `TracingUnboundedReceiver` is dropped

Fix #13849 

`tracing_unbounded` uses `async_channel` internally, in which, the pending messages of the channel will not be dropped even if all the receivers have been dropped and these messages can never be accessed.

This may cause blocking issues when using `tracing_unbounded` to send `Sender<T>` and there is quite a lot of such usage within substrate as #13849 mentioned.

This PR fixes the issue by manually draining all the pending messages in the channel when `TracingUnboundedReceiver` is dropped and a test is added to cover the abovementioned case.

cc @bkchr 

---

### [#13824](https://github.com/paritytech/substrate/pull/13824) Make blocks per request configurable

Resolves https://github.com/paritytech/substrate/issues/10130


---

### [#13799](https://github.com/paritytech/substrate/pull/13799) Remove deprecated batch verification

This removes the deprecated batch verification. This was actually never really activated. Nevertheless, we need to keep the host functions around to support old runtimes which may import these host functions. However, we do not give access to these functions anymore. This means that any new runtime can not call them anymore. The host function implementations we keep will not do batch verification and will instead fall back to the always existing option of directly verifying the passed signature. `finish_batch_verification` will return the combined result of all the batch verify calls.

This removes the `TaskExecutorExt` which only existed to support the batch verification. So, any code that used this extension can just remove the registration of them. It also removes `SignatureBatching` that was used by `frame-executive` to control the batch verification. However, there wasn't any `Verify` implementation that called the batch verification functions.

polkadot companion: https://github.com/paritytech/polkadot/pull/6999



---

### [#13794](https://github.com/paritytech/substrate/pull/13794) Fix `try-runtime follow-chain`, try-runtime upgrade tuple tests, cli test utils

- [x] Fixes `folllow-chain` bug (closes https://github.com/paritytech/substrate/issues/13696)
- [x] Refactors existing node CLI test utility functions so that they may be used by other packages 
- [x] Adds a `follow-chain` test (related https://github.com/paritytech/substrate/issues/13796)
- [x] Adds test validating that `pre_upgrade` and `post_upgrade` hooks are executed correctly for tuple migrations (related: https://github.com/paritytech/substrate/issues/13681)

---

### [#13769](https://github.com/paritytech/substrate/pull/13769) ProofRecorder: Implement transactional support

This implements transactional support for `ProofRecorder`. A transaction can be started with `start_transaction` and then later commited or rolled back. This is important for block producers to not include data from transactions that didn't make it to the block, because they e.g. panicked or similar. 

Closes: https://github.com/paritytech/substrate/issues/10222

---

### [#13740](https://github.com/paritytech/substrate/pull/13740) refactor(sc-executor): use wasm executor builder instead of old apis

- Use the `builder` style apis to create runtime executor
- Deprecated the old `new` api for executor
- Improve and fix inconsistency about executor config(e.g. confused `max_runtime_instances`  with `runtime_cache_size`).
- Add `new_native_executor` to reduce boilerplate code.

--- 
polkadot address: 15ouFh2SHpGbHtDPsJ6cXQfes9Cx1gEFnJJsJVqPGzBSTudr

## 👀 Releases

## 📰 Substrate jobs

Have a look at all the open roles in the ecosystem on the [Substrate Job Board](https://careers.substrate.io/jobs).

Got ideas for content you’d like to see in future newsletters? Make a PR to the next edition [here](https://github.com/substrate-developer-hub/newsletter/pulls) – we’d love to include them. ❤️

_Previous editions of this newsletter are available in the public archive rendered on [this web page](https://substrate-developer-hub.github.io/newsletter/) as well as [on Polkaverse](https://polkaverse.com/10647). Join us there to comment, emote or provide feedback on our newsletters – all using a decentralised social media space built with Substrate and IPFS._
