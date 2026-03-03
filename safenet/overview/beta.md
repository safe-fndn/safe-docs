---
title: Safenet Beta
sidebarTitle: Safenet Beta
description: Current status of the Safenet Beta network - what is live, what is in scope, and how to observe network activity.
---

Safenet Beta is the first live deployment of the Safenet protocol. It runs with a permissioned validator set and focuses on core consensus, transaction attestation, and SAFE token staking.

## What is live in Beta

- Validator coordination and threshold signing (FROST)
- SAFE token staking toward validators
- Transaction proposal and attestation flow
- Public explorer for network activity

## Scope and limitations

Safenet Beta is a deliberate starting point:

- **Safe transactions on EVM chains only**
- **Permissioned validator set**: validators are selected by the Safe Ecosystem Foundation
- **Pre-defined security checks**: no open transaction checker market yet
- **No slashing**: stake is not at risk of being slashed in Beta

See the [Roadmap](/safenet/overview/roadmap) for what comes after Beta.

## Explorer

The Beta Explorer provides a transparent, public view into transactions proposed and checked by the Safenet validator set.

The Explorer is available at _TODO_.

TODO: Add screenshots of UI.

### Explore network activity

- Live stream of recently proposed Safe transactions
- Status tracking: **Proposed**, **Attested**, **Timed-out**
- Search by Safe address or safeTxHash

Each transaction has a dedicated detail page showing:

- Safe transaction summary and decoding
- Proposal history and attestation status
- Validator participation
- Links to Safe\{Wallet\} and chain explorers (if available)

### Submit a proposal

If a Safe transaction has not yet been proposed to Safenet Beta, it can be submitted directly from the explorer.

- No wallet connection required
- Sponsored relayer submission
- Manual entry or SafeTxHash prefill

[Code on GitHub](https://github.com/safe-research/safenet/tree/main/explorer)

[Report feedback / open issue](https://github.com/safe-research/issues/new)
