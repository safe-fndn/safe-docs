---
title: What is Safenet?
sidebarTitle: Overview
description: Safenet enforces transaction security onchain by preventing high-risk transactions from executing.
---

<Note>
Safenet is currently in Beta. The validator set is permissioned and slashing is not yet active. See [Safenet Beta](/safenet/overview/beta) for current status.
</Note>

Safenet is a protocol for **onchain transaction security enforcement**.

It acts as a **last line of defense** against malicious or high-risk transactions by ensuring that transactions are **validated before execution**, rather than merely displaying non-binding warnings.

Safenet replaces centralized transaction-checking services with a **resilient, validator-based network** that enforces security guarantees onchain.

## How Safenet protects accounts

Most transaction security tools today display warnings. They cannot stop a transaction from executing. Safenet changes this.

When a transaction is proposed, Safenet validators check it against a defined set of security rules. If the transaction passes, validators produce a cryptographic attestation. The Safe guard verifies that attestation onchain before allowing execution. If no valid attestation exists, the transaction is blocked.

This means protection is enforced by the protocol, not by user behavior. A phishing site, a compromised wallet UI, or an opaque approval cannot bypass it.

## What makes Safenet different

**Decentralized validation**
Security checks are performed by a network of validators, not a single API or server. The network tolerates up to one-third of validators acting dishonestly and still produces correct attestations.

**Onchain enforcement**
Attestations are cryptographic signatures verifiable on any EVM-compatible chain. A transaction without a valid attestation cannot execute, regardless of who signed it.

**A path to sustainable security incentives**
Safenet aims to create a market for transaction security: checkers compete to provide real-time risk signals, and validators attest to market outcomes. It is envisioned that this creates a sustainable path toward fee-based security services, which makes staking economically meaningful. This market mechanism is planned for after Beta.

**Open to all chains and wallets**
Any Safe on any supported EVM chain can use Safenet. No proprietary infrastructure required.

## Who is Safenet for?

**Safe users**
Safenet protects your account from malicious transactions, even if your wallet UI is compromised. See the [FAQ](/safenet/faq) to learn more and explore recent network activity.

**Stakers and delegators**
Delegate SAFE tokens to validators and earn rewards for securing the network. See [Staking](/safenet/staking/validator-staking).

**Validators, wallet operators, and security firms**
If you are interested in running a validator, integrating Safenet into your wallet, or contributing transaction security logic, reach out.

TODO: Add reach-out form link once available.

## Safenet Beta

Safenet is currently live in Beta, focusing on core consensus, threshold signing, and SAFE token staking with a permissioned validator set.

See [Safenet Beta](/safenet/overview/beta) for what is live today, and the [Roadmap](/safenet/overview/roadmap) for what comes next.
