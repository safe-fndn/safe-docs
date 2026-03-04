---
title: How to delegate stake?
description: How to delegate SAFE tokens to a Safenet validator and earn staking rewards.
---

Anyone holding SAFE tokens can delegate stake to a validator and earn a share of their rewards, without running a node. See [Staking overview](/safenet/staking/overview) for how delegation fits into the broader staking system.

## Choosing a validator

Your rewards depend directly on the validator you back.

**Participation rate** is the most important factor. If a validator's participation falls below 75% in a reward period, neither they nor their delegators earn rewards for that period. Look for validators with a consistently high participation rate.

**Self-stake level** signals a validator's own exposure. Validators must maintain a minimum average self-stake of 3,500,000 SAFE to be eligible for their own reward share. If they fall below this, they forfeit their own rewards but delegator rewards are unaffected.

**Total stake** affects reward efficiency. Reward weight grows sub-linearly once a validator's total stake exceeds a per-validator threshold. Very large validators earn proportionally less per token than smaller ones, so delegating to a mid-sized validator may yield better returns.

You can view validator stats, including participation rates and stake levels in the staking interface. There is also a [Safenet Beta dashboard on Dune](https://dune.com/safe/safenet-beta) available.

You can split your delegation across more than one validator simultaneously.

## How to delegate

TODO: Link to staking interface once available.

1. Connect your wallet to the staking interface
2. Browse the validator list and select a validator
3. Enter the amount of SAFE to delegate
4. Approve the SAFE token transfer
5. Confirm the staking transaction

For those who prefer to interact with the contract directly, the Staking contract source and ABI are available on [GitHub](https://github.com/safe-research/safenet).

Your delegation is active once the transaction is confirmed. Rewards are calculated using a time-weighted average over the reward period, so stake added mid-period earns proportionally for the time it was active.

## Checking your balance

Your current delegation balance and accrued rewards are visible in the staking interface. You can look up your wallet address to see which validators you have delegated to and your current stake amounts for each.

## Moving to a different validator

There is no direct redelegation path. To move stake from one validator to another, you must go through a full withdrawal and restake cycle:

1. Initiate a withdrawal from your current validator
2. Wait out the **2-day** withdrawal delay
3. Claim your tokens
4. Delegate to your new validator

Your tokens are locked and not earning rewards during the withdrawal delay. Factor this time cost in when deciding whether to switch validators.

→ See: [Staking lock-up periods](/safenet/staking/lockup) for the withdrawal flow and current delay duration.
