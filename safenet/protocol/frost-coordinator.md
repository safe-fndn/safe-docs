---
title: FROST Coordinator
description: The [FROSTCoordinator contract](https://github.com/safe-research/shieldnet/blob/main/contracts/src/FROSTCoordinator.sol) orchestrates **distributed key generation (DKG)** and **threshold signing ceremonies** for FROST groups. It is the cryptographic heart of Safenet, enabling validators to collectively generate and use shared signing keys without any single party knowing the complete private key.
---

### Purpose

| Function | Description |
|----------|-------------|
| **Key Generation** | Coordinate DKG ceremonies to create threshold signing groups |
| **Nonce Management** | Track precommitted nonces for secure signing |
| **Signature Aggregation** | Collect and aggregate signature shares |
| **Callback Integration** | Notify other contracts when ceremonies complete |

### Key Characteristics

- **Stateless Ceremonies**: Each ceremony is identified by deterministic IDs
- **[RFC-9591](https://datatracker.ietf.org/doc/html/rfc9591) Compliant**: Implements FROST(secp256k1, SHA-256) ciphersuite

---

## ELI5: What is FROST?

Imagine a treasure chest that needs multiple keys to open:

**Traditional Multi-sig**: 
- 3 people each have their own key
- Need 2-of-3 keys to open
- Everyone knows exactly who signed

**FROST Threshold Signatures**:
- 3 people collectively create ONE "master key"
- Each person holds a PIECE of this key (not a complete key!)
- Nobody can reconstruct the full private key

**Why is this better?**
1. **Efficiency**: One signature instead of multiple
2. **Compatibility**: Works with existing systems expecting single signatures
3. **Security**: No single point of failure - the full key never exists in one place
