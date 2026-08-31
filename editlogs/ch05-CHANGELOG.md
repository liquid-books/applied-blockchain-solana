# Chapter 5 Change Log — Additive Edit per EDIT-SPEC-2026-08

**File:** `chapters/ch05-liquidity-raydium.md`
**Date:** 2026-08-31
**SOL price constant used:** $100 (per author correction of 2026-08-31)

All changes are (a) insertions at spec-named locations or (b) the exact quoted corrections. No existing prose was rewritten, reworded, moved, or deleted beyond the quoted correction text.

---

## Corrections (old → new)

1. **Glossary, "Raydium"**
   - Old: "A major decentralized exchange and AMM protocol on the Solana blockchain. Raydium is notable for combining on-chain AMM pools with access to Serum's central limit order book, and for its integration with the Jupiter aggregator."
   - New: "A major Solana DEX offering constant-product (Standard/CPMM) and concentrated-liquidity (CLMM) pools, integrated with the Jupiter aggregator."
   - Reason: Serum defunct since late 2022.

2. **Step 2, Scenario A**
   - Old: "At SOL = \$150, that prices your token at roughly \$0.015 each"
   - New: "At SOL = \$100, that prices your token at roughly \$0.01 each"

3. **Step 2, Scenario B**
   - Old: "At SOL = \$150, that prices your token at roughly \$0.075 each"
   - New: "At SOL = \$100, that prices your token at roughly \$0.05 each"

4. **Step 2, Scenario C**
   - Old: "At SOL = \$150, that prices your token at roughly \$0.15 each"
   - New: "At SOL = \$100, that prices your token at roughly \$0.10 each"

5. **"What You Need" admonition (Activity)**
   - Old: "At minimum \$20 worth of SOL in your wallet (more is better for meaningful liquidity)"
   - New: "At minimum 0.15 SOL for Raydium's pool-creation fee, plus the SOL you will deposit into the pool, plus ~0.02 SOL for rent and transaction fees"

6. **Step 5 "Initialize the Pool"**
   - Old: "Approve both. The total cost will depend on current Solana network fees but should be under \$1 in total transaction fees for the initialization, plus whatever SOL you deposited into the pool."
   - New: "Approve both. Raydium charges a one-time 0.15 SOL pool-creation fee (shown in the confirmation), plus under \$1 in rent and transaction fees, plus whatever SOL you deposit."

7. **Step 3 "Create the Standard AMM Pool" — CPMM labeling (additive sentence to first line)**
   - Old first line: "On Raydium, navigate to **Liquidity** → **Create Pool** → **Standard AMM**."
   - New first line: same + appended: "The pool type is labeled **Standard AMM (CPMM)** in Raydium's interface — this is the CPMM program, which is what the *Pool Types* section earlier in this chapter and the *Burn & Earn* step later in this lab refer to."

