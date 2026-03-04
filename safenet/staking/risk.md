---
title: Is my stake at risk?
description: Understanding the risks to staked SAFE tokens in Safenet Beta.
---

## No slashing in Beta

In Safenet Beta, **staked tokens cannot be slashed**. There is no mechanism for the protocol to confiscate or destroy staked SAFE under any circumstances in the current phase.

**Post-Beta**: Once slashing is introduced, a portion of staked tokens could be at risk if a validator is found to have acted maliciously or violated protocol rules. The specific conditions, amounts, and governance process for slashing will be proposed ahead of that phase. It would need an active migration by every staker. See: [Roadmap](/safenet/overview/roadmap) for a plan post-beta.

## Smart contract risk

Staking SAFE tokens in any smart contract carries inherent risk. Key facts about the Staking contract:

- The contract is **non-upgradeable**: its logic cannot be changed after deployment
- It has been independently **audited**: See: [Security](/safenet/security) for the full audit report and contract details
- It holds no protocol-level permissions over your tokens beyond what you approve

As with any smart contract interaction, you should only stake amounts you are comfortable locking under these conditions.

## Withdrawal delay risk

During the lock-up period, stakers **cannot immediately exit**. Your tokens remain in the contract until the 2-day withdrawal delay passes after you initiate a withdrawal.

- If a validator is deregistered by the protocol owner, your withdrawal proceeds normally; deregistration does not block pending withdrawals.
- If you need to exit urgently, you must wait out the delay period regardless of what happens to your validator.

→ See: [Staking lock-up periods](/safenet/staking/lockup) for the full withdrawal flow.

## Validator performance risk

If your chosen validator's participation falls below **75%** during a reward period, **neither you nor the validator earn rewards for that period**. Your staked SAFE tokens are not at risk; only your rewards for that period are forfeited.

You can monitor your validator's participation rate in the staking interface. If you want to move to a different validator, you must go through a full withdrawal and restake cycle. There is no direct redelegation path.

→ See: [How to delegate stake](/safenet/staking/delegate) for how to choose a validator and what to look for.
