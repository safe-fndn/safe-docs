---
title: Overview
description: This documentation covers the onchain smart contract infrastructure that powers Safenet.
---

## Core Contracts

### 1. [Staking Contract](/safenet/protocol/staking)
**Purpose**: Manages validator registration and SAFE token staking.

| Aspect | Description |
|--------|-------------|
| Token | SAFE (ERC-20) |
| Role | Economic security layer |
| Key Feature | Timelocked withdrawals |
| Access Control | Owner-governed with public execution |

**Key Operations**:
- Stake tokens toward validators
- Initiate and claim withdrawals
- Register/deregister validators (owner)

### 2. [FROST Coordinator Contract](/safenet/protocol/frost-coordinator)
**Purpose**: Orchestrates distributed key generation (DKG) and threshold signing ceremonies.

| Aspect | Description |
|--------|-------------|
| Protocol | FROST (RFC-9591) |
| Curve | secp256k1 |
| Role | Cryptographic coordination |
| Key Feature | onchain signature aggregation |

**Key Operations**:
- Distributed Key Generation (DKG)
- Nonce preprocessing
- Signature share collection and aggregation

### 3. [Consensus Contract](/safenet/protocol/consensus)
**Purpose**: Manages validator epochs and transaction attestations.

| Aspect | Description |
|--------|-------------|
| Role | Protocol state machine |
| Key Feature | Epoch-based validator rotation |
| Integration | Calls FROSTCoordinator for signatures |

**Key Operations**:
- Propose and stage new epochs
- Propose transactions for validation
- Record attestations

---

## Contract Interactions

```mermaid
sequenceDiagram
    participant Owner
    participant Staker
    participant Validator
    participant Staking
    participant FROSTCoordinator
    participant Consensus
    
    Note over Owner,Staking: Setup Phase
    Owner->>Staking: proposeValidators()
    Owner->>Staking: executeValidatorChanges()
    Staker->>Staking: stake(validator, amount)
    
    Note over Validator,FROSTCoordinator: Key Generation Phase
    Validator->>FROSTCoordinator: keyGenAndCommit()
    Validator->>FROSTCoordinator: keyGenSecretShare()
    Validator->>FROSTCoordinator: keyGenConfirmWithCallback()
    FROSTCoordinator->>Consensus: onKeyGenCompleted()
    
    Note over Validator,Consensus: Signing Phase
    Validator->>FROSTCoordinator: preprocess() [nonces]
    Validator->>Consensus: proposeTransaction()
    Consensus->>FROSTCoordinator: sign()
    Validator->>FROSTCoordinator: signRevealNonces()
    Validator->>FROSTCoordinator: signShareWithCallback()
    FROSTCoordinator->>Consensus: onSignCompleted()
    Consensus->>Consensus: attestTransaction()
```

---

## Related Resources

- [RFC-9591: FROST Protocol](https://datatracker.ietf.org/doc/html/rfc9591)
- [FROST Book](https://frost.zfnd.org/frost.html)
- [Safenet Source Code](https://github.com/safe-research/shieldnet)