*(Note: the index.md "$20" framing correction belongs to the index.md editor's scope, not this file.)*

---

## Insertions

### A. New section `## Pool Types: Constant Product vs. Concentrated Liquidity`
- Location: after "The Constant Product Formula: Two Piles of Coins", before "Price Discovery: Why the Pool Wins".
- First line: "The x·y=k pool has a quiet inefficiency: it spreads your capital across *every possible price* from zero to infinity."
- Contents: CPMM inefficiency, CLMM/Whirlpools/DLMM, in-range depth vs. out-of-range zero earnings + full IL, irrigation analogy, rule of thumb (constant product for new tokens / concentrated once a range exists), cross-ref Ch. 10 *Liquidity Depth*. Includes figure `ch05-cpmm-vs-clmm.png`.

### B. New subsection `### MEV and the Sandwich`
- Location: end of "Slippage, Pool Depth, and the Thin Liquidity Problem", before "LP Tokens and Fees".
- First line: "Slippage has a predator."
- Contents: sandwich attack mechanics, Jupiter slippage tolerance as attacker budget, MEV definition, Jito bundles and MEV tips in staking yield (cross-ref Ch. 4 and *Real Yield vs. Emissions Yield*), practical rule (low slippage, never auto/unlimited on thin pools). Includes figure `ch05-sandwich-attack.png`.

### C. New section `## Launchpads and Bonding Curves`
- Location: after "Centralized Exchanges as Gatekeepers vs. Decentralized Rails", before "Activity: Open the Market".
- First line: "There is a second way to open a market — one that requires no seed capital at all…"
- Contents: bonding curve as one-sided pool, launchpads and graduation, pump.fun → PumpSwap (post-March 2025), Raydium LaunchLab → CPMM pool, three reasons it matters (volume, fair-launch argument, visible rug-pull mechanics / deployer-buys-first), cross-refs to Ch. 2 memecoins and Ch. 12 rug pulls. Includes figure `ch05-bonding-curve-migration.png`.

### D. New section `## Managing Liquidity After Launch`
- Location: after "Reading Your Position Over Time", before "Beyond the Pool: The DeFi Stack".
- First line: "Opening the pool is day one. What you do with it afterward is a signal every buyer reads."
- Contents: adding liquidity as demand grows; removing liquidity read as a warning; protocol-owned liquidity (cross-ref Ch. 11); locking/burning LP tokens incl. Burn & Earn + Fee Key NFT (cross-ref Ch. 12, lab Step 7); market makers and CEX listings only after organic metrics (cross-ref Ch. 10).

### E. New section `## Beyond the Pool: The DeFi Stack` (the DeFi section)
- Location: after "Managing Liquidity After Launch", before "The Broader Picture: What You Just Built".
- First line: "The pool you just built is one of five primitives that, composed together, are what 'decentralized finance' actually means…"
- Opening: two paragraphs (five primitives, money legos, programs calling programs, cross-ref Ch. 8). Figure `ch05-defi-stack-overview.png`.
- Subsections, all as specified:
  1. `### 1. Stablecoins: The Unit of Account` — definition + USDC's roles; three backing models (fiat-reserve USDC / crypto-collateralized DAI + MakerDAO cross-ref Ch. 11 / algorithmic UST collapse); USDC freeze authority & "not your issuer, not your dollars" (cross-refs Ch. 1, Ch. 3); March 2023 depeg; GENIUS Act paragraph (July 2025, permitted issuers, 1:1 reserves, monthly disclosure, redemption at par, OCC/Treasury rules through 2026, full effect early 2027, cross-ref Ch. 12). Figure `ch05-stablecoin-backing-models.png`.
  2. `### 2. Staking and Liquid Staking: Yield on the Base Asset` — native staking (delegation ≠ custody, epoch unstaking), liquid staking (mSOL/JitoSOL, tradable/poolable/collateral while earning, smart-contract risk + discount risk), one sentence on restaking flagged beyond scope. Figure `ch05-staking-yield-decomposition.png`.
  3. `### 3. Lending Markets: Borrowing Against What You Hold` — utilization curve, Kamino/Marginfi, over-collateralization worked numbers ($100 SOL → ~$70 USDC @ 70% LTV), health factor formula, liquidation as open bounty, collateral as Ch. 4's deepest sink, thin-pool liquidation cascade, "Where the Analogy Breaks Down" (bank calls; program doesn't). Figures `ch05-lending-market-health-factor.png`, `ch05-liquidation-cascade.png`.
  4. `### 4. Oracles: Where the Price Comes From` — why not one pool, Pyth (publishers + confidence interval), Switchboard, downstream dependence (Ch. 7 Pricing Problem, Ch. 2 RWA), exploit surface. Figure `ch05-oracle-flow.png`.
  5. `### 5. Real Yield vs. Emissions Yield` — the one-sentence test; SOL staking decomposition; LP fees as real yield; three-line LEARN worked example (0.25% fees on $40 volume / $20 pool ≈ 6% annualized real vs. minted-LEARN "45% APY" emissions; delete-the-emissions-line test); ties to Ch. 4 Circular Yield.
  6. `### 6. DeFi Risk` — five named risks each in one paragraph: smart-contract risk (cross-ref Ch. 8 auditor checklist), oracle manipulation, liquidation cascades, bridge risk (cross-ref Ch. 0 box, Wormhole/Ronin), composability risk; closing defenses list.
  7. `### 7. The DeFi Map` — TVL, DeFiLlama by chain/protocol, category recognition (DEX/lending/liquid staking/perps), double-counting caveat.

