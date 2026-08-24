<p align="center">
  <img src="https://github.com/Paxeer-Network/.github/blob/main/blocks.png?raw=true" alt="Paxeer Network" width="1200">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Chain_ID-125-00B4D8?style=for-the-badge" alt="Chain ID 125" />
  <img src="https://img.shields.io/badge/Cosmos-hyperpax__125--1-111827?style=for-the-badge" alt="Cosmos chain id" />
  <img src="https://img.shields.io/badge/LayerX-Limited_beta_Sept_7-7c3aed?style=for-the-badge" alt="LayerX beta" />
</p>

<h1 align="center">Paxeer Network</h1>

<p align="center">
  <strong>The settlement layer for machine commerce.</strong><br />
  An EVM L1 (chain ID <code>125</code>) where agents hold policy-bound wallets, pay for work, and leave a record they cannot rewrite.
</p>

<p align="center">
  <a href="https://paxeer.app">paxeer.app</a> ·
  <a href="https://layerx.paxeer.app">LayerX</a> ·
  <a href="https://paxscan.io">Paxscan</a> ·
  <a href="https://github.com/Sidiora-Labs/LayerX-Protocol">LayerX Protocol</a>
</p>

---

## What this org is

Paxeer is the chain. **LayerX** is the fast activity lane that sits on it.

| Layer | Owns |
| --- | --- |
| **Paxeer L1** | Custody, checkpoints, guarantor bonds, challenges, withdrawals, emergency exits |
| **LayerX** | Identity, delegated authority, global ordering, balances, payments, agreements, trading, receipts, replay |

Thousands of LayerX activities can collapse into one periodic checkpoint. A normal agent payment does not require a Paxeer transaction. Custody never leaves Paxeer.

LayerX is **source-available** and in **limited beta** (opens September 7). There is no public LayerX RPC, faucet, or explorer yet — and **no LayerX token**. Agents hold **USDX** inside LayerX; **USDL** backs it one-for-one on this L1; **HPX / PAX** is Paxeer gas.

---

## Network

| | |
| --- | --- |
| **EVM chain ID** | `125` |
| **Cosmos chain ID** | `hyperpax_125-1` |
| **Public RPC** | `https://public-rpc.paxeer.app/rpc` |
| **Explorer** | [paxscan.io](https://paxscan.io) |
| **Bech32 prefix** | `pax` |
| **Native gas** | HPX (`ahpx`, 18 decimals) — also called PAX on LayerX surfaces |
| **Runtime** | `hyperpaxd` (Alexandria Fork) |

April 2026 performance report ([`paxeer-performance-report`](https://github.com/Paxeer-Network/paxeer-performance-report)): 10 validators, 48 RPC nodes, 14 regions, **277 ms** average block time (341 ms p95).

```json
{
  "networkName": "HyperPaxeer",
  "rpcUrl": "https://public-rpc.paxeer.app/rpc",
  "chainId": 125,
  "cosmosChainId": "hyperpax_125-1",
  "baseDenom": "ahpx",
  "displayDenom": "hpx",
  "decimals": 18,
  "bech32Prefix": "pax",
  "blockExplorer": "https://paxscan.io"
}
```

Add the chain in MetaMask / any EVM wallet with those fields. Standard tooling works: Foundry, Hardhat, wagmi, viem, ethers.

---

## Architecture

Paxeer pairs a production **EVM** execution layer with the **Argus Virtual Machine** (AVM) — a C++ register-based runtime for risk, capital allocation, and funded smart-wallet management.

```
                    Paxeer Network
+----------------------+      +----------------------+
|     EVM OS layer     |      |     Argus VM (AVM)   |
|    Alexandria Fork   |      |   C++ runtime, .avm  |
|  Solidity contracts  |      |  Risk + capital      |
|  Custom precompiles  |      |  Funded smart wallet |
|  0x901–0x904         |      |  ArgLang (.arg)      |
+----------------------+      +----------------------+
         CometBFT  ·  Cosmos SDK  ·  IBC
```

The EVM is the shell (consensus, networking, JSON-RPC). The AVM is the value engine. They meet at on-chain contract boundaries.

**LayerX** is not a general-purpose rollup. It is the agent activity layer: one signed record per action (LXC/1), eight protocol modules, and **402LXP** as the only balance writer. You pay for work done (bytes, signatures, state) — specified base fee **5,000 µUSDX** (~½¢). Finality is L0→L4 onto this chain. The guarantee behind a batch is bonded re-execution, not a validity proof.

---

## Start here

| Repo | What it is |
| --- | --- |
| [`hyperpaxeer-os`](https://github.com/Paxeer-Network/hyperpaxeer-os) | HyperPaxeer runtime / node |
| [`paxeer-performance-report`](https://github.com/Paxeer-Network/paxeer-performance-report) | April 2026 network report |
| [`Paxeer-Smart-Contract-SDK`](https://github.com/Paxeer-Network/Paxeer-Smart-Contract-SDK) | Solidity building blocks |
| [`Paxeer-Token-Registry`](https://github.com/Paxeer-Network/Paxeer-Token-Registry) | Token registry |
| [`paxport-android-apk`](https://github.com/Paxeer-Network/paxport-android-apk) | Paxport — self-custody wallet |
| [`Paxeer-Network-Brand-Kit`](https://github.com/Paxeer-Network/Paxeer-Network-Brand-Kit) | Brand |
| [`Sidiora-Labs/LayerX-Protocol`](https://github.com/Sidiora-Labs/LayerX-Protocol) | LayerX node, spec, SDKs, MCP (source-available) |
| [LayerX wiki](https://github.com/Sidiora-Labs/LayerX-Protocol/wiki) | Protocol, modules, fees, status |

Markets and applications live in this org too (spot, perps, launchpad, options, oracles). Prefer the current runtime and the LayerX protocol repo over archived `Pax-v1-*` trees.

---

## LayerX, plainly

- Limited beta opens **September 7**.
- Source is open for inspection while we qualify the public lane.
- No public LayerX RPC / faucet / explorer yet.
- No LayerX token and no token sale.
- License during development is inspection-only; broader license after qualification. See the [LayerX LICENSE](https://github.com/Sidiora-Labs/LayerX-Protocol/blob/main/LICENSE).

If a page claims “LayerX is live,” “zero LayerX fees,” or a LayerX token, it is not from this org or Sidiora Labs.

---

## Which Paxeer / LayerX?

This organization is **Paxeer Network** (EVM `125`), specified with LayerX as **LXP1** by [Sidiora Labs](https://github.com/Sidiora-Labs).

Ours: [paxeer.app](https://paxeer.app) · [layerx.paxeer.app](https://layerx.paxeer.app) · [sidiora.xyz](https://sidiora.xyz) · [github.com/Sidiora-Labs](https://github.com/Sidiora-Labs)

Other companies use these names. A page that does not trace back to one of those is a different project.
