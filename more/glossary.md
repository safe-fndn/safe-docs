---
title: "Glossary"
description: "Definitions of terms and concepts used throughout the Safe documentation."
---

## Account Abstraction

Account Abstraction is a paradigm aimed at improving the blockchain user experience by replacing the reliance on [externally-owned accounts](#externally-owned-account) (EOAs) with programmable [smart accounts](#smart-account).

Key benefits of Account Abstraction include:
- Elimination of seed phrase reliance
- Improved multi-chain interactions
- Account recovery mechanisms
- [Gasless transactions](#gasless-transaction)
- Transaction batching

See also:
- [Ethereum Account Abstraction roadmap](https://ethereum.org/en/roadmap/account-abstraction)
- [ERC-4337: Account Abstraction](https://www.erc4337.io)

---

## Bundler

Bundlers are specialized nodes defined by the [ERC-4337](#erc-4337) standard. They collect [UserOperation](#useroperation) objects from a dedicated mempool, bundle them together, and submit them to the blockchain via the [EntryPoint](#entrypoint) contract.

Bundlers initially pay the transaction fees and are later reimbursed by the user’s smart account or a [Paymaster](#paymaster).

See also:
- [ERC-4337 bundling process](https://eips.ethereum.org/EIPS/eip-4337#bundling)
- [Bundlers documentation](https://docs.erc4337.io/bundlers)

---

## ERC-1271

[ERC-1271](https://eips.ethereum.org/EIPS/eip-1271) defines a standard interface that allows smart contracts to validate signatures. A contract implementing ERC-1271 exposes an `isValidSignature(hash, signature)` function that returns whether a given signature is valid for that contract.

This enables smart accounts to participate in signature-based authentication flows.

---

## ERC-712

[ERC-712](https://eips.ethereum.org/EIPS/eip-712) specifies a standard for hashing and signing typed structured data, making signed messages more readable and secure compared to raw bytestring signing.

---

## EntryPoint

The EntryPoint is a singleton smart contract defined by [ERC-4337](#erc-4337). It is responsible for validating and executing bundles of [UserOperation](#useroperation) objects submitted by [Bundlers](#bundler).

See also:
- [EntryPoint specification](https://eips.ethereum.org/EIPS/eip-4337#entrypoint-definition)

---

## ERC-4337

[ERC-4337](https://eips.ethereum.org/EIPS/eip-4337) introduces Account Abstraction without requiring changes to Ethereum’s consensus layer. It defines a new pseudo-transaction object called `UserOperation` and a dedicated mempool.

[Bundlers](#bundler) aggregate UserOperations and submit them to the blockchain via the [EntryPoint](#entrypoint) contract.

See also:
- [ERC-4337 documentation](https://www.erc4337.io)

---

## Externally-Owned Account

An externally-owned account (EOA) is one of the two Ethereum account types. EOAs are controlled by a private key, contain no executable code, and initiate transactions by signing them directly.

See also:
- [Ethereum accounts](https://ethereum.org/en/developers/docs/accounts)
- [Ethereum whitepaper – accounts](https://ethereum.org/en/whitepaper/#ethereum-accounts)

---

## Gasless Transaction

Gasless transactions (also called meta-transactions) allow users to interact with the blockchain without directly paying gas fees. Instead, a third party—commonly a [Relayer](#relayer) or a [Paymaster](#paymaster)—submits and pays for the transaction on the user’s behalf.

Users sign a message describing the desired action, while the relayer constructs and executes the on-chain transaction.

---

## Multi-signature

A multi-signature account is a type of [smart account](#smart-account) that requires approvals from multiple owners to execute transactions. Owners can be [externally-owned accounts](#externally-owned-account) or other smart accounts.

### Common configurations

- **0/0 Safe**  
  An account with no owners, fully controlled by [Safe Modules](#safe-module). Commonly used for automation.

- **1/1 Safe**  
  A single-owner account. Simple to manage but requires a recovery plan in case the owner loses access.

- **N/N Safe**  
  All owners must approve each transaction. Offers strong shared control but requires careful key management.

- **N/M Safe**  
  Only a subset of owners must approve transactions, balancing security and flexibility.

### How it works

- Owners and thresholds are stored on-chain.
- Transactions include signatures from the required owners.
- The Safe contract verifies signatures before execution.

### Benefits

- **Enhanced security** through reduced single points of failure
- **Flexible ownership** and threshold configuration
- **Broad wallet compatibility**, including:
  - Hardware wallets (Ledger, Trezor)
  - Software wallets (MetaMask, Trust Wallet)
  - MPC wallets (Fireblocks, Zengo)
  - Other smart accounts
  - Social login or passkey-based wallets
- **Upgradability**, including owner and threshold changes
- **Auditability** of all executed transactions

---

## Network

A blockchain network is a distributed system of nodes that maintain a shared ledger using a consensus mechanism. Networks enable decentralized transaction execution without a central authority.

See also:
- [Ethereum networks](https://ethereum.org/en/developers/docs/networks)

---

## Owner

A Safe owner is an account authorized to manage a Safe and approve transactions. Owners can be EOAs or smart accounts. The [threshold](#threshold) determines how many owner approvals are required.

See also:
- [OwnerManager.sol](https://github.com/safe-fndn/safe-smart-account/blob/main/contracts/base/OwnerManager.sol)

---

## Paymaster

Paymasters are smart contracts that sponsor gas fees for users under [ERC-4337](#erc-4337). They can enable gasless experiences or allow gas payments using ERC-20 tokens.

See also:
- [ERC-4337 Paymasters](https://eips.ethereum.org/EIPS/eip-4337#extension-paymasters)
- [Paymasters documentation](https://docs.erc4337.io/paymasters)

---

## Relayer

A relayer is a third-party service that submits transactions to the blockchain on behalf of users, often paying gas costs upfront.

See also:
- [What is relaying?](https://docs.gelato.network/developer-services/relay/what-is-relaying)

---

## Safe{DAO}

Safe{DAO} is a decentralized autonomous organization that governs and supports the Safe ecosystem through grants, governance, and ecosystem investments.

See also:
- [Safe{DAO} Forum](https://forum.safe.global)
- [Governance process](https://forum.safe.global/t/how-to-safedao-governance-process/846)
- [Proposals on Snapshot](https://snapshot.org/#/safe.eth)

---

## Safe{Wallet}

[Safe{Wallet}](https://app.safe.global) is the official interface for creating and managing Safe accounts.

See also:
- [Getting started with Safe{Wallet}](https://help.safe.global/en/collections/9801-getting-started)

---

## Safe Apps

Safe Apps are third-party web applications integrated into the Safe Apps marketplace. They interact with Safe accounts via the Safe Apps SDK and are not owned or audited by Safe.

See also:
- [Safe Apps SDK](https://github.com/safe-global/safe-apps-sdk)

---

## Safe Guard

A Safe Guard is a smart contract that adds pre- and post-execution checks to Safe transactions.

See also:
- [Safe Guards documentation](/smart_account/guards)
- [Zodiac Guards](https://zodiac.wiki/index.php%3Ftitle=Introduction:_Zodiac_Protocol.html#Guards)

---

## Safe Module

A Safe Module is a smart contract that extends Safe functionality while keeping core contracts minimal.

See also:
- [Safe Modules documentation](/smart_account/modules)
- [Safe Modules repository](https://github.com/safe-fndn/safe-modules)
- [Zodiac Modules](https://zodiac.wiki/index.php%3Ftitle=Introduction:_Zodiac_Protocol.html#Modules)

---

## Smart Account

A smart account is a smart-contract-based account that provides enhanced security and programmability compared to EOAs. Transactions are executed according to on-chain logic rather than a single private key.

Common features include:
- [Multi-signature](#multi-signature)
- Transaction batching
- Account recovery
- [Gasless transactions](#gasless-transaction)

Safe is a widely adopted implementation of smart accounts.

---

## Transaction

A transaction updates blockchain state and is typically initiated by an [externally-owned account](#externally-owned-account).

A Safe transaction is executed via the Safe contract’s `execTransaction` function.

See also:
- [Ethereum transactions](https://ethereum.org/developers/docs/transactions)

---

## Threshold

The threshold defines how many owner approvals are required to execute a Safe transaction.

---

## UserOperation

`UserOperation` is a pseudo-transaction type introduced by [ERC-4337](#erc-4337). UserOperations are sent to a dedicated mempool and executed through the [EntryPoint](#entrypoint) contract.

See also:
- [UserOperation specification](https://eips.ethereum.org/EIPS/eip-4337#useroperation)
- [UserOperation mempool](https://docs.erc4337.io/bundlers/userop-mempool-overview)

---

## Wallet

A wallet is an application or interface that allows users to manage blockchain accounts, sign messages, and submit transactions.

See also:
- [Ethereum wallets](https://ethereum.org/wallets)
