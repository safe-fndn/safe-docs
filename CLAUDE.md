# CLAUDE.md: Safe Documentation

## Workflow rule

**Always plan before acting.** For any task that involves more than a single, obvious edit:

1. Read all relevant files first
2. Write out a concrete plan: what files will change, what will be created, what will be deleted, and why
3. Present the plan to the user and wait for explicit confirmation
4. Only then execute

Do not start editing files until the plan is confirmed. If you discover something unexpected mid-execution that changes the plan, stop and re-confirm.

## Project overview

This is the documentation site for [Safe](https://safefoundation.org/), built with [Mintlify](https://mintlify.com/). The site is hosted at `https://docs.safefoundation.org`.

The repo contains two main documentation areas:

- **Safe Smart Account** (`/smart-account`, `/features`, `/security`): technical docs for the Safe smart account protocol
- **Safenet** (`/safenet`): public-facing docs for the Safenet protocol (currently in Beta, nav tab is `hidden: true`)

**Only work in `/safenet` unless explicitly told otherwise.**

Navigation is defined in `docs.json` at the root. Adding a file without registering it in `docs.json` will not make it appear in the sidebar. Registering a path in `docs.json` that doesn't have a corresponding file will cause a build error.

## Safenet: what it is

Safenet is a protocol for onchain transaction security enforcement. It replaces centralized transaction-checking services with a decentralized Validator network that attests to Safe transactions before they execute. In Safenet Beta, Validators are permissioned, the Validator set is small, and no slashing is active. The Beta focuses on proving out the core staking, consensus, and FROST threshold signing mechanics.

## Safenet: target audience

The Safenet docs are primarily written for **non-technical readers** who hold SAFE tokens and are evaluating whether to stake or delegate. Secondary audiences:

- **Stakers and Delegators**: SAFE token holders who want to earn rewards by backing Validators. Main audience for all staking pages. Assume no Solidity knowledge; explain mechanics in plain language with analogies where helpful.
- **Validators**: technically sophisticated node operators. Can handle more precise language, but avoid unnecessary jargon.
- **Curious observers**: people who have heard about Safenet and want to understand what it does and whether it is safe. The overview and FAQ are their entry points.

The docs are **not** primarily targeted at:
- Wallet developers integrating Safenet (that audience is served separately)
- DeFi protocol researchers or cryptographers (link out to technical specs rather than reproducing them)

## Writing guidelines

### Tone
- Clear and direct. No marketing language ("revolutionary", "cutting-edge", "seamless").
- Honest about Beta limitations. If something isn't live yet or is pending DAO approval, say so explicitly.
- Confident but not overclaiming. Safenet makes specific guarantees; describe those accurately without overstating.
- Do not use em dashes (—). Use a comma, colon, or rewrite the sentence instead.
- Avoid semicolons unless necessary. Prefer two short sentences over one joined with a semicolon.
- Prefer short declarative sentences.

### Structure
- Lead with what the reader needs to know, not with background context.
- Use headings to make pages scannable. Readers often land mid-page from search.
- Prefer short paragraphs over walls of text.
- Use `<Note>` callouts for important caveats (e.g. pending DAO approval, Beta limitations).
- Use `<Warning>` callouts sparingly: only for things that could cause loss of funds or security issues.
- Do not use `---` as a section separator in page content. The only valid `---` lines in any file are line 1 (opening frontmatter fence) and the line immediately after the last frontmatter field (closing frontmatter fence). Every other `---` in a file is a content separator and must be removed. When removing content `---` separators, be careful not to accidentally remove the frontmatter closing fence on line 4 or 5.
- Remove trailing whitespace from all lines.
- Every file must end with a single newline.

### Right sidebar (table of contents) depth

Mintlify renders every `##` and `###` heading as an entry in the right-hand sidebar. Long sidebars hurt scannability.

Target a maximum of **6 entries** in the right sidebar per page. Count every `##` and `###` heading when assessing a page.

If adding `###` headings would push the total above 6, use **bold labels** (`**Label**`) instead. Bold labels give visual structure on the page without creating sidebar entries.

Use `###` headings only when a subsection is substantial enough that a reader would want to navigate directly to it. Prefer bold labels for short subsections, glossary entries, parameter lists, and formula groups.

### Stubs and TODOs
- Pages that are not yet written should still have a clear structure: frontmatter title and description, a `<Note>` saying the page is in progress, and `TODO:` comments that are specific enough for a writer to act on.
- Never leave a page with only `TODO` and a bullet list if you can give it proper section headings instead.
- Always write TODOs as plain text on their own line: `TODO: description of what is needed.`
- Never use HTML comments for TODOs (`<!-- TODO: ... -->`). Mintlify renders these as errors.
- TODOs should be placed on their own line, not inline within a sentence.

### Links
- Always use absolute paths from the site root (e.g. `/safenet/staking/rewards`), not relative paths.
- When referencing a page that exists, link to it. Don't leave "see the staking docs" without an actual link.
- When referencing a page that doesn't exist yet, add a TODO note rather than a broken link.

### Code and technical content
- Include code examples where they help a developer audience, but keep them out of pages targeted purely at Stakers/Delegators.
- Mermaid diagrams are supported and useful for flows (staking, withdrawal, signing rounds).
- Math (LaTeX) is supported for the rewards calculation page; use it there, not elsewhere.

## Source of truth and factual boundaries

- Do not invent tokenomics parameters, reward rates, Validator counts, timelines, or DAO decisions.
- If a parameter (e.g. APR, lock-up duration, Validator minimum stake) is not explicitly stated in the repo, ask before adding it.
- If something depends on future DAO approval, clearly label it as proposed and not final.
- If unsure whether something is live onchain, state that explicitly rather than assuming.
- Do not imply security guarantees beyond what is formally enforced by the protocol.

## Claims and guarantees

Safenet does not guarantee that a transaction is economically safe. It does not prevent all possible attacks. It does not insure user funds. It does not replace user responsibility for reviewing transactions.

Avoid language that implies "guaranteed protection", "fully secure", or "trustless protection against all attacks".

## Terminology consistency

Use canonical terms consistently:
- "Validator" (not checker, node, guardian, etc.)
- "Attestation" (not approval or guarantee)
- "Delegator" (not nominator or Staker, unless specifically referring to Validator self-staking)
- "Safenet Beta" (capitalized, as a proper name)

If you introduce a new term, define it once and reuse it consistently.

### Vale vocabulary and capitalization

A vale spell-check vocabulary is maintained at `.vale/styles/config/vocabularies/safe/accept.txt`. The capitalization in that file is canonical and must be followed exactly in prose.

Current canonical spellings:

| Term | Notes |
|------|-------|
| Attestation, Attestors | Capitalized when used as proper role/concept names |
| calldata, delegatecalls | Lowercase, one word |
| Chainalysis | Proper noun |
| Delegator | Capitalized |
| EOAs, ERC20, ERC721 | Uppercase acronyms |
| Ethereum | Proper noun |
| gasless, offchain, onchain | Lowercase, one word |
| Mainnet | Capitalized |
| Merkle | Capitalized |
| Mintlify | Proper noun |
| Multisig | Capitalized |
| permissioned, permissionless | Lowercase |
| Pimlico | Proper noun |
| Reality.eth | Exact spelling |
| redelegate | Lowercase, one word |
| SafeDAO | Exact spelling |
| Safenet | Capitalized, one word |
| Stakers | Capitalized |
| timelocked, timelock | Lowercase, one word |
| Validator, Validators | Capitalized |
| zkSync | Exact spelling (lowercase z) |

**Exception: file names and link paths.** Do not apply these capitalizations to file names, directory names, or link paths. Those use lowercase kebab-case only (e.g. `/safenet/staking/validator-staking`, not `/safenet/staking/Validator-staking`).

## Beta labeling pattern

Every page that describes live Safenet functionality must:
- Clearly state that Safenet is currently in Beta.
- Specify what is not yet active (e.g. slashing, permissionless Validators).
- Avoid forward-looking guarantees about mainnet launch timelines.

Do not assume Beta means temporary. Describe the current state as it exists.

## Decision-oriented writing

For staking-related pages, always answer these implicitly or explicitly:
- What can I do?
- What do I earn?
- What can go wrong?
- When can I exit?
- What assumptions does this depend on?

If a page does not help a reader make a decision, reconsider its structure.

## Change impact awareness

Before modifying any page that touches staking mechanics, reward calculation, lock-up periods, Validator requirements, or slashing (future), explicitly check:

1. Does this contradict another Safenet page?
2. Does this require updating the FAQ?
3. Does this require updating diagrams?
4. Does this require updating the roadmap or Beta status?

List impacted files in the plan.

## When to refuse or ask for clarification

If asked to fabricate performance metrics, speculate about token price or investment returns, provide legal or financial advice, or announce features not yet approved, respond by asking for clarification or explicitly stating the limitation.

## Mintlify conventions

- Navigation is in `docs.json` under `navigation.tabs[].pages`. Pages can be bare strings (file path without `.md`) or group objects `{ "group": "...", "pages": [...] }`.
- Frontmatter fields used: `title`, `description`, `sidebarTitle` (optional, overrides sidebar label without changing `<h1>`).
- Supported callout components: `<Note>`, `<Warning>`, `<Tip>`, `<Info>`.
- Mermaid fences (` ```mermaid `) render inline.
- LaTeX is supported in `.mdx` files with `$$...$$` blocks.
- The `hidden: true` flag on the Safenet tab hides it from the nav; remove this when the docs are ready to go live.

## Current Safenet nav structure

```
safenet/
├── overview/
│   ├── introduction.md       # What is Safenet?
│   ├── validators.md         # Safenet Validators
│   ├── beta.md               # Safenet Beta (status + Explorer)
│   └── roadmap.md            # Roadmap
├── staking/
│   ├── validator-staking.md  # How are Validators staked?
│   ├── delegate.md           # How to delegate stake?
│   ├── rewards.mdx           # Staking rewards
│   ├── lockup.md             # Staking lock-up periods
│   └── risk.md               # Is my stake at risk? (incl. audits)
└── faq.md                    # FAQs
```
