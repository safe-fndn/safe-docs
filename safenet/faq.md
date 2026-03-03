---
title: FAQs
description: Frequently asked questions about Safenet and Safenet Beta.
---

## How do I use Safenet and the Explorer in Beta?

The Safenet Beta Explorer is a public interface for observing transaction validation activity on the network. No wallet connection or account is required to view activity.

**Exploring network activity**

The Explorer provides a live stream of Safe transactions that have been proposed to the Safenet validator set. Each transaction shows its current status (**Proposed**, **Attested**, or **Timed-out**) and a detail page with the full transaction breakdown, validator participation, and links to Safe\{Wallet\} and chain explorers.

You can search by Safe address or `safeTxHash`.

**Submitting a transaction for validation**

If your Safe transaction has not yet been proposed to Safenet Beta, you can submit it directly from the Explorer:

1. Navigate to the Explorer at _TODO: link_
2. Enter your `safeTxHash` or paste the transaction details manually
3. Submit (no wallet required, the submission is relayed for you)

The Explorer is intentionally simple in Beta and focused on transparency. It will evolve alongside the protocol.

[Explorer source on GitHub](https://github.com/safe-research/safenet/tree/main/explorer) · [Report an issue](https://github.com/safe-research/issues/new)

## How long does transaction validation take?

TODO: Answer with real latency expectations from the Beta network: typical time from proposal to attestation under normal conditions, and what affects this (validator participation, network conditions, signing round timeouts).

## How do I verify my transaction is secure?

TODO: Describe the verification flow:

- How to look up a transaction's attestation status in the Explorer
- What a valid attestation means (FROST threshold signature, onchain record)
- How to verify the attestation cryptographically if needed
- What "Attested" vs "Proposed" vs "Timed-out" mean in practice

## Can I become a validator?

In Safenet Beta, the validator set is **permissioned**: validators are selected by the Safe Ecosystem Foundation.

TODO: Add link to the validator interest / application form.

The roadmap includes moving toward a more open validator set in future phases. → See: [Roadmap](/safenet/overview/roadmap)

## Is this supported by the DAO?

TODO: Describe the relationship between Safenet and SafeDAO: what has been approved by SafeDAO governance, what is pending (e.g., the rewards proposal), and how the project relates to the broader Safe Ecosystem Foundation mandate.

## Is the code open source?

TODO: Confirm open source status and link to the relevant repositories:

- Smart contracts (Staking, Consensus, FROSTCoordinator): link to `safe-research/shieldnet`
- Explorer: link to `safe-research/safenet`
- Any off-chain components / validator client

## Where can I learn more about the technical details?

TODO: Point to:

- The smart contract documentation (protocol internals, currently not in public nav but available)
- FROST protocol spec: [RFC-9591](https://datatracker.ietf.org/doc/html/rfc9591)
- Source code repositories
- Research blog posts or papers if available
- Contact / community channels for technical questions

## How do I programmatically propose Safe transactions for validation?

TODO: Cover the developer path for submitting transactions to Safenet:

- The `proposeTransaction` function on the Consensus contract
- Required transaction format (`SafeTransaction.T` struct)
- How to listen for `TransactionProposed` and `TransactionAttested` events
- How to retrieve and use the resulting FROST attestation
- Any available SDKs or client libraries

Example starting point (see Consensus contract docs for full detail):

```solidity
bytes32 message = consensus.proposeTransaction(tx);
// Wait for TransactionAttested event, then:
(bytes32 msg, FROST.Signature memory sig) = consensus.getRecentAttestation(tx);
```
