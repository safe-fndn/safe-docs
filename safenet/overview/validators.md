---
title: Safenet Validators
description: The role of Validators in the Safenet protocol - what they do, why decentralization matters, and how they are incentivized.
---

Validators are the core participants in the Safenet network. They collectively check and attest to Safe transactions before execution. Because attestations require a threshold of Validators to cooperate, no single participant controls whether a transaction is approved or blocked.

## What Validators do

When a Safe transaction is proposed to Safenet, Validators check it against a defined set of security rules. If the transaction satisfies all rules, Validators coordinate to produce a FROST threshold signature: a cryptographic attestation that the transaction is valid.

The Safe guard checks this attestation onchain before allowing execution. Without a valid attestation, the transaction cannot proceed.

Validators only attest to outcomes that are fully deterministic. Given the same transaction data, every honest Validator reaches the same conclusion. This is what allows the network to maintain its security guarantees even when some Validators behave dishonestly.

The network tolerates up to one-third of Validators acting dishonestly. As long as fewer than one-third are compromised, no invalid attestation can be produced. This property is known as Byzantine Fault Tolerance (BFT).

## Decentralization and trust

The Safenet Validator set is run by a varied group of independent organizations. This is a deliberate design choice: no single company controls whether a transaction is attested.

This distinguishes Safenet from centralized transaction checking services, where a single server or API is the sole arbiter of transaction safety. A compromised or captured central service can fail silently. Safenet requires a coordinated majority of independent Validators to be compromised simultaneously, and even then, the onchain nature of attestations means any failure is publicly visible and auditable.

All Validator attestations are recorded onchain. Anyone can inspect which Validators participated in a given signing round and independently verify the threshold signature.

See [Safenet Beta](/safenet/overview/beta) for the current Validator set.

## Validator incentives

Validators earn SAFE token rewards in proportion to their stake and participation rate. Reward mechanics, including commission rates, minimum stake, and distribution schedule, are defined in the staking rewards design.

See [Staking rewards](/safenet/staking/rewards) for full details.

## Joining as a Validator

In Safenet Beta, Validators are onboarded by the Safe Ecosystem Foundation. The Validator set is planned to expand and eventually become permissionless.

See [Safenet Beta](/safenet/overview/beta) for details on the current set, and the [Roadmap](/safenet/overview/roadmap) for plans toward permissionless onboarding.

TODO: Add reach-out form link for Validator interest once available.
