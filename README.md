<!-- gully-header:start -->
<p align="center">
  <a href="https://gullychain.xyz">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset=".github/assets/gullychain-badge-dark.png">
      <img alt="Powered by GullyChain" src=".github/assets/gullychain-badge-light.png" width="360" height="96">
    </picture>
  </a>
</p>

<p align="center"><b>The social chain where your profile is your wallet. Arbitrum Orbit L3, testnet chain 485590.</b></p>

<p align="center">Chain Kit: Stylus SDK for Rust smart contracts on Gully Chain.</p>

<p align="center">
  <a href="https://gullychain.xyz"><img src="https://img.shields.io/badge/gullychain.xyz-01D9FA?style=for-the-badge&labelColor=000000&logo=googlechrome&logoColor=000000" alt="Website"></a>
  <a href="https://docs.gullychain.xyz"><img src="https://img.shields.io/badge/Docs-0A0F1A?style=for-the-badge&labelColor=000000&logo=readthedocs&logoColor=01D9FA" alt="Docs"></a>
  <a href="https://t.me/GullyChain"><img src="https://img.shields.io/badge/Telegram-0A0F1A?style=for-the-badge&labelColor=000000&logo=telegram&logoColor=26A5E4" alt="Telegram"></a>
  <a href="https://discord.com/invite/tY2ErsNNBp"><img src="https://img.shields.io/badge/Discord-0A0F1A?style=for-the-badge&labelColor=000000&logo=discord&logoColor=5865F2" alt="Discord"></a>
  <a href="https://x.com/Gully_Labs"><img src="https://img.shields.io/badge/@Gully__Labs-0A0F1A?style=for-the-badge&labelColor=000000&logo=x&logoColor=white" alt="X"></a>
</p>

<p align="center"><sub>A Gully Chain fork of <a href="https://github.com/OffchainLabs/stylus-sdk-rs">OffchainLabs/stylus-sdk-rs</a>, maintained by <a href="https://gullylabs.xyz">Gully Labs</a>. It is upstream publishes no licence file, so all rights stay with the upstream authors. The upstream README follows below as published. Not affiliated with or endorsed by OffchainLabs.</sub></p>

---
<!-- gully-header:end -->

<br />
<p align="center">
  <a href="https://arbitrum.io/">
    <img src="https://arbitrum.io/assets/stylus/stylus_with_paint_bg.png" alt="Logo" width="100%">
  </a>

  <h3 align="center">The Stylus SDK</h3>

  <p align="center">
    <a href="https://docs.arbitrum.io/stylus/gentle-introduction"><strong>Rust contracts on Arbitrum »</strong></a>
    <br />
  </p>
</p>

## Overview

