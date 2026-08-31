# Change Log — Chapters 11 & 12 + Lab Sites Resources Page (EDIT-SPEC-2026-08)

All edits additive per Rule Zero. No existing prose rewritten except the exact corrections quoted below.

---

## Chapter 11 — `chapters/ch11-governance-treasury.md`

### Corrections

1. **Quadratic voting (body, Discussion section).**
   - Old: "**Quadratic voting** makes each additional vote more expensive — your first token gives you one vote, but your second costs two tokens, your third costs three, and so on."
   - New: "**Quadratic voting** makes each additional vote more expensive — *n* votes cost *n²* tokens in total, so each additional vote costs more than the last (the *n*th vote costs 2*n*−1): 1, 3, 5… Ten votes cost 100 tokens; a hundred votes cost 10,000."
   - (Following sentence "This compresses the power of large holders…" retained unchanged.)

2. **Quadratic voting (glossary).**
   - Old: "Your first vote costs 1 token, your second costs 4, your third costs 9."
   - New: "*n* votes cost *n²* tokens in total, so each additional vote costs more than the last (the *n*th vote costs 2*n*−1): 1, 3, 5… Ten votes cost 100 tokens; a hundred votes cost 10,000."

3. **UNI launch price ("Uniswap: Governance as Brand").**
   - Old: "Uniswap's UNI token launched with \$6.43 per UNI and an initial market cap of hundreds of millions of dollars — before…"
   - New: "Uniswap's UNI token began trading near \$3 on September 17, 2020 and roughly doubled within a day, giving it a market cap in the billions — before…"

### Insertions

