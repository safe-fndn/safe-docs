---
title: Glossary of Terms and Parameters
description: This document provides definitions for all terms, parameters, and concepts used throughout the Safenet smart contract documentation.
---

## Core Concepts

### Protocol Terms

| Term | Definition |
|------|------------|
| **Safenet** | A decentralized protocol for on-chain transaction security enforcement using threshold signatures |
| **Threshold Signature** | A cryptographic scheme where `t` out of `n` participants must cooperate to create a valid signature |
| **FROST** | Flexible Round-Optimized Schnorr Threshold - the specific threshold signature protocol used ([RFC-9591](https://datatracker.ietf.org/doc/html/rfc9591)) |
| **DKG** | Distributed Key Generation - process where participants jointly create a shared key without a trusted dealer |
| **Attestation** | A FROST signature proving validators approved a transaction |

### Participant Roles

| Role | Description |
|------|-------------|
| **Validator** | A registered participant who can participate in DKG and signing ceremonies |
| **Staker/Delegator** | Someone who delegates SAFE tokens toward a validator. In Safenet a validator can stake to self. |
| **Owner** | The privileged address that can propose configuration changes |
| **Coordinator** | The FROSTCoordinator contract that orchestrates cryptographic ceremonies |

### Epoch Terminology

| Term | Definition |
|------|------------|
| **Epoch** | A period governed by a specific validator set (FROST group) |
| **Rollover** | The transition from one epoch to the next |
| **Rollover Block** | The block number at which a staged epoch becomes active |

---

## Mathematical Concepts

### Modular Arithmetic

| Operation | Description |
|-----------|-------------|
| $a \mod N$ | Remainder when $a$ is divided by $N$ |
| $a^{-1} \mod N$ | Modular multiplicative inverse (the number $b$ such that $a \cdot b = 1 \mod N$) |
| $-a \mod N$ | Computed as $N - a$ when $a > 0$ |

---

## Contract-Specific Terms

### Staking Contract

| Term | Definition |
|------|------------|
| **Stake** | SAFE tokens locked in the contract toward a validator |
| **Withdraw Delay** | Mandatory waiting period before withdrawn tokens can be claimed |
| **Withdrawal Queue** | Ordered list of pending withdrawals for a staker |
| **Withdrawal Node** | A single withdrawal request in the queue |
| **Claimable** | A withdrawal whose delay has passed and can be claimed |
| **Config Time Delay** | Mandatory waiting period for configuration changes |
| **Proposal** | A staged configuration change waiting for timelock |

---

## Mathematical Notation

| Notation | Meaning |
|----------|---------|
| $G$ | Generator point of secp256k1 |
| $N$ | Order of the curve group |
| $P$ | Field prime |
| $Y$ | Group public key |
| $Y_i$ | Participant $i$'s public key share |
| $s_i$ | Participant $i$'s signing share / secret key share |
| $n$ | Total number of participants |
| $t$ | Threshold (minimum signers required) |
| $x \cdot G$ | Scalar multiplication of $G$ by $x$ |
| $P + Q$ | Point addition |
| $\sum$ | Summation |
| $\prod$ | Product |
| $a \bmod n$ | Modular arithmetic |
| $H_{domain}(x)$ | Domain separated hash of $x$ |
| $t$-of-$n$ | Threshold scheme (t signers required out of n total) |
| $[1, N-1]$ | Range of valid scalars |
| $\xleftarrow{\$}$ | Randomly sampled from |
| $\stackrel{?}{=}$ | Verification check (equality test) |
| $\lambda_i$ | Lagrange coefficient for participant $i$ |
| $\rho_i$ | Binding factor for participant $i$ |

---

## Common Errors and Their Meanings

### Staking Errors

| Error | Meaning | Resolution |
|-------|---------|------------|
| `InvalidAmount()` | Amount is zero | Provide non-zero amount |
| `InvalidAddress()` | Address is zero | Provide valid address |
| `NotValidator()` | Not a registered validator | Stake to registered validator |
| `InsufficientStake()` | Not enough stake | Reduce withdrawal amount |
| `NoClaimableWithdrawal()` | Withdrawal not ready | Wait for delay period |

### FROST Coordinator Errors

| Error | Meaning | Resolution |
|-------|---------|------------|
| `GroupNotReady()` | Wrong phase for operation | Wait for correct phase |
| `InvalidGroupParameters()` | Bad count/threshold | Ensure count ≥ threshold > 1 |
| `InvalidSecretShare()` | Wrong number of shares | Submit count-1 shares |
| `NotSigning()` | No ceremony in progress | Start with `sign()` |
| `NotSigned()` | Signature incomplete | Wait for more shares |

### Consensus Errors

| Error | Meaning | Resolution |
|-------|---------|------------|
| `InvalidRollover()` | Bad epoch parameters | Check epoch ordering and timing |
| `NotCoordinator()` | Unauthorized callback | Only coordinator can call |
| `AlreadyAttested()` | Safe Tx is already attested | Use the existing attestation or propose a new one in next epoch |
