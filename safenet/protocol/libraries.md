---
title: Supporting Libraries Reference
description: 
---

## Overview

Safenet's smart contracts rely on a set of specialized libraries for cryptographic operations, data management, and protocol utilities. This document provides a reference for each library.

---

## Core Cryptographic Libraries

### FROST.sol

**Purpose**: Implementation of the FROST(secp256k1, SHA-256) ciphersuite per [RFC-9591](https://datatracker.ietf.org/doc/html/rfc9591).

#### Types

| Type | Description |
|------|-------------|
| `Identifier` | Wrapped `uint256` for participant IDs (must be non-zero) |

#### Key Functions

| Function | Description |
|----------|-------------|
| `newIdentifier(uint256)` | Create and validate an identifier |
| `nonce(bytes32, uint256)` | Generate nonce from randomness and secret |
| `bindingFactors(Point, Commitment[], bytes32)` | Compute binding factors for signing |
| `challenge(Point, Point, bytes32)` | Compute signature challenge |
| `verify(Point, Signature, bytes32)` | Verify a FROST signature |
| `verifyShare(Point, Point, Point, SignatureShare, bytes32)` | Verify a signature share |

#### Hash Functions (Internal)

The library implements RFC-9591 hash functions:
- `H1`: Hash to scalar (binding factor)
- `H2`: Hash to scalar (challenge)
- `H3`: Hash to scalar (nonce generation)
- `H4`: Message hash
- `H5`: Commitment hash

---

### Secp256k1.sol

**Purpose**: Elliptic curve operations on the secp256k1 curve.

#### Constants

| Constant | Value | Description |
|----------|-------|-------------|
| `B` | 7 | Curve coefficient (y² = x³ + 7) |
| `P` | 2²⁵⁶ - 2³² - 977 | Field prime |
| `N` | 0xfffffffffffffffffffffffffffffffebaaedce6af48a03bbfd25e8cd0364141 | Group order |

#### Key Functions

| Function | Description |
|----------|-------------|
| `add(Point, Point)` | Point addition |
| `mul(Point, uint256)` | Scalar multiplication |
| `mulmuladd(uint256, uint256, Point, Point)` | Combined mul-mul-add for verification |
| `serialize(Point)` | Convert to compressed format |
| `eq(Point, Point)` | Point equality |
| `requireOnCurve(Point)` | Validate point is on curve |
| `requireNonZero(Point)` | Validate point is not identity |

#### Implementation Notes

- Uses affine coordinates (not projective) for simplicity
- Single `modexp` precompile call per division
- Optimized for single additions (typical use case)

---

## Protocol Libraries

### ConsensusMessages.sol

**Purpose**: Compute EIP-712 structured messages for consensus operations.

#### Constants (Type Hashes)

```solidity
// keccak256("EIP712Domain(uint256 chainId,address verifyingContract)")
bytes32 DOMAIN_TYPEHASH

// keccak256("EpochRollover(uint64 activeEpoch,uint64 proposedEpoch,uint64 rolloverBlock,uint256 groupKeyX,uint256 groupKeyY)")
bytes32 EPOCH_ROLLOVER_TYPEHASH

// keccak256("TransactionProposal(uint64 epoch,bytes32 safeTxHash)")
bytes32 TRANSACTION_PROPOSAL_TYPEHASH
```

#### Functions

| Function | Description |
|----------|-------------|
| `domain(uint256, address)` | Compute EIP-712 domain separator |
| `epochRollover(bytes32, uint64, uint64, uint64, Point)` | Create epoch rollover message |
| `transactionProposal(bytes32, uint64, bytes32)` | Create transaction proposal message |

---

### MetaTransaction.sol

**Purpose**: Define and hash meta-transactions for cross-chain execution.

#### Structs

```solidity
struct T {
    uint256 chainId;     // Target chain ID
    address account;     // Executing account
    address to;          // Target address
    uint256 value;       // ETH value
    Operation operation; // CALL or DELEGATECALL
    bytes data;          // Calldata
    uint256 nonce;       // Replay protection
}

enum Operation {
    CALL,
    DELEGATECALL
}
```

#### Functions

| Function | Description |
|----------|-------------|
| `hash(T)` | Compute EIP-712 struct hash |

---

## Identifier Libraries

### FROSTGroupId.sol

**Purpose**: Unique identifier for FROST groups.

#### Type

```solidity
type T is bytes32;
```

The group ID is computed deterministically from:
- Participant Merkle root
- Participant count
- Threshold
- Context data

#### Format

```
| <-- 192 bits: hash data --> | <-- 64 bits: reserved (zero) --> |
```

#### Functions

| Function | Description |
|----------|-------------|
| `create(bytes32, uint16, uint16, bytes32)` | Create group ID from parameters |
| `mask(bytes32)` | Extract group ID portion |
| `eq(T, T)` | Compare group IDs |
| `requireValid(T)` | Validate format |

---

### FROSTSignatureId.sol

**Purpose**: Unique identifier for signing ceremonies.

#### Type

```solidity
type T is bytes32;
```

Combines group ID with sequence number:
```
| <-- 192 bits: group ID --> | <-- 64 bits: sequence + 1 --> |
```

The `+1` offset ensures signature IDs are never zero even for sequence 0.

#### Functions

| Function | Description |
|----------|-------------|
| `create(FROSTGroupId.T, uint64)` | Create signature ID |
| `group(T)` | Extract group ID |
| `sequence(T)` | Extract sequence number |
| `isZero(T)` | Check if zero |
| `requireValid(T)` | Validate format |

---

## Data Structure Libraries

### FROSTParticipantMap.sol

**Purpose**: Track FROST participants during DKG and signing.

#### Functions

| Function | Description |
|----------|-------------|
| `init(T, bytes32)` | Initialize with Merkle root |
| `initialized(T)` | Check if initialized |
| `register(T, Identifier, address, bytes32[])` | Register participant with Merkle proof |
| `set(T, address, Point)` | Set participant's public key |
| `identifierOf(T, address)` | Get identifier for address |
| `getKey(T, Identifier)` | Get public key for identifier |
| `confirm(T, Identifier)` | Mark participant as confirmed |
| `complain(T, Identifier, Identifier)` | File complaint |
| `respond(T, Identifier, Identifier)` | Respond to complaint |

---

### FROSTNonceCommitmentSet.sol

**Purpose**: Track precommitted nonces for signing.

#### Constants

| Constant | Value | Description |
|----------|-------|-------------|
| `_CHUNKSZ` | 10 | Each chunk = 2¹⁰ = 1024 nonces |
| `_OFFSETMASK` | 0x3ff | Mask for offset extraction |
| `_ROOTMASK` | ~0x3ff | Mask for root extraction |

#### Functions

| Function | Description |
|----------|-------------|
| `commit(T, Identifier, bytes32, uint64)` | Commit to nonce chunk |
| `verify(T, Identifier, Point, Point, uint64, bytes32[])` | Verify nonce inclusion |

---

### FROSTSignatureShares.sol

**Purpose**: Accumulate and aggregate signature shares.

#### Functions

| Function | Description |
|----------|-------------|
| `register(T, Identifier, SignatureShare, Point, bytes32, bytes32[])` | Add share with Merkle proof |
| `groupSignature(T, bytes32)` | Get accumulated signature |

#### Aggregation Logic

Shares are aggregated by:
```
R = Σ Rᵢ  (point addition)
z = Σ zᵢ  (scalar addition mod N)
```

---

## Interface

### IFROSTCoordinatorCallback.sol

**Purpose**: Interface for contracts receiving FROST coordinator callbacks.

```solidity
interface IFROSTCoordinatorCallback {
    // Called when DKG completes successfully
    function onKeyGenCompleted(FROSTGroupId.T gid, bytes calldata context) external;
    
    // Called when signing completes successfully
    function onSignCompleted(FROSTSignatureId.T sid, bytes calldata context) external;
}
```

---

## Gas Optimization Notes

### Storage Packing

Several libraries use bit-packing for efficient storage:

1. **FROSTNonceCommitmentSet**: Packs Merkle root and offset into single `bytes32`
2. **FROSTGroupId**: Uses upper 192 bits, reserves lower 64 bits
3. **FROSTSignatureId**: Encodes group ID + sequence in single `bytes32`
4. **GroupParameters**: Packs status, counts, and sequence into single slot

### Assembly Usage

Critical paths use inline assembly for:
- Hash computation without memory allocation
- Efficient data encoding
- Point serialization

### Precompile Usage

- `modexp` (0x05): Used for modular division in `Secp256k1`
- Standard Merkle proof verification uses OpenZeppelin's optimized implementation

---

## Security Notes

### Identifier Validation

All identifier types validate on creation:
- `FROST.Identifier`: Must be non-zero
- `FROSTGroupId`: Lower 64 bits must be zero
- `FROSTSignatureId`: Must have non-zero sequence portion

### Merkle Proof Security

Participant and nonce verification use secure Merkle proofs:
- Leaf hashing prevents second preimage attacks
- Proof length validation prevents malformed proofs

### Scalar Validation

All scalars are validated to be less than curve order `N` before use in signature operations.

---