### F. Lab extensions to "Activity: Open the Market"
- `### Step 7: Lock It (10 min)` — inserted after "Verify Your Pool on Solscan". Burn & Earn walkthrough (Liquidity → Create → Burn & Earn, confirmation sentence, Fee Key NFT, observation-only alternative), RugCheck step (score + line items + screenshots), two-sentence write-up. Includes figure `ch05-rugcheck-annotated.png`.
- `### Step 8: Watch a Bonding Curve (10 min, observation only, no purchase)` — pump.fun board, DexScreener migration check, Solscan deployer share, two-sentence write-up.
- Lab notebook table: three new rows appended — "LP locked/burned (Y/N, %)", "RugCheck score", "Slippage tolerance used on the Jupiter swap".

### G. New lab `## 🔬 Hands-On Lab: DeFi in an Afternoon (90 min, mainnet, ≈ $10 at risk)`
- Location: after the extended Activity (after Step 8), before "Reading Your Position Over Time".
- Preface: "This lab is designed for a second class session. Every step uses small amounts; every step ends with something recorded."
- Part A — Hold a Dollar (Phantom swap 0.02 SOL→USDC; USDC mint authorities on Solscan; holders; write-up).
- Part B — Stake It (native staking by observation with 1 SOL minimum note + ≥1 SOL alternative; Marinade 0.05 SOL executed; Jito observation; inflation-rate write-up).
- Part C — Borrow Against It (Kamino Main Market, Marginfi alternative; supply 0.05 SOL/mSOL; borrow 1 USDC; record Net Value/LTV/Liquidation LTV/Health; liquidation price check; repay + withdraw; why-not-listed write-up).
- Part D — Find the Oracle (Pyth SOL/USD feed: price, confidence, publishers; compare to own pool; write-up).
- Part E — Read the Map (DeFiLlama Solana TVL + top five labeled; Part B/C protocol TVLs; three-sentence write-up).
- Deliverable — The DeFi Lab Sheet (one-page table, five answers, five transaction signatures).

### H. Second Discussion prompt
- Location: after the existing "Discussion Prompt" admonition (existing prompt untouched), before "Discussion Guidelines".
- Added `:::{admonition} Discussion Prompt 2` (`:class: important`): "Your pool, your stake, your loan and its oracle all ran without a bank, a broker, or a clearinghouse. Which of those institutions did DeFi actually replace today, which did it merely hide (the validator, the oracle publishers, the issuer of USDC), and who do you call when the program is wrong?" + line "The same guidelines below apply to this prompt."

### I. Glossary additions (appended after existing "Standard AMM" entry; all existing entries untouched except the "Raydium" correction above)
Concentrated Liquidity · MEV · Sandwich Attack · Bonding Curve · Launchpad · Protocol-Owned Liquidity · Liquidity Lock · Stablecoin · Fiat-Reserve Stablecoin · Crypto-Collateralized Stablecoin · Algorithmic Stablecoin · Depeg · Staking · Delegation · Validator Commission · Epoch · Liquid Staking Token (LST) · Lending Market · Utilization Rate · Loan-to-Value (LTV) · Health Factor · Liquidation · Liquidation Cascade · Price Oracle · Pyth · Real Yield · Emissions Yield · Total Value Locked (TVL) · Composability Risk · Money Legos

### J. New figure directives added (10) + `NEW IMAGES NEEDED` comment at file end
`ch05-cpmm-vs-clmm.png` · `ch05-sandwich-attack.png` · `ch05-bonding-curve-migration.png` · `ch05-rugcheck-annotated.png` · `ch05-defi-stack-overview.png` · `ch05-stablecoin-backing-models.png` · `ch05-staking-yield-decomposition.png` · `ch05-lending-market-health-factor.png` · `ch05-oracle-flow.png` · `ch05-liquidation-cascade.png`
