---
title: Safenet Beta
sidebarTitle: Safenet Beta
description: Current status of the Safenet Beta network - what is live, what is being tested, and how to observe network activity.
---

Safenet Beta is the first live deployment of the Safenet protocol. It runs with a permissioned validator set and focuses on core consensus, transaction attestation, and SAFE token staking.

## What is live in Beta

- Validator coordination and threshold signing (FROST)
- SAFE token staking and open delegation
- Transaction proposal and attestation flow
- Static transaction security checks
- Public explorer for network activity

## Beta goals

Safenet Beta is designed to validate the protocol's core assumptions under real-world conditions:

- Can the validator network reliably process transaction checks at scale?
- Can validator participation be measured and enforced through reward eligibility?
- Can SAFE staking and delegation bootstrap meaningful economic security?

Beta staking rewards are subsidized for an initial period. Long-term, rewards will be funded by transaction fees paid by users and integrators.

## Validator set

The Beta validator set consists of validators run by independent organizations, selected by the Safe Ecosystem Foundation. All validators must maintain a minimum self-stake of 3,500,000 SAFE.

Validator coordination is handled via contracts on Gnosis Chain. Deployment info:

- Consensus contract: `TODO`
- Coordinator contract: `TODO`

Safenet Beta uses the following permissioned validator set:

| Validator | Address |
|---|---|
| TODO | `TODO` |
| TODO | `TODO` |
| TODO | `TODO` |
| TODO | `TODO` |
| TODO | `TODO` |

TODO: Link to validator.json once live

## Transaction checks

In Safenet Beta, validators attest to a fixed set of static security checks. These checks are fully deterministic: given the same transaction data, every honest validator reaches the same conclusion.

[Current checks applied to every proposed Safe transaction:](https://github.com/safe-research/safenet/tree/main/validator/src/consensus/verify/safeTx/checks)

- No unexpected delegatecalls
- Upgrade only to trusted singletons
- Only allow adding trusted modules
- Only trusted fallback handlers can be set
- Only trusted guards can be set

Advanced, context-specific checks (transfer volume analysis, allow/deny lists, actively exploited contracts) are planned for later phases. See the [Roadmap](/safenet/overview/roadmap).

## Scope and limitations

Safenet Beta is a deliberate starting point:

- **Safe transactions on EVM chains only**
- **Permissioned validator set**: validators are selected by the Safe Ecosystem Foundation
- **Static security checks only**: no open transaction checker market yet
- **No slashing**: stake is not at risk of being slashed in Beta

See the [Roadmap](/safenet/overview/roadmap) for what comes after Beta.

## Explorer

The Beta Explorer is a public tool for viewing transactions proposed and checked by the Safenet validator set. See the [FAQ](/safenet/resources/faq) for details.