The Stylus SDK enables smart contract developers to write programs for **Arbitrum chains** written in the [Rust](https://www.rust-lang.org/tools/install) programming language. Stylus programs are compiled to [WebAssembly](https://webassembly.org/) and can then be deployed on-chain to execute alongside Solidity smart contracts. Stylus programs are not only orders of magnitude cheaper and faster but also enable what was thought to be previously impossible for WebAssembly: **EVM-interoperability**.

For information about deploying Rust smart contracts, see the [Cargo Stylus CLI Tool](https://github.com/OffchainLabs/stylus-sdk-rs/tree/main/cargo-stylus). For more information about Stylus, see [Stylus: A Gentle Introduction](https://docs.arbitrum.io/stylus/gentle-introduction). For a simpler intro to Stylus Rust development, see the [Quick Start guide](https://docs.arbitrum.io/stylus/quickstart).

Comprehensive documentation on the Rust SDK can be found [here](https://docs.arbitrum.io/stylus/rust-sdk-guide).

## Feature highlights

The SDK makes it easy to develop Ethereum ABI-equivalent Stylus contracts in Rust. It provides a full suite of types and shortcuts that abstract away the details of Ethereum's storage layout, making it easy to _just write Rust_. For an in depth exploration of the features, please see comprehensive [Feature Overview][overview].

Some of the features available in the SDK include:

- **Generic**, storage-backed Rust types for programming **Solidity-equivalent** smart contracts with optimal storage caching.
- Simple macros for writing **language-agnostic** methods and entrypoints.
- Automatic export of Solidity interfaces for interoperability across programming languages.
- Powerful **primitive types** backed by the feature-rich Alloy.

Rust programs written with the Stylus SDK can call and be called by Solidity smart contracts due to ABI equivalence with Ethereum programming languages. In fact, existing Solidity DEXs can list Rust tokens without modification, and vice versa.

```rust
use stylus_sdk::{alloy_primitives::U256, prelude::*};

// Generate Solidity-equivalent, Rust structs backed by storage.
sol_storage! {
  #[entrypoint]
  pub struct Counter {
    uint256 number;
  }
}

#[public]
impl Counter {
  // Gets the number value from storage.
  pub fn number(&self) -> Result<U256, Vec<u8>> {
    Ok(self.number.get())
  }

  // Sets a number in storage to a user-specified value.
  pub fn set_number(&mut self, new_number: U256) -> Result<(), Vec<u8>> {
    self.number.set(new_number);
    Ok(())
  }
}
```

Additionally, the Stylus SDK supports `#[no_std]` for contracts that wish to opt out of the standard library. In fact, the entire SDK is available from `#[no_std]`, so no special feature flag is required. This can be helpful for reducing binary size, and may be preferable in pure-compute use cases like cryptography.

Most users will want to use the standard library, which is available since the Stylus VM supports `rustc`'s `wasm32-unknown-unknown` target triple. In the future we may add `wasm32-wasi` too, along with floating point and SIMD, which the Stylus VM does not yet support.

[overview]: https://docs.arbitrum.io/stylus/reference/rust-sdk-guide

## Don't know Rust?

The Stylus VM supports more than just Rust. In fact, any programming language that compiles down to WebAssembly could in principle be deployed to Stylus-enabled chains. The table below includes the official ports of the SDK, with more coming soon.

| Repo             | Use cases                   | License           |
|:-----------------|:----------------------------|:------------------|
| [Rust SDK][Rust] | Everything!                 | Apache 2.0 or MIT |
| [C/C++ SDK][C]   | Cryptography and algorithms | Apache 2.0 or MIT |
| [AssemblyScript SDK][AssemblyScript]* | Educational | Apache 2.0 or MIT |
| [Bf SDK][Bf]     | Educational                 | Apache 2.0 or MIT |
| [Cargo Stylus][CargoStylus]     | Deploying Stylus programs | Apache 2.0 or MIT |

Want to write your own? [Join us in the `#stylus` channel on discord][discord]!

_*This SDK is developed and maintained by an independent team._

[Rust]: https://github.com/OffchainLabs/stylus-sdk-rs
[C]: https://github.com/OffchainLabs/stylus-sdk-c
[AssemblyScript]: https://github.com/wakeuplabs-io/assembly-script-stylus-sdk
[Bf]: https://github.com/OffchainLabs/stylus-sdk-bf

[discord]: https://discord.com/invite/5KE54JwyTs

## Developing Stylus Programs

The Stylus SDK is just one of the building blocks in creating and deploying WebAssembly programs to Arbitrum chains. To create a new Stylus project from a hello-world example and deploy it onchain, check out some of our tools below:

| Repo             | Use cases                   | License           |
|:-----------------|:----------------------------|:------------------|
| [Stylus Hello World][HelloWorld]     | Rust Stylus starter template | Apache 2.0 or MIT |
| [Cargo Stylus CLI][CargoStylus]     | Deploying Stylus programs | Apache 2.0 or MIT |

[HelloWorld]: https://github.com/OffchainLabs/stylus-hello-world
[CargoStylus]: https://github.com/OffchainLabs/stylus-sdk-rs/tree/main/cargo-stylus

## License

&copy; 2022-2024 Offchain Labs, Inc.

This project is licensed under either of

- [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0) ([licenses/Apache-2.0](licenses/Apache-2.0))
- [MIT license](https://opensource.org/licenses/MIT) ([licenses/MIT](licenses/MIT))

at your option.

The [SPDX](https://spdx.dev) license identifier for this project is `MIT OR Apache-2.0`.


<!-- gully-footer:start -->
---

<p align="center">
  <a href="https://gullylabs.xyz">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset=".github/assets/powered-by-gully-labs-dark-2x.png">
      <img alt="Powered by Gully Labs" src=".github/assets/powered-by-gully-labs-light-2x.png" width="254" height="64">
    </picture>
  </a>
</p>
<!-- gully-footer:end -->
