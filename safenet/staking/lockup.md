---
title: Lock-up periods
description: How withdrawal delays work and what to expect when unstaking SAFE tokens.
---

Staked SAFE tokens are not immediately withdrawable. After requesting a withdrawal, a mandatory **2-day waiting period** applies before you can claim your tokens back.

## How to withdraw

Choose one of the [available staking interfaces](http://safefoundation.org/safenet).

1. Go to the staking interface and connect your wallet
2. Select the Validator you want to withdraw from and enter the amount
3. Confirm the withdrawal transaction. Your tokens enter the 2-day waiting period
4. After 2 days, return to the staking interface to claim your tokens

Tokens in the withdrawal queue do not count toward your time-weighted stake average, so they do not earn rewards during the waiting period.

## Waiting period

The withdrawal delay is currently **2 days**. This delay exists so that if a Validator misbehaves, there is time to respond before they can exit their stake.

**Multiple pending withdrawals**: If you initiate more than one withdrawal, they are processed in the order they were submitted. You must claim each one before the next becomes available.

## Changing the delay

The withdrawal delay is a protocol parameter governed by SafeDAO. Any proposed change must wait **7 days** after approval before taking effect. This ensures Stakers always have advance notice before a change applies. The maximum withdrawal delay that can be set is 7 days, ie. **there will never be a withdrawal delay longer than 7 days** with the current, immutable Staking contract.

<Note>
The current withdrawal delay is 2 days. If this changes upon SafeDAO approval, the new value will be reflected here.
</Note>

The Staking contract is deployed on Ethereum Mainnet at [`0x115E78f160e1E3eF163B05C84562Fa16fA338509`](https://etherscan.io/address/0x115E78f160e1E3eF163B05C84562Fa16fA338509).
