---
title: How to delegate stake?
description: How to delegate SAFE tokens to a Safenet validator and earn staking rewards.
---

<Note>
This page is a work in progress. The staking interface and delegation flow will be documented ahead of the Safenet Beta launch.
</Note>

## Delegators vs. validator self-stake

Anyone holding SAFE tokens can participate in Safenet security by delegating stake to a validator; you do not need to run a node yourself.

- **Validators** stake SAFE tokens toward their own address (self-stake) and must maintain a minimum of **3,500,000 SAFE** to be eligible for validator rewards.
- **Delegators** stake SAFE toward a validator's address. Your tokens back that validator's security contribution and entitle you to a share of rewards.

Delegated stake and self-stake are tracked separately in the Staking contract but both contribute to the validator's total stake weight for reward purposes.

## Choosing a validator to delegate to

TODO: Cover the following:

- What to look for in a validator (participation rate, total stake, self-stake level)
- Where to see a live list of validators and their stats (Explorer / staking interface)
- Risks of delegating to a low-participation validator (rewards affected, stake is not at risk)
- Whether you can split delegation across multiple validators

## How to delegate

TODO: Step-by-step walkthrough:

1. Connect your wallet to the staking interface (link TBD)
2. Browse the validator list and select a validator
3. Enter the amount of SAFE to delegate
4. Approve the SAFE token transfer
5. Confirm the staking transaction

Alternatively, delegate directly via the Staking contract:

```solidity
// 1. Approve the staking contract to spend your SAFE
IERC20(SAFE_TOKEN).approve(STAKING_ADDRESS, amount);

// 2. Stake toward your chosen validator
Staking(STAKING_ADDRESS).stake(validatorAddress, amount);
```

## Checking your delegation balance

```solidity
// Your stake toward a specific validator
uint256 myStake = staking.stakes(myAddress, validatorAddress);

// Your total stake across all validators
uint256 myTotal = staking.totalStakerStakes(myAddress);
```

## Moving delegation between validators

TODO: Describe whether and how delegators can move stake from one validator to another: whether this requires a withdrawal + re-stake cycle or if there is a direct redelegation path.

→ See: [Staking lock-up periods](/safenet/staking/lockup) for withdrawal delay implications.

## Staking interface

TODO: Link to the dedicated staking and claiming interface once available.
