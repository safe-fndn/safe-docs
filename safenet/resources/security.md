---
title: Security
description: Deployed contracts, source code, audit reports, and what is immutable vs configurable in Safenet Beta.
---

Safenet Beta is built on three smart contracts. The Staking contract lives on Ethereum Mainnet and holds staked SAFE tokens. The Consensus and FROSTCoordinator contracts live on Gnosis Chain and handle transaction attestation and threshold signing.

## Deployed contracts

| Contract | Chain | Address | Source | Audit |
|---|---|---|---|---|
| Staking | Ethereum Mainnet | [`0x115E78f160e1E3eF163B05C84562Fa16fA338509`](https://etherscan.io/address/0x115E78f160e1E3eF163B05C84562Fa16fA338509) | [Staking.sol](https://github.com/safe-research/safenet/blob/beta/contracts/src/Staking.sol) | [Report](https://github.com/safe-research/safenet/blob/beta/contracts/audits/audit.md) |
| Consensus | Gnosis Chain | TODO | [Consensus.sol](https://github.com/safe-research/safenet/blob/main/contracts/src/Consensus.sol) | **Not audited** |
| FROSTCoordinator | Gnosis Chain | TODO | [FROSTCoordinator.sol](https://github.com/safe-research/safenet/blob/beta/contracts/src/FROSTCoordinator.sol) | **Not audited** |

<Note>
Consensus and FROSTCoordinator contract addresses will be added once deployed.
</Note>

Both Consensus and FROSTCoordinator contracts are non-upgradeable and hold **no user funds**.

## Immutability and parameters

**Staking contract**

The Staking contract has an owner (the SafeDAO via the Safe Ecosystem Foundation) but is not upgradeable. The owner can propose changes to two parameters. All proposed changes go through a mandatory 7-day timelock before taking effect. After the timelock, anyone can execute the queued change.

| Parameter | Current value | Mutable | Who can propose | Constraint |
|---|---|---|---|---|
| `SAFE_TOKEN` | [SAFE on Mainnet](https://etherscan.io/token/0x5afe3855358e112b5647b952709e6165e1c1eeee) | No | — | — |
| `CONFIG_TIME_DELAY` | 7 days | No | — | — |
| `withdrawDelay` | 2 days | Yes | Contract owner (SafeDAO/SEF) | Max value capped at `CONFIG_TIME_DELAY` (7 days); 7-day timelock before change takes effect |
| Validator registry | Permissioned set | Yes | Contract owner (SafeDAO/SEF) | 7-day timelock before changes take effect |

The owner can also recover tokens accidentally sent to the contract, but cannot access staked SAFE or tokens in the withdrawal queue.

The Staking contract has been independently formally verified and audited by [Certora](https://www.certora.com/). See the [full report](https://github.com/safe-research/safenet/blob/beta/contracts/audits/audit.md) for details.

**Consensus and FROSTCoordinator contracts**

Both contracts are non-upgradeable and have no owner. There are no admin functions and no configurable parameters.

Validator Staker addresses in the Consensus contract are self-set by each Validator. Epoch transitions (changes to the active Validator set) require a threshold signature from the current Validator set, not any central authority.

<Note>
    In case there is an unrecoverable failure in Safenet Beta, both contracts have to be redeployed and the network needs to be relaunched.
</Note>
