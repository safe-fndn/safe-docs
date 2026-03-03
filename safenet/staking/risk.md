---
title: Is my stake at risk?
description: Understanding the risks to staked SAFE tokens in Safenet Beta.
---

## No slashing in Beta

In Safenet Beta, **staked tokens cannot be slashed**. There is no mechanism for the protocol to confiscate or destroy staked SAFE under any circumstances in the current phase.

Economic slashing is planned for a later phase as part of stronger cryptoeconomic accountability guarantees. This page will be updated when slashing mechanics are defined and approved by SafeDAO.

→ See: [Roadmap](/safenet/overview/roadmap)

## Smart contract risk

Staking SAFE tokens in any smart contract carries inherent risk. Key facts about the Staking contract:

- The contract is **non-upgradeable**: its logic cannot be changed after deployment
- It has been independently **audited** (see below)
- It holds no protocol-level permissions over your tokens beyond what you approve

As with any smart contract interaction, you should only stake amounts you are comfortable locking under these conditions.

## Audits

### Safenet Staking Contract

**Chain**: Mainnet

The Safenet Beta Staking contract has undergone an independent audit. The report is available [here](https://github.com/safe-research/shieldnet/blob/main/contracts/audits/audit.md). The audit focused on identifying vulnerabilities and ensuring the security of the staking mechanisms.

### Safenet Consensus Contract

**Chain**: Gnosis Chain

The Safenet Consensus contract has not undergone an audit yet. The contract is owner-governed and no user funds are directly at risk through it; its two main functions are posting transactions for attestation and collecting attestations. An audit is planned for a later stage.

## Withdrawal delay risk

During the lock-up period, stakers **cannot immediately exit**. Your tokens remain in the contract until the withdrawal delay passes after you initiate a withdrawal.

- If a validator is deregistered by the protocol owner, your withdrawal proceeds normally; deregistration does not block pending withdrawals.
- If you need to exit urgently, you must wait out the delay period regardless of what happens to your validator.

→ See: [Staking lock-up periods](/safenet/staking/lockup) for the full withdrawal flow.

## Validator performance risk

If your chosen validator's participation falls below **75%** during a reward period, **neither you nor the validator earn rewards for that period**. Your staked SAFE tokens are not at risk; only your rewards for that period are forfeited.

TODO: Describe how delegators can monitor validator participation and what options they have to redelegate.

## Future slashing

Once slashing is introduced (post-Beta), a portion of staked tokens could be at risk if a validator is found to have acted maliciously or violated protocol rules. The specific conditions, amounts, and governance process for slashing will be published ahead of that phase.