4. **New section "Managing the Treasury, Not Just Guarding It"** — inserted after "Multisignature Wallets: Nobody Holds the Keys Alone", before "Governance Attacks: What Can Go Wrong". First line: "The multisig answers *who can move the money*." Covers: vault composition (Ch. 4's 50–70% stablecoins restated as policy), runway = stable assets ÷ monthly burn (stablecoins only), written spending policy with thresholds (multisig vs. Realms vote; cross-ref proposal threshold), scheduled/announced diversification, founder's dilemma of selling one's own token (never market-sell into own thin pool — Ch. 5; OTC / time-weighted / announced schedule; Ch. 10 exchange-inflow signal), protocol-owned liquidity as treasury asset (Ch. 5). Includes new figure directive `fig-ch11-treasury-runway` (`../images/ch11-treasury-runway.png`).

5. **New section "The Legal Wrapper: A DAO Is Not Yet a Legal Person"** — inserted after "The Decentralization Spectrum: Where You Actually Sit", before "Activity: Form the DAO". First line: "Your DAO can vote, spend, and execute — but it cannot sign an office lease…" Covers: unincorporated DAO as general partnership with member liability, CFTC v. Ooki DAO (2022 charge, forum service, 2023 default judgment), wrappers: Wyoming DAO LLC, Marshall Islands DAO LLC, Cayman foundation company, Swiss association (Verein); wrapper holds bank account/contracts/taxes while on-chain governance directs it; cross-ref Ch. 12 entity choice and Howey "efforts of others". Includes new figure directive `fig-ch11-legal-wrappers` (`../images/ch11-legal-wrappers.png`).

6. **Lab — Part 1, new Step 7** (appended after existing Step 6): Squads Settings → Members walkthrough (without executing) of adding a fourth signer and raising threshold to 3-of-4; screenshot the proposal screen; framed as Ch. 12 succession step. First line: "In Squads, open **Settings → Members**…"

7. **Lab — Part 2, new Step 6** (appended after existing Step 5): Realms → DAO → Params/Config screenshot; identify proposal threshold, vote duration, execution delay; set 1-hour time lock if configurable and note the effect in Part 3. First line: "In Realms → your DAO → **Params/Config**…"

8. **Lab — new "Part 4: Treasury Policy (15 minutes)"** (inserted after Part 3 Step 8, before "What You Have Built"): half-page treasury policy — target stablecoin %, monthly burn, runway (stablecoins only), spending thresholds (multisig / Realms vote), plan to convert 10% of token holdings to USDC without moving the price (named method). Submitted with executed-proposal screenshot.

9. **Glossary — 4 new entries** appended after "Sybil Attack": Legal Wrapper, DAO LLC, Foundation Company, General Partnership Liability.

10. **End of chapter:** `<!-- NEW IMAGES NEEDED: ch11-treasury-runway.png … ch11-legal-wrappers.png … -->` comment appended after Walk Away With.

---

## Chapter 12 — `chapters/ch12-legal-risk.md`

### Insertions (no corrections were specified for Ch. 12)

1. **New subsection "If It Is a Security: The Exemption Map"** — inserted inside "The Securities Question", at the end of "How Token Design Shifts the Answer" (after "…before launch, not after a subpoena."), before "Disclosure and Transparency". First line: "Concluding that your token is a security is a compliance path, not a dead end." Covers Reg D 506(c) (accredited only, general solicitation allowed, resale restricted), Reg S (offshore), Reg CF (capped public raises via registered portal), Reg A+ (larger qualified public raises); mapping of holding periods / accredited-only restrictions to Token-2022 default-frozen and permanent-delegate extensions (Ch. 3) and compliant RWA tokens (Ch. 2). Includes new figure directive `fig-ch12-exemption-map` (`../images/ch12-exemption-map.png`).

2. **New section "Money Transmission, AML, and FinCEN"** — inserted after "The Securities Question" (immediately after the Exemption Map subsection), before "Disclosure and Transparency: Legal Shield and Marketing Tool". First line: "Securities law is one regulator." Covers: MSB definition and obligations (FinCEN registration, AML program, KYC, state money-transmitter licenses), FinCEN's user / exchanger / administrator distinction, issuer traps (redeeming for fiat, custodial wallet, swap desk), practical rules (self-custody & P2P not transmission; hosted wallet / on-off-ramp is; OFAC applies to everyone — cross-ref USDC freeze authority, Ch. 1). Includes new figure directive `fig-ch12-msb` (`../images/ch12-msb-decision-tree.png`).

3. **New admonition "Regulatory Snapshot — as of August 2026"** (`:class: note`) — inserted at the end of "The Launch Checklist as a Living Document", after the "living documents… reviewed quarterly" paragraph. Bullets exactly per spec: SEC posture (Crypto Task Force, memecoin staff statement Feb 2025, protocol staking statement May 2025, staff statements not rules), GENIUS Act (signed July 18 2025; permitted payment stablecoin issuers; 1:1 reserves; full effect early 2027), Digital Asset Market Clarity Act (H.R. 3633; passed House July 2025; Senate Banking Committee May 2026; awaiting Senate floor vote Sept 2026), MiCA (fully in force since Dec 30 2024). Closing line: "Update this box every term; the dates above are the last verification."

4. **"The Threat Landscape" — pointer sentence appended at end of section** (after the Emergency Panic Attack warning box): "DeFi-specific risks — oracle manipulation, bridge exploits, liquidation cascades, composability failure — are covered in Chapter 5, *DeFi Risk*; treat every protocol you integrate as part of your attack surface."

5. **Launch checklist — 2 new items** appended to Pre-Launch → "Legal and disclosure": "[ ] Tax treatment of the airdrop, contributor payments, and treasury sales reviewed (Chapter 6)" and "[ ] MSB/money-transmitter analysis completed if you custody, redeem, or exchange for customers".

6. **Lab "Red-Team Your Own Project" — Individual Analysis, 3 new items** appended after item 5: item 6 **Buyer's Check yourself** (run Ch. 10's 60-second check; paste into one-page explainer's Risks section); item 7 **Phishing drill** (write the scammer's exact Discord message, then the pinned security rule that defeats it); item 8 **Regulator drill** (one paragraph each: security? — Howey; money transmitter? — FinCEN section; airdrop recipients' tax? — Ch. 6 box).

7. **Glossary — 5 new entries** appended after "Succession Planning": FinCEN, Money Services Business (MSB), AML, KYC (with cross-ref to Ch. 1 custodial onboarding), OFAC.

8. **End of chapter:** `<!-- NEW IMAGES NEEDED: ch12-exemption-map.png … ch12-msb-decision-tree.png … ch12-regulatory-snapshot.png … -->` comment appended after the seealso block.

---

## New file — `resources/lab-sites.md`

- Created MyST resources page "Lab Sites Reference" with front matter matching house style, the full sites table from spec Section 6, and a `:::{note}` admonition: "**Last verified: August 2026.**" plus guidance to re-check before starting labs.

## `myst.yml`

- TOC: added entry `Lab Sites Reference → resources/lab-sites.md` at the end, after the Chapter 12 entry. No other TOC changes.
