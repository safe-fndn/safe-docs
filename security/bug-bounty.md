---
title: "Bug Bounty Program"
description: "Report smart contract vulnerabilities in Safe Smart Accounts and earn rewards of up to $1,000,000 through responsible disclosure."
---

<Note>
  This bug bounty program **applies only to smart contract–related vulnerabilities**.  For issues related to [Safe\{Wallet\}](https://app.safe.global), please contact [wallet-reports@safe.global](mailto:wallet-reports@safe.global).
</Note>

The Safe Bug Bounty program rewards security researchers who help identify vulnerabilities in Safe Smart Accounts and officially supported modules. Rewards can reach **up to \$1,000,000**, depending on severity and impact.

Before submitting, please carefully review the rules and scope below. To report a vulnerability, contact us at
[bounty@safefoundation.org](mailto:bounty@safefoundation.org).

You can also review [past bounties](/security/past-bounties).

## Audits

Safe smart contracts are regularly reviewed by independent security experts.
For details, see the [Audits](/security/audits) page.

## Rules

Many rules from the [Ethereum Foundation Bug Bounty Program](https://bounty.ethereum.org) apply to Safe as well:

- Issues already known to the Safe team or previously reported are not eligible.
- Public disclosure of a vulnerability makes it ineligible for a bounty.
- Safe employees, contractors, auditors, and anyone paid by Safe (directly or indirectly) are not eligible.
- Eligibility, severity classification, and reward amounts are determined solely by the Safe Bug Bounty panel.

## Scope

The bug bounty covers core Safe contracts and selected officially supported modules.

### Safe Smart Account versions

- **v1.5.0** ([Release](https://github.com/safe-fndn/safe-smart-account/releases/tag/v1.5.0), [README](https://github.com/safe-fndn/safe-smart-account/blob/v1.5.0/README.md))
- **v1.4.1** ([Release](https://github.com/safe-fndn/safe-smart-account/releases/tag/v1.4.1),[README](https://github.com/safe-fndn/safe-smart-account/blob/v1.4.1/README.md))
- **v1.3.0** ([Release](https://github.com/safe-fndn/safe-smart-account/releases/tag/v1.3.0),[README](https://github.com/safe-fndn/safe-smart-account/blob/v1.3.0/README.md))
- **v1.2.0** ([Release](https://github.com/safe-fndn/safe-smart-account/releases/tag/v1.2.0),[README](https://github.com/safe-fndn/safe-smart-account/blob/v1.2.0/README.md))
- **v1.1.1** ([Release](https://github.com/safe-fndn/safe-smart-account/releases/tag/v1.1.1),[README](https://github.com/safe-fndn/safe-smart-account/blob/v1.1.1/README.md))

### Supported Safe Modules

- [Safe 4337 Module v0.3.0](https://github.com/safe-fndn/safe-modules/tree/4337/v0.3.0/modules/4337)
- [Safe Passkey Module v0.2.1](https://github.com/safe-fndn/safe-modules/tree/passkey/v0.2.1/modules/passkey)
- [Social Recovery Module v0.1.0](https://github.com/safe-fndn/safe-modules/tree/recovery/v0.1.0/modules/recovery)

### In scope contracts

**Safe core contracts (v1.4.1, v1.5.0)**

- `Safe.sol`, `SafeL2.sol`
- `SafeProxy.sol`, `SafeProxyFactory.sol`
- `MultiSend.sol`, `MultiSendCallOnly.sol`, `CreateCall.sol`
- `TokenCallbackHandler.sol`, `CompatibilityFallbackHandler.sol`, `ExtensibleFallbackHandler.sol`

**Legacy Gnosis Safe contracts (v1.1.1, v1.2.0, v1.3.0)**

- `GnosisSafe.sol`, `GnosisSafeL2.sol`
- `GnosisSafeProxy.sol`, `GnosisSafeProxyFactory.sol`
- `CreateAndAddModules.sol`, `MultiSend.sol`, `MultiSendCallOnly.sol`, `CreateCall.sol`
- `DefaultCallbackHandler.sol`, `CompatibilityFallbackHandler.sol`

**Module contracts**

- `Safe4337Module.sol`
- `SafeWebAuthnSignerFactory.sol`
- `SafeWebAuthnSignerProxy.sol`
- `SafeWebAuthnSignerSingleton.sol`
- `SafeWebAuthnSharedSigner.sol`
- `WebAuthn.sol`, `P256.sol`

Deployed contract addresses can be found in the [Safe Deployments repository](https://github.com/safe-global/safe-deployments).

### Examples of issues in scope

- Theft of funds or tokens
- Freezing or permanently locking funds
- Replay attacks on the same chain
- Changing Safe or module settings without owner consent

### Out of scope

- Contracts, modules, or libraries not listed above
- Gas optimizations
- Known issues listed in audits or documentation
- Issues already fixed in newer versions

## Intended behavior

To understand expected contract behavior, refer to:

- The [Safe Smart Account README](https://github.com/safe-fndn/safe-smart-account/blob/v1.5.0/README.md)
- Release notes and the [CHANGELOG](https://github.com/safe-fndn/safe-smart-account/blob/v1.5.0/CHANGELOG.md)
- The [Safe Smart Account documentation](/smart-account/overview)

For modules:

- [Safe 4337 Module README](https://github.com/safe-fndn/safe-modules/tree/4337/v0.3.0/modules/4337/README.md)
- [Safe Passkey README](https://github.com/safe-fndn/safe-modules/tree/passkey/v0.2.1/modules/passkey/README.md)
- [Social Recovery Module README](https://github.com/safe-fndn/safe-modules/blob/recovery/v0.1.0/modules/recovery/README.md)

## Compensation

All valid bug reports are considered for a bounty. Rewards depend on severity and impact.

### High severity — up to \$1,000,000

- Direct theft of funds or tokens
- Permanent fund lockups
- Bugs that require an urgent redeploy

### Medium severity — up to \$50,000

- Fund loss due to unexpected or unintuitive behavior
- Issues users cannot reasonably anticipate

### Low severity — up to \$10,000

- Fee avoidance
- Exploits that degrade user experience

Bounties are paid in [USDC on Ethereum Mainnet](https://etherscan.io/token/0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48).

Submission quality matters. A strong report includes a clear explanation and reproducible steps.

## Submission process

Email your report to [bounty@safefoundation.org](mailto:bounty@safefoundation.org).

Please include:

- A detailed description of the issue
- Steps to reproduce
- Your Ethereum Mainnet address for payment

Anonymous submissions are welcome. If multiple addresses are provided, one will be selected at Safe’s discretion.

For details on data handling, see our [Privacy Policy](https://safefoundation.org/privacy).

## Responsible disclosure policy

If you follow the guidelines below, Safe will not pursue legal action in response to your report.

We ask that you:

- Allow reasonable time for investigation and remediation before public disclosure
- Avoid privacy violations or service disruption
- Do not exploit the issue in production
- Comply with all applicable laws

Public disclosure or intent to exploit a vulnerability on Mainnet will make a report ineligible for a bounty. When in doubt, the [Ethereum Foundation Bug Bounty rules](https://bounty.ethereum.org) apply.

Questions? Contact us at [bounty@safefoundation.org](mailto:bounty@safefoundation.org).

_Happy hunting!_

## Note on Safe\{Wallet\}

Issues related to **Safe\{Wallet\}** (web, mobile, or backend services) are generally **out of scope**.

For non-security bugs, open an issue in the relevant repository, such as [safe-wallet-monorepo](https://github.com/safe-global/safe-wallet-monorepo/issues).

For **severe security issues** affecting Safe\{Wallet\}, contact [wallet-reports@safe.global](mailto:wallet-reports@safe.global).\
Any rewards for Safe\{Wallet\} issues are granted at the sole discretion of the team maintaining Safe\{Wallet\}.
