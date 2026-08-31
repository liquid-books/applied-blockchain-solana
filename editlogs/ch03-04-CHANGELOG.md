# Change Log — Chapters 3 & 4 + Tokenomics Model (Edit Spec 2026-08)

**Scope:** `chapters/ch03-launch-your-token.md`, `chapters/ch04-tokenomics.md`, `resources/ch04-tokenomics-model.xlsx` (new).
**Rule Zero compliance:** all changes are insertions or spec-quoted corrections. No existing prose was reworded, moved, or deleted beyond the exact quoted corrections below. Book-wide SOL price constant: **SOL ≈ $100** (per author correction, 2026-08-31).

---

## Chapter 3 — Launch Your Token (`chapters/ch03-launch-your-token.md`)

### Corrections (old → new)

1. **"The Squarespace Analogy" section.**
   - Old: `**Solana Token Creator** by Orca`
   - New: `**Solana Compass's Token Creator** (solanacompass.com/tools/create-solana-token)`
   - Reason (spec): Orca is a DEX with no token-creator product. Smithii and SPL Token UI unchanged.

2. **"Associated Token Accounts" section — ATA rent dollar figure** (spec's "Cost Anatomy" alignment; the figure lives in the ATA section).
   - Old: `approximately 0.002 SOL, about $0.30 at typical prices`
   - New: `approximately 0.002 SOL, about $0.20 at SOL ≈ $100`

### Insertions

3. **New section `## Token-2022: Extensions for Business Tokens`** — inserted after the "Three Powers" section (after the authority-revocation-roadmap figure), before "Associated Token Accounts".
   - First line: "There are two token programs on Solana."
   - Contents: two-token-programs framing with compatibility note (Phantom/Solscan/Jupiter/Raydium CPMM yes; Raydium AMM v4 and legacy tools no); one paragraph each on the 8 extensions (transfer fee, non-transferable, permanent delegate, default account state/frozen, confidential transfers, interest-bearing, metadata pointer/on-chain metadata, transfer hook), each tied to the chapter cross-reference the spec names; decision table (`### Which Extensions for Which Token?`) with rows for the four Ch. 2 token types plus "regulated asset" and a "what a buyer should think" column (permanent delegate on a community token = walk away); "Where the Analogy Breaks Down" admonition (extensions set at mint creation; permanence decision); new figure directive `fig-ch03-token2022` → `../images/ch03-token2022-extensions-table.png`.

4. **Lab: new `### Step 8: Read a Token-2022 Token in the Wild (10 min)`** — inserted after Step 7's final paragraph, before "### Deliverable".
   - First line: "On Solscan, open the PYUSD (PayPal USD) mint: `2b1kV6DkPAnxd5ixfnxCpjxmKwqjjaYmCZfHsFu24GXo`."
   - PYUSD Owner Program check, Extensions panel exercise, comparison to student's own token. Per spec verbatim.

5. **Lab: new `### Step 3b (Optional, Devnet): Mint a Token-2022 Test Token`** — inserted immediately after Step 8, before "### Deliverable" (appended per spec's "extend means append"; existing steps not renumbered).
   - First line: "Switch Phantom to devnet (Settings → Developer Settings → Testnet Mode)."
   - Smithii Tax Token Creator on devnet, 1% transfer fee, withheld-fee observation. Per spec verbatim.

6. **Glossary: 9 new entries appended** after "Mainnet-Beta": Token-2022, Transfer Fee (Extension), Non-Transferable (Extension), Permanent Delegate (Extension), Default Account State (Extension), Confidential Transfers (Extension), Interest-Bearing (Extension), Metadata Pointer (Extension), Transfer Hook (Extension). Existing entries untouched.

7. **End of chapter:** `<!-- NEW IMAGES NEEDED: ch03-token2022-extensions-table.png ... -->` comment appended after the closing "Next: Chapter 4" line.

---

## Chapter 4 — Tokenomics on a Napkin (`chapters/ch04-tokenomics.md`)

### Insertions (no corrections were specified for this chapter)

1. **Pointer sentence** appended to the end of the "The Circular Yield" failure-pattern paragraph:
   - "Chapter 5's *Real Yield vs. Emissions Yield* gives the mechanism and a test you can run on any advertised APY."

2. **Pointer** appended to the "Collateral" bullet in the Velocity sink list:
   - Old bullet ending: `…to access loans or derivatives`
   - New bullet ending: `…to access loans or derivatives (how lending markets do this: Chapter 5, *Beyond the Pool*)`

3. **New section `## The Other Side of the Napkin: Demand`** — inserted after "Velocity: The Hidden Killer", before "Reading a Tokenomics Table Like an Investor".
   - First line: "Everything in this chapter so far — supply, allocation, vesting, unlocks — describes one curve."
   - Contents (the spec's 4 numbered items): (1) minimum demand model using Ch. 7 tier thresholds (100/500/2,000/10,000) and the chapter's worked-example numbers ($200,000 fees → 2M tokens burned at $0.10 ≈ 167k/mo); (2) implied price band — sink demand vs. circulating float; (3) the inflection, computed with the worked example's year-1 (417k/mo issued vs. 167k/mo burned) and year-2 (≈437.5k vs. ≈417k/mo) numbers; (4) the napkin-not-a-valuation caveat. New figure directive `fig-ch04-inflection` → `../images/ch04-demand-vs-supply-inflection.png`.

4. **Activity "Model Three Futures": new `**Step 5: Add the demand column.**`** — appended after the sample investor justification note (end of Step 4), before the Discussion section. Users at months 1/6/12 × Ch. 7 tier requirement + monthly burns vs. unlocks; mark the inflection month or note its absence within 12 months and what to change.

5. **Spreadsheet note** — `:::{note}` admonition inserted directly after Step 5, pointing to `resources/ch04-tokenomics-model.xlsx` with its four tabs (Allocation, Vesting, Circulating, Demand) and noting the formulas are live.

6. **End of chapter:** `<!-- NEW IMAGES NEEDED: ch04-demand-vs-supply-inflection.png ... -->` comment appended after the Key Takeaways block.

### Reverted self-edit (for transparency)

- During editing, Step 4's bold line was briefly modified with a parenthetical; this violated Rule Zero and was reverted to the original text in the same session. Final file contains the original Step 4 line unchanged.

---

## New file — `resources/ch04-tokenomics-model.xlsx`

Built with exceljs; **all derived cells are formulas** (cross-tab cell references), not hardcoded values. Seeded with the chapter's worked-example / Balanced-scenario defaults.

- **Allocation tab:** Total Supply input (100,000,000); six categories (Team & Founders 20% / 12-mo cliff / 48-mo vest, Investors 12% / 30-mo vest, Community 35% / 48-mo vest, Liquidity Pool 8% / immediate, Marketing 5% / 12-mo vest, Treasury 20% / 36-mo vest — the chapter's Scenario C "Balanced"); Tokens column = `%×TotalSupply` formulas; TOTAL row = SUM formulas.
- **Vesting tab:** months 0–36; per-category cumulative unlocked formulas referencing Allocation: `IF(vest=0, all, IF(month<cliff, 0, tokens×MIN(month/vest,1)))` — reproduces the chapter's cliff behavior (month 12 of a 48-month vest unlocks 25% at once, then ~2.1%/month); Total Unlocked = row SUM.
- **Circulating tab:** months 0–36; Circulating Supply = `Vesting!H` reference; % of Total Supply = `÷Allocation!$B$1`; Monthly Unlocks = first-difference formula.
- **Demand tab:** input block (starting users 100, 25% monthly growth, 500 tokens held/user = Ch. 7 Builder tier, $16,667/mo fees ≈ $200k/yr, $0.10 price, 5% annual emissions — all from the chapter's worked example); months 1–36 with Users (compounding formula), Tokens Locked (`users×held`), Newly Locked (first difference), Monthly Burns (`fees÷price`), Monthly Unlocks (`Circulating!D` reference), Monthly Emissions (`TotalSupply×rate÷12`), Net Demand `=(burns+newlyLocked)−(unlocks+emissions)`, and Inflection indicator `=IF(burns+newlyLocked>=unlocks+emissions,"INFLECTION","-")`.

---

## New images needed (added as end-of-chapter comments)

- `ch03-token2022-extensions-table.png`
- `ch04-demand-vs-supply-inflection.png`
