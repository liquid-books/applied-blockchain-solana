# TokenSystems Gap Audit — Full Edit Specification

**Book:** *TokenSystems.io: Build a Token Economy on Solana* (Dr. Ernesto Lee) — 13 chapters (Ch. 0–12), MyST Markdown, repo `liquid-books/applied-blockchain-solana`
**Audit basis:** every chapter read in full from source; each finding verified against the text
**Constraints:** (1) no new chapters; (2) **additive only — the existing book is not to be rewritten.**
**Purpose of this document:** a complete, chapter-by-chapter specification of what to ADD, that an editing AI can execute in one pass.

**BOOK-WIDE SOL PRICE CONSTANT (set by editor): SOL ≈ $100. Use in index.md note and Ch. 1, 3, 5, 6 dollar figures.**

---

## 0. Instructions for the editing AI

Read this section before touching any file.

> ### ⛔ RULE ZERO — ADDITIVE ONLY
> The book as written is good and stays as written. Your job is to **insert new material** at the locations named below and to make the **small, specific factual corrections** listed under "Corrections" (a wrong number, a wrong tool name, a broken link, a duplicated glossary entry). You must **not**:
> - rewrite, reword, condense, "improve," or restructure any existing paragraph, section, lab step, discussion prompt, figure, video block, or glossary entry that this spec does not explicitly name;
> - move existing sections;
> - change the author's voice, analogies, examples, or chapter openings;
> - delete anything except the exact text a "Corrections" line tells you to replace.
>
> Every change you make should be either (a) a block of new text inserted at a named location, or (b) a one-line correction quoted in this spec. If you are unsure whether something is an insertion or a rewrite, it is a rewrite — do not do it. When finished, produce a change log listing every insertion (chapter, section, first line of inserted text) and every correction (old text → new text) so the author can review them.

1. **Do not add chapters.** All additions are inserted into the 13 existing chapter files plus `index.md`.
1a. **DeFi lives in one place: Chapter 5.** All DeFi material (stablecoins, staking, liquid staking, lending, collateral, liquidation, oracles, yield, DeFi risk) is a single long section in Ch. 5 with one consolidated lab. Other chapters receive at most a one-line cross-reference to it.
2. **Match the house format.** The book is MyST Markdown. Use these existing conventions exactly:
   - Figures: `:::{figure} ../images/chNN-slug.png` with `:label:`, `:alt:`, `:width: 80%`, `:align: center`, a bold caption line, and closing `:::`. For any new figure, create the directive with a descriptive `:alt:` and add the filename to a `NEW IMAGES NEEDED` list at the end of the chapter (the author will generate the images).
   - Callouts: `:::{admonition} Title` with `:class: note|tip|warning|important|seealso`, or the short forms `:::{note}`, `:::{tip}`, `:::{warning}`.
   - Videos: a bold `**▶ Watch: Title (N min)**` line followed by the responsive `<div>`/`<iframe>` block used throughout the book.
   - Glossaries: a fenced ```{glossary}``` block with `Term` on one line and a two-space-indented definition on the next.
   - Standard end-of-chapter sections, in this order where present: `🎯 In-Class Assignment`, `🔬 Hands-On Lab` (or `Activity`), `💬 Discussion`, `Glossary`, `Walk Away With`, `Leader's Takeaway` / `Key Takeaways`.
   - Voice: second person, direct, business-first, one analogy per concept followed by a "Where the Analogy Breaks Down" note when the analogy is imperfect. No hype words ("revolutionary," "ecosystem," "community" as filler).
3. **Every lab step must be executable by a non-programmer** with a browser, Phantom, and a small SOL balance. Name the exact site, the exact button or menu path where known, what the student should observe, and what they record.
4. **Keep the running token.** The token minted in Ch. 3 on mainnet is used in Ch. 5, 7, 9, 11. Where a lab must run on devnet (Ch. 6, Ch. 8), say so explicitly and tell the student to mint a throwaway devnet token.
5. **Cross-references:** when a new section relies on a concept in another chapter, add a one-line cross-reference ("see Chapter 3, *Token-2022*").
7. **Every tool, URL, cost, and fact in this spec was verified live in August 2026.** Where a tool named in the existing book has shut down, this spec names the replacement and the exact steps; use them as written.
8. **Do not rewrite existing prose that is not named here.** Insert, extend, and correct only what this spec calls for. (See Rule Zero.)
9. **"Extend" means append.** Where this spec says to extend a lab or section, add new numbered steps or paragraphs after the existing ones. Do not renumber, merge, or edit the existing steps.

---

## 1. Verdict and coverage scorecard

**Verdict.** The book's spine holds: NAAT canvas → token brief → live mint → live pool → distribution → utility → program → NFTs → analytics → DAO → launch document. Nine of thirteen chapters are strong for their scope. The gaps cluster in three places: (1) DeFi and financial plumbing — "DeFi" currently means one AMM pool; stablecoins, staking, lending, collateral, oracles are named but never explained; (2) the smart-contract chapter shows no code and never touches a token; (3) the 2024–26 Solana toolkit — Token-2022 extensions, concentrated liquidity, liquidity locks, launchpads, memecoins — is absent.

| Subject | Rating | Home after this edit |
|---|---|---|
| Blockchain fundamentals, NAAT, decision test | Strong | Ch. 0 (+ beginner lab) |
| Keys, wallets, custody | Strong | Ch. 1 (+ embedded-wallet paragraph) |
| Token design | Strong | Ch. 2 (+ memecoin section) |
| SPL launch, authorities, metadata | Strong | Ch. 3 (+ Token-2022) |
| Tokenomics | Strong | Ch. 4 (+ demand model) |
| AMM mechanics | Strong | Ch. 5 |
| **Pool types, launchpads, MEV, liquidity locks** | Thin → **Ch. 5** | new sections + lab steps |
| **DeFi — stablecoins, staking, liquid staking, lending, collateral, liquidation, oracles, real vs. emissions yield, DeFi risk** | Missing → **Ch. 5, one long section "Beyond the Pool: The DeFi Stack"** | new section + one consolidated lab |
| Distribution | Strong | Ch. 6 (+ tax box) |
| Utility without code | Strong | Ch. 7 (+ Solana Pay) |
| Smart contracts | Thin → extended | Ch. 8 (+ code, PDAs/CPI, auditor checklist) |
| NFTs | Strong (with fixes) | Ch. 9 |
| Analytics | Strong | Ch. 10 (+ buyer's check, Dune) |
| Governance | Strong | Ch. 11 (+ treasury mgmt, legal wrapper) |
| Legal — Howey | Strong | Ch. 12 |
| **FinCEN/AML, exemptions, tax, DeFi risk, regulatory currency** | Missing/promised → **Ch. 12** | new sections |

**Where DeFi lives (no new chapter): one section in Chapter 5.** Chapter 5 is already the book's DeFi chapter — it opens with the 31-minute "Introduction to DeFi" video and builds the first DeFi primitive, the AMM pool. Everything else that "DeFi" means is added there as **one long section, "Beyond the Pool: The DeFi Stack,"** inserted after "Reading Your Position Over Time" and before "The Broader Picture," with **one consolidated lab, "DeFi in an Afternoon."** Contents, in order: stablecoins → staking and liquid staking → lending, collateral, liquidation → oracles → real yield vs. emissions yield → DeFi risk → the DeFi map. Chapter 5 becomes the longest chapter; the lab is designed to run as a second class session.

Other chapters get one-line pointers only:

| Chapter | One-line pointer to add (no other DeFi content) |
|---|---|
| Ch. 1, "Custody Models" | "Stablecoins such as USDC add a second custody question — the issuer's — covered in Chapter 5, *Beyond the Pool*." |
| Ch. 4, "The Circular Yield" failure pattern | "Chapter 5's *Real Yield vs. Emissions Yield* gives the mechanism and a test you can run on any advertised APY." |
| Ch. 4, "Velocity" sink list, "Collateral" bullet | "(how lending markets do this: Chapter 5, *Beyond the Pool*)" |
| Ch. 7, "The Pricing Problem," dollar-denominated bullet | "…using a price oracle such as Pyth (Chapter 5, *Oracles*)." |
| Ch. 10, "Liquidity Depth" | "For the chain-wide version of this number see DeFiLlama (Chapter 5, *The DeFi Map*)." |
| Ch. 12, "The Threat Landscape," end | "DeFi-specific risks — oracle manipulation, bridge exploits, collateral cascades — are covered in Chapter 5, *DeFi Risk*; treat any protocol you integrate as part of your attack surface." |

---

## 2. Global fixes (apply across files)

| Location | Fix |
|---|---|
| `index.md` line ~126 | Ch. 5 card links to `./chapters/ch05-raydium-liquidity.md`; file is `ch05-liquidity-raydium.md`. Live link 404s. Fix the path. |
| `index.md` Ch. 10 card | Says "Dune Analytics, Solscan…". Ch. 10 never uses Dune. Keep the card and add the Dune step to Ch. 10 (specified below). |
| `index.md` Ch. 12 card | Says "FinCEN compliance." Ch. 12 never mentions FinCEN. Add the section to Ch. 12 (specified below). |
| `index.md` "Why Solana" | Add: "Dollar figures throughout this book assume SOL ≈ $100. Recompute with the current price." Use $100 in Ch. 1, 3, 5, 6. |
| All chapters | "65,000 transactions per second" → "a theoretical ceiling of 65,000 TPS; sustained real-world throughput is in the low thousands." |
| Ch. 2 glossary | Convert from bold-prose to the ```{glossary}``` directive used by every other chapter. |
| Ch. 0 glossary | Remove the duplicate "Genesis Block" entry. |

---

## 3. Chapter-by-chapter specification

### Chapter 0 — What Is a Blockchain?

**Small factual corrections (replace only the quoted text; nothing else in the chapter changes)**
- "The Trust Problem": change "Seven hundred billion dollars in shareholder value evaporated" to roughly "$74 billion" (Enron's peak market value was ~$70B).
- "The Revolution You Just Understood": fix the garbled sentence "In the United States today, approximately 1.8 billion adults globally lack access…" → "Globally, about 1.4 billion adults lack access to formal banking (World Bank Global Findex)."
- Qualify "65,000 TPS" per the global fix.
- Glossary: delete duplicate "Genesis Block."

**Additions**
- In the `Alternative Chains — Different Tradeoffs` admonition, add one paragraph: what a bridge is (lock on chain A, mint a "wrapped" representation on chain B), why bridges hold enormous pooled value and have been the site of the largest hacks (Wormhole 2022, Ronin 2022), and that Wormhole is Solana's primary bridge. One sentence of cross-reference to Ch. 12's threat landscape.

**New lab — insert before "🎯 Activity: The NAAT Canvas" as `🔬 Hands-On Lab: See a Blockchain Work (30 minutes)`**

Purpose: before the NAAT canvas, every student manipulates a hash, breaks a chain, and watches two live networks produce blocks. No wallet needed.

Part 1 — Hashes (5 min)
1. Open `https://andersbrownworth.com/blockchain/hash`.
2. Type your full name in the Data box. Copy the 64-character hash into your notes.
3. Change one letter of your name. Observe the entire hash change. Record the new hash.
4. Paste a paragraph of any length. Observe the hash is still 64 characters.
5. Write one sentence: why can't you work backwards from the hash to the paragraph?

Part 2 — A block (5 min)
1. Open `https://andersbrownworth.com/blockchain/block`.
2. Type any data. Notice the block shows red (invalid) because the hash does not start with the required zeros.
3. Click **Mine**. Watch the Nonce field count up until a valid hash is found. Record the nonce.
4. Change one character of the data. The block turns red again. This is why editing a block requires re-mining it.

Part 3 — Break a chain (10 min)
1. Open `https://andersbrownworth.com/blockchain/blockchain`. Five linked blocks appear, all green.
2. Edit the data in Block 2. Observe Blocks 2, 3, 4, and 5 all turn red — every later block contains Block 2's old hash.
3. Click **Mine** on Block 2. It turns green; 3, 4, 5 stay red. Mine each one in order until the chain is green again. Count how many mines it took.
4. Write one sentence: on a real network with thousands of nodes adding new blocks every 400 ms, why can an attacker never finish this catch-up?

Part 4 — Distributed copies (5 min)
1. Open `https://andersbrownworth.com/blockchain/distributed`. Three peers (A, B, C) each hold an identical chain.
2. Edit Block 3 on Peer B and re-mine it and every block after it until Peer B's chain is fully green.
3. Compare the final hash of Block 5 on Peer B to Peer A and Peer C. They differ. Write one sentence: how do A and C know B is lying?

Part 5 — Two live networks (5 min)
1. Open `https://mempool.space`. Watch the block row at the top. Note the time since the last Bitcoin block and the average block interval (~10 min). Note the fee estimates in sat/vB.
2. Open `https://explorer.solana.com` and click **Live Cluster Stats** (or observe the stats panel on the home page). Note the current slot number, transactions per second, and the block time (~400 ms). Wait 10 seconds and note how many slots advanced.
3. Click any recent Solana block. Note the number of transactions in it and the "Block Hash" and "Parent Block Hash" fields — this is Part 3, live.

Deliverable: a one-page PDF with your four screenshots (hash, broken chain, peers disagreeing, Solana block with parent hash highlighted) and your four one-sentence answers.

---

### Chapter 1 — Your First Transaction

**Small factual corrections (replace only the quoted text; nothing else in the chapter changes)**
- "Phantom: Solana's Primary Wallet": delete "open-source" (Phantom is closed-source; audited). Replace "over 3 million active users" with "more than 15 million monthly active users."
- "The Ethereum Challenge": after the Layer-2 parenthetical, add two sentences acknowledging that Ethereum L2s (Base, Arbitrum) are the realistic 2026 comparison on fees and speed, and that the book's argument for Solana rests on a single integrated execution layer with no bridging between L1 and L2.
- Apply the SOL-price assumption note ($100).

**Addition — append to "Custody Models: Self-Custody vs. Custodial Wallets" (after the Hardware Wallets subsection, as a fourth subsection):**

`### Embedded Wallets` — two paragraphs: wallet-as-a-service inside an app (Privy, Dynamic, and wallet vendors' embedded SDKs), passkey login, the user never sees a seed phrase; the trade-off is convenience and recoverability vs. the app provider becoming a quasi-custodian. One sentence cross-ref to Ch. 7's UX discussion. Add glossary entry: Embedded Wallet.

**Pointer — one sentence at the end of "Custody Models":** "Stablecoins such as USDC add a second custody question — the issuer's — covered in Chapter 5, *Beyond the Pool*."

---

### Chapter 2 — Design Your Token

**Small factual corrections (replace only the quoted text; nothing else in the chapter changes)**
- Convert the glossary to the `{glossary}` directive.

**New section — insert after "The 'Why Would Anyone Want This?' Test", before "Activity: Write Your Token Brief":**

`## The Hardest Version of the Test: Memecoins`

Cover:
1. Definition: a token whose stated representation is none of the four (payment, access, ownership, reputation) — its value is attention. Name that Solana has been the dominant chain for memecoins since 2023 (BONK, WIF as examples of ones that persisted).
2. Run the actor table on a memecoin honestly: reason to hold = expected price appreciation from more attention; reason to spend = none; sink = none. It fails Failure Pattern 1 by construction — and some still succeed for a while. Explain why: attention is a real, if perishable, resource, and a memecoin is a coordination game, not a business.
3. What a business student should take from them: (a) they are the purest demonstration that liquidity and distribution can exist with zero utility; (b) the ones that survive bolt utility on afterward (BONK's integrations) — utility after the fact is the reverse of this book's method; (c) the launch mechanics (bonding curves) are covered in Ch. 5.
4. A one-line "Where the Analogy Breaks Down": a memecoin is closer to a collectible than a currency; Ch. 9's NFT lens often fits it better than Ch. 2's.

**Additions to existing sections**
- "Access" subsection: after the Helium example, add a paragraph naming **DePIN** (decentralized physical infrastructure networks) as the archetype — earn tokens by supplying a physical resource (coverage, storage, mapping); Helium and Hivemapper are the Ch. 2 lab's own examples.
- "Ownership" subsection: expand the RWA paragraph into a `:::{admonition} How a Real-World Asset Becomes a Token` box: an off-chain legal entity (SPV) holds the asset; the token is a claim on that entity; transfer restrictions (accredited-only) are enforced on-chain — cross-ref Ch. 3 *Token-2022: Default Frozen / Permanent Delegate* and Ch. 12 exemptions.

**Lab — add to "🔬 Hands-On Lab" as Part 0 (individual, 15 min) before Part 1:**

Part 0 — Run the test on a memecoin
1. Open `https://dexscreener.com`, select the **Solana** chain filter, sort by 24h volume.
2. Pick one token whose name or logo is clearly a meme. Open its page. Record: price, 24h volume, liquidity, market cap, and age of the pair.
3. Click through to its Solscan page (the link icon next to the mint address). Record holder count and the top-10 holder share.
4. Fill in the Actor Table for it: Buyers / Early holders / Deployer. Be honest about the Reason to Spend column.
5. Write three sentences: does it pass the "why would anyone want this" test, and what single addition would make it pass?

---

### Chapter 3 — Launch Your Token

**Small factual corrections (replace only the quoted text; nothing else in the chapter changes)**
- "The Squarespace Analogy": Orca (a DEX) has no token-creator product. Replace "**Solana Token Creator** by Orca" with "**Solana Compass's Token Creator** (solanacompass.com/tools/create-solana-token)". Smithii and SPL Token UI stay as written.
- "Cost Anatomy": align the ATA rent dollar figure with the book-wide SOL price ($100).

**New section — insert after "Three Powers…", before "Associated Token Accounts":**

`## Token-2022: Extensions for Business Tokens`

Cover:
1. There are two token programs on Solana. The original SPL Token program (what the lab uses) and **Token-2022** (Token Extensions), which adds optional, per-mint features. A Token-2022 mint is still an SPL-standard token: Phantom, Solscan, Jupiter, and Raydium's CPMM pools all support it; older programs such as Raydium's AMM v4 pools and some legacy tools do not, so check before pairing a Token-2022 mint with an older protocol.
2. The extensions that matter for a business token, one paragraph each, tied to where the book already needs them:
   - **Transfer fee** — a percentage of every transfer withheld to a treasury or burned. This is Ch. 4's consumption sink enforced by the protocol rather than by your app.
   - **Non-transferable** — a token that cannot leave the wallet it was minted to. This is the real way to build Ch. 2's reputation token and Ch. 9's soulbound credential.
   - **Permanent delegate** — an authority that can transfer or burn tokens from any account. The compliance clawback for regulated assets (Ch. 12). Also a red flag on a token that claims to be community-owned.
   - **Default account state (frozen)** — new token accounts start frozen until the issuer thaws them: KYC-gated tokens; the RWA pattern from Ch. 2.
   - **Confidential transfers** — amounts encrypted on-chain while remaining auditable by the issuer. The privacy answer to Ch. 10's "glass airplane."
   - **Interest-bearing** — a display-only rate that shows balances growing; no new tokens are minted.
   - **Metadata pointer / on-chain metadata** — name, symbol, and URI stored on the mint without Metaplex.
   - **Transfer hook** — a program that runs on every transfer; the mechanism behind enforceable NFT royalties in Ch. 9.
3. A decision table: rows = the four token types from Ch. 2 plus "regulated asset"; columns = which extensions to consider; a final column "what a buyer should think when they see it" (e.g., permanent delegate on a "community" token = walk away).
4. "Where the Analogy Breaks Down": extensions are set at mint creation and most cannot be added later — another permanence decision.

Add glossary entries for each extension and for Token-2022.

**Lab — add to "🛠️ Hands-On Lab" after Step 7:**

Step 8 — Read a Token-2022 token in the wild (10 min)
1. On Solscan, open the PYUSD (PayPal USD) mint: `2b1kV6DkPAnxd5ixfnxCpjxmKwqjjaYmCZfHsFu24GXo`. On the token page, note the **Owner Program** field shows **Token 2022 Program**, not the original SPL Token program.
2. Find the **Extensions** panel. PYUSD enables confidential transfers, transfer hook, permanent delegate, metadata + metadata pointer, mint close authority, and transfer fees. For each, write which business need from the table above it serves (for example: permanent delegate = regulatory clawback; confidential transfers = payroll privacy).
3. Compare to your own token's page: your token program, your extensions (none). Write two sentences on which single extension you would add to your token and why — or why none.

Step 3b (optional, devnet) — Mint a Token-2022 test token
1. Switch Phantom to devnet (Settings → Developer Settings → Testnet Mode). Get devnet SOL at `https://faucet.solana.com`.
2. Open Smithii's **Tax Token Creator** (tools.smithii.io → Solana → Tax Token Creator), which mints a Token-2022 token with the transfer-fee extension. Switch it to devnet, and create a throwaway token with a 1% transfer fee.
3. Send 100 tokens to your backup wallet. On Solscan (devnet), open the transfer and find the withheld fee. Record it.

---

### Chapter 4 — Tokenomics on a Napkin

**Pointers (one sentence each, appended to the existing paragraph):**
- End of "The Circular Yield" failure pattern: "Chapter 5's *Real Yield vs. Emissions Yield* gives the mechanism and a test you can run on any advertised APY."
- "Velocity" sink list, the "Collateral" bullet: append "(how lending markets do this: Chapter 5, *Beyond the Pool*)".

**New section — insert after "Velocity: The Hidden Killer", before "Reading a Tokenomics Table Like an Investor":**

`## The Other Side of the Napkin: Demand`

Cover:
1. Supply curves without demand curves produce no price. The minimum demand model: expected users per month × tokens each must hold (pull the tier thresholds from Ch. 7's table) × average holding period → tokens locked in sinks. Add tokens consumed (burned) per month.
2. Implied price band: (tokens demanded in sinks) vs. (circulating supply from the Step 3 projection). When sink demand exceeds circulating float, price pressure is upward; when unlocks exceed sink growth, downward.
3. The inflection: the month where monthly burns + newly locked tokens ≥ monthly unlocks + emissions. Show it with the chapter's existing worked example numbers.
4. One honest caveat: this is a napkin, not a valuation; it tells you whether the design is coherent, not what the price will be.

**Activity — extend "🛠 Activity: Model Three Futures":**
- Add **Step 5 — Add the demand column:** for the chosen scenario, estimate users at months 1, 6, 12 (three numbers), multiply by the Ch. 7 tier requirement, add monthly burns, and mark the inflection month (or note that there isn't one within 12 months and what you would change).
- Add a note that a starter spreadsheet is provided in the repo at `resources/ch04-tokenomics-model.xlsx` with tabs for Allocation, Vesting, Circulating, Demand. **Create this file** (columns as described; formulas, not values).

---

### Chapter 5 — Liquidity on Raydium

**Small factual corrections (replace only the quoted text; nothing else in the chapter changes)**
- Glossary "Raydium": remove "access to Serum's central limit order book" (Serum is defunct since late 2022). Replace with: "a major Solana DEX offering constant-product (Standard/CPMM) and concentrated-liquidity (CLMM) pools, integrated with the Jupiter aggregator."
- Scenario dollar prices: use the book-wide SOL assumption ($100).
- **Pool-creation cost (the chapter understates it).** Raydium charges a **0.15 SOL pool-creation fee** for a Standard AMM (CPMM) pool, separate from rent and transaction fees. Three places to correct: (a) "What You Need": change "At minimum $20 worth of SOL in your wallet" to "At minimum 0.15 SOL for Raydium's pool-creation fee, plus the SOL you will deposit into the pool, plus ~0.02 SOL for rent and transaction fees"; (b) Step 5 "Initialize the Pool": change "The total cost … should be under $1 in total transaction fees" to "Raydium charges a one-time 0.15 SOL pool-creation fee (shown in the confirmation), plus under $1 in rent and transaction fees, plus whatever SOL you deposit"; (c) Step 3: the pool type is labeled **Standard AMM (CPMM)** in Raydium's interface — note that this is the CPMM program, which is what the new *Pool Types* section and *Burn & Earn* step refer to. Also update the index card's "$20" framing in "What This Book Is" (Chapter 5 line) to "for the cost of a pool-creation fee and a few dollars of liquidity."

**New section A — insert after "The Constant Product Formula", before "Price Discovery":**

`## Pool Types: Constant Product vs. Concentrated Liquidity`

Cover: the x·y=k pool spreads capital across all prices from 0 to ∞, so most of it never trades; a **concentrated liquidity** pool (Raydium CLMM, Orca Whirlpools, Meteora DLMM) lets each LP choose a price range, so the same capital provides far more depth inside the range — and earns nothing, while suffering full impermanent loss, outside it. Rule of thumb for the reader: constant product for a new token with no price history (what the lab uses); concentrated pools once the price has a range and there are active LPs. Cross-ref Ch. 10 liquidity depth.

**New section B — insert into "Slippage, Pool Depth, and the Thin Liquidity Problem" as a final subsection:**

`### MEV and the Sandwich`

Cover: because pending transactions are visible, a bot can place a buy before yours and a sell after it, pocketing the price impact you created — a **sandwich attack**. This is why Jupiter has a slippage-tolerance setting: it is the maximum price impact you will accept, and a high tolerance is an invitation. Name that Solana's MEV largely routes through Jito bundles and that "MEV tips" are part of the staking yield discussed in Ch. 4. Practical rule: set slippage as low as the trade will clear; never "auto/unlimited" on a thin pool.

**New section C — insert after "Centralized Exchanges as Gatekeepers vs. Decentralized Rails", before "Activity: Open the Market":**

`## Launchpads and Bonding Curves`

Cover:
1. A **bonding curve** is a pool with only one side: the program sells tokens along a fixed price curve (price rises as more are bought) and holds the SOL it receives. No LP seeding is needed; the first buyer sets nothing — the curve does.
2. **Launchpads** automate this: anyone creates a token for a few cents, it trades on the curve, and when the curve fills to a threshold ("graduation") the accumulated SOL and tokens are migrated into an AMM pool. pump.fun is the reference case on Solana: until March 2025 graduated tokens migrated to a Raydium pool; since then they migrate to pump.fun's own DEX, **PumpSwap**. Raydium answered with its own launchpad, **LaunchLab**, whose graduated tokens land in a Raydium CPMM pool.
3. Why it matters for this course: it is the dominant new-token pathway on Solana; it makes the "fair launch" argument concrete (no presale, no team allocation, everyone buys on the curve); and it makes rug-pull mechanics visible — the deployer usually buys first at the bottom of the curve.
4. Connect to Ch. 2's memecoin section and Ch. 12's rug-pull mechanics.

**New section D — insert after "Reading Your Position Over Time":**

`## Managing Liquidity After Launch`

Cover in short paragraphs: adding liquidity as demand grows; removing liquidity (and why a buyer reads any removal as a warning); **protocol-owned liquidity** (the treasury holds the LP position — cross-ref Ch. 11); **locking or burning LP tokens** as the credible commitment that the pool cannot be drained (cross-ref Ch. 12 rug pull); when a professional market maker or CEX listing enters the picture (only after organic volume and holder count justify it; Ch. 10 metrics).

**New section E — THE DeFi SECTION. Insert after "Managing Liquidity After Launch", before "The Broader Picture: What You Just Built":**

`## Beyond the Pool: The DeFi Stack`

Open with two paragraphs: the pool you just built is one of five primitives that, composed together, are what "decentralized finance" means — a stable unit of account, a yield on the base asset, a way to borrow against what you hold, a source of truth for prices, and markets to trade all of it. Each is a program (Chapter 8) that anyone can call, and each can call the others — "money legos." This section walks the five in the order a business will meet them, then names the risks that come with composing them. Everything here is done by observation or with a few dollars in the lab that follows.

`### 1. Stablecoins: The Unit of Account`
1. Definition: a token designed to hold a fixed value against a reference asset, almost always the U.S. dollar. USDC is issued natively on Solana and is the quote asset for most pools, the treasury asset in Chapter 4, and the "convert immediately" target in Chapter 7.
2. Three backing models, one example each: **fiat-reserve** (USDC — the issuer holds cash and short-term Treasuries and publishes attestations), **crypto-collateralized** (DAI — over-collateralized by other crypto, parameters set by MakerDAO governance; cross-ref Ch. 11), **algorithmic** (Terra/UST, May 2022 — no reserve; collapsed in days; the cautionary case).
3. The custody twist: USDC's mint keeps a **freeze authority** held by the issuer, which can freeze any USDC account (it has, under sanctions orders). "Not your keys, not your coins" has a corollary: "not your issuer, not your dollars." Cross-ref Ch. 1 custody and Ch. 3 freeze authority.
4. **Depeg**: USDC traded near $0.88 for a weekend in March 2023 when part of its reserves sat in a failed bank. A stablecoin is exactly as stable as its reserves and its redemption path.
5. Regulation in one paragraph: the GENIUS Act, signed into U.S. law in July 2025, is the first federal stablecoin framework — it limits issuance to licensed "permitted payment stablecoin issuers," requires 1:1 reserves in cash and short-term Treasuries, monthly reserve disclosures, and redemption at par. Implementing regulations were issued by the OCC and Treasury through 2026, with the framework taking full effect in early 2027. Cross-ref Ch. 12 regulatory snapshot.

`### 2. Staking and Liquid Staking: Yield on the Base Asset`
1. **Native staking**: delegate SOL to a validator; the validator votes on blocks; inflation rewards (Chapter 4's 8% → 1.5% schedule) flow to stakers minus the validator's commission. Unstaking takes an epoch (~2–3 days). Delegation is not custody — the SOL never leaves your control.
2. **Liquid staking**: deposit SOL, receive a liquid staking token (mSOL from Marinade, JitoSOL from Jito) that rises against SOL as rewards accrue and can be traded, pooled, or posted as collateral while still earning. What it adds: smart-contract risk and a second market that can trade at a discount to the SOL it represents.
3. One sentence on restaking, flagged beyond scope.

`### 3. Lending Markets: Borrowing Against What You Hold`
1. A **lending market** is the second kind of pool: depositors supply an asset and earn interest; borrowers post collateral and borrow a different asset; the interest rate is set by a **utilization curve** (the more of the pool is borrowed, the higher the rate). On Solana: Kamino, Marginfi (name two; do not rank).
2. **Over-collateralization**: post $100 of SOL, borrow up to ~$70 of USDC at a 70% loan-to-value. **Health factor** = collateral value × liquidation threshold ÷ debt. Below 1.0 anyone may **liquidate** you: repay your debt and take your collateral at a discount.
3. Why this matters to your token: "collateral" is the deepest utility sink in Chapter 4's list — tokens posted as collateral are locked. And why it is dangerous for a new token: a thin pool (earlier in this chapter) means one sale drops the price, which drops every borrower's health factor, which triggers liquidations, which sell more — the **cascade**. Lending markets therefore list only tokens with deep liquidity and a reliable price feed, which leads to:
4. "Where the Analogy Breaks Down": a bank calls you before foreclosing; a lending program liquidates in the block the health factor crosses 1.0.

`### 4. Oracles: Where the Price Comes From`
1. A lending market cannot read prices from one pool — a pool can be pushed. It reads a **price oracle**: an on-chain feed aggregated from many venues. On Solana: **Pyth** (a network of publishers; each feed carries a price and a confidence interval) and **Switchboard**.
2. Everything downstream depends on it: every liquidation, every dollar-denominated token price (Chapter 7's Pricing Problem), every RWA token (Chapter 2). Oracle manipulation and stale feeds sit behind a large share of DeFi exploits — see *DeFi Risk* below.

`### 5. Real Yield vs. Emissions Yield`
The test that ties this section to Chapter 4's "Circular Yield" failure pattern: *what asset is the yield paid in, and where did that asset come from?* SOL staking yield is mostly inflation (dilution redistributed to stakers) plus a smaller share of real fees and MEV tips (see *MEV and the Sandwich* earlier in this chapter). LP fees from your pool are real yield — paid by traders. A protocol's "40% APY paid in its own token" is emissions unless a fee stream backs it. Give a three-line worked example using the chapter's LEARN pool: fees earned ÷ capital deposited, annualized, vs. an emissions program that mints LEARN to LPs.

`### 6. DeFi Risk`
Five named risks, one paragraph each: **smart-contract risk** (the program has a bug; cross-ref Ch. 8 auditor checklist); **oracle manipulation** (push a thin pool's price so a lending market mis-values collateral); **liquidation cascades** (above); **bridge risk** (assets wrapped from another chain depend on the bridge's security — the industry's largest losses; cross-ref Ch. 0 box); **composability risk** (a protocol you integrated is exploited and your token is the collateral being dumped). Defenses for the reader: integrate only audited protocols; prefer oracle-based pricing over pool-based; watch whether your token is listed as collateral anywhere (Ch. 10); never post more than you can lose to liquidation.

`### 7. The DeFi Map`
One paragraph: **total value locked (TVL)** as the industry's headline metric and DeFiLlama as the place to read it by chain and by protocol; how to recognize which category each top protocol belongs to (DEX, lending, liquid staking, perps); and the caveat that TVL counts the same dollar more than once when assets are re-deposited across legos.

Add glossary entries (to the Ch. 5 glossary): Stablecoin, Fiat-Reserve / Crypto-Collateralized / Algorithmic Stablecoin, Depeg, Staking, Delegation, Validator Commission, Epoch, Liquid Staking Token (LST), Lending Market, Utilization Rate, Loan-to-Value (LTV), Health Factor, Liquidation, Liquidation Cascade, Price Oracle, Pyth, Real Yield, Emissions Yield, Total Value Locked (TVL), Composability Risk, Money Legos.

**New lab — insert after the extended "Activity: Open the Market" (i.e., after Step 8) as a separate section `🔬 Hands-On Lab: DeFi in an Afternoon (90 min, mainnet, ≈ $10 at risk)`.**

Preface: "This lab is designed for a second class session. Every step uses small amounts; every step ends with something recorded."

Part A — Hold a dollar (10 min)
1. In Phantom, click **Swap**. From: SOL. To: USDC. Amount: 0.02 SOL. Record the quoted rate, the route Phantom shows (which pools it used), and the fee. Confirm.
2. On Solscan, search the USDC mint `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v`. Record **Mint Authority** and **Freeze Authority**. Note the freeze authority is not "None."
3. Open the **Holders** tab. Record holder count and the largest holder.
4. Write two sentences: what can the issuer do to your USDC that no one can do to your SOL, and why might a business hold USDC anyway?

Part B — Stake it (15 min)
1. Native staking, by observation (Phantom requires a minimum of 1 SOL to stake natively, so most students will not execute this): in Phantom's token list open **Solana** → **More** → **Stake SOL** → **Native Staking**. Phantom shows a validator list with each validator's commission and estimated APY. Record the commission and APY of the top suggestion, then look the same validator up on `https://solanacompass.com` (or `https://validators.app`) and record its uptime/skip rate. Close without staking. (A student with ≥1 SOL to spare may stake it: click **Stake**, then record the stake account address; unstaking is under **Native Stakes → Other → Unstake** and takes until the next epoch.)
2. Liquid staking, executed: open `https://marinade.finance`, click **Stake**, connect Phantom, and stake 0.05 SOL. Record the SOL→mSOL exchange rate you received (mSOL received ÷ SOL deposited), the displayed APY, and the transaction signature. Confirm mSOL appears in Phantom.
3. Open `https://www.jito.network`. Record JitoSOL's displayed APY and the line showing MEV rewards. Do not transact.
4. Find Solana's current inflation rate (Solscan's or the explorer's supply page shows it). Write three sentences: how much of each of the three yields is emissions vs. real fees/MEV, and which one is Chapter 4's "circular yield"?

Part C — Borrow against it (25 min)
1. Open `https://app.kamino.finance` and connect Phantom. Open **Borrow/Lend** and select the **Main Market**. Each asset row shows its supply APY, borrow APY, and maximum loan-to-value. (Marginfi at `https://app.marginfi.com` is an equivalent alternative with a **Lend** page and the same fields.)
2. Click **SOL** → **Supply** and deposit 0.05 SOL (or the mSOL from Part B — a staked asset can also be collateral). Record the supply APY.
3. Click **USDC** → **Borrow** and borrow 1 USDC (the app enforces a minimum; take the smallest it allows). Your position panel now shows **Net Value**, **LTV**, **Liquidation LTV**, and a **Health** gauge. Record all four.
4. Record the SOL price at which the app says your position would be liquidated. Check it: liquidation occurs when debt ÷ collateral value reaches the Liquidation LTV.
5. Repay the USDC and withdraw the collateral. Record total interest paid.
6. Search the market list for your Chapter 3 token. It is not there. Write two sentences: which two things from this chapter and Chapter 10 would a lending market require before listing it?

Part D — Find the oracle (10 min)
1. Open `https://pyth.network/price-feeds/crypto-sol-usd`. Record the price, the confidence interval, and the number of publishers.
2. Compare to the SOL price shown in your own Raydium pool from earlier in this chapter (SOL per LEARN inverted). Write one sentence: why must the lending market in Part C read Pyth rather than a pool?

Part E — Read the map (10 min)
1. Open `https://defillama.com/chain/Solana`. Record total TVL and the top five protocols. Label each as DEX, lending, liquid staking, or other.
2. Find the protocol you used in Part C and the one you used in Part B. Record their TVL.
3. Write three sentences: which lego did your money touch in which order today, where would a bug in any one of them have left you, and which single risk from *DeFi Risk* worried you most while doing it?

Deliverable — the DeFi Lab Sheet: a one-page table with every recorded value from Parts A–E, the five short written answers, and the transaction signatures for the swap, the stake, the deposit, the borrow, and the repayment.

**Discussion (add as a second prompt to the chapter's Discussion section, do not replace the existing one):**
"Your pool, your stake, your loan and its oracle all ran without a bank, a broker, or a clearinghouse. Which of those institutions did DeFi actually replace today, which did it merely hide (the validator, the oracle publishers, the issuer of USDC), and who do you call when the program is wrong?" Same guidelines as the existing prompt.

**Lab — extend "Activity: Open the Market":**

Step 7 — Lock it (10 min)
1. The "Standard AMM" pool you created is a Raydium **CPMM** pool, and Raydium's **Burn & Earn** can lock it permanently while you keep the right to collect its trading fees. On Raydium go to **Liquidity** → **Create** → **Burn & Earn**, select your position, read the confirmation (it shows the position address, size, and pool), type the confirmation sentence the screen asks for, and click **Confirm**. The lock is irreversible; a **Fee Key** NFT arrives in your wallet — whoever holds it can claim the locked position's fees. If you want to keep your capital for later chapters, do not lock; instead read the Burn & Earn screen up to the confirmation, close it, and complete step 2 by observation.
2. Open `https://rugcheck.xyz`, paste your mint address. Record the risk score and each line item: mint authority, freeze authority, LP locked %, top holders. Take a screenshot before and (if you locked) after.
3. Write two sentences: what a buyer sees on RugCheck for your token today, and what one change would most improve it.

Step 8 — Watch a bonding curve (10 min, observation only, no purchase)
1. Open `https://pump.fun`. Pick any token on the board. Note the **bonding curve progress** percentage and the market cap.
2. Find the same token on DexScreener by pasting its address. If it has migrated, note the pool it migrated to and the moment of migration in the chart.
3. Open its Solscan holders tab. Record the deployer's share (usually the top non-pool wallet).
4. Write two sentences: what happens to the price the moment the curve migrates, and what would you check before buying anything on a curve?

Add to the lab notebook table: "LP locked/burned (Y/N, %)", "RugCheck score", "Slippage tolerance used on the Jupiter swap".

---

### Chapter 6 — Distribute It

**Small factual corrections (replace only the quoted text; nothing else in the chapter changes)**
- Resolve the network thread. Recommended: keep the lab on **devnet** and add, at the top of "Hands-On Lab": "This lab runs on devnet because you will be sending tokens to many wallets and testing cancellation. Your Chapter 3 token exists only on mainnet. Mint a throwaway devnet token first (Chapter 3, Step 3b, or any creator switched to devnet) and use it for every step below."
- Align the ATA rent dollar figure ("~$0.50") with Ch. 3 and the book-wide SOL price ($100).

**New box — insert after "Computing Your Distribution Cost":**

`:::{admonition} The Tax Line Nobody Budgets` (`:class: warning`)

Cover, U.S. framing with a "your jurisdiction differs" caveat: an airdrop received is ordinary income at fair market value on the date of receipt (IRS guidance since 2019; cross-ref the FMV glossary entry); streaming payments and vesting releases to contributors are compensation and are taxable when received; adding or removing liquidity and swapping tokens are generally taxable events; brokers now report digital-asset transactions on Form 1099-DA. The issuer's obligation: if you are paying contractors in tokens, you have the same reporting duties as if you paid in dollars. Cross-ref Ch. 12 launch checklist.

Add glossary entries: Taxable Event, Form 1099-DA.

**Lab — add to Part 1 (Streamflow):**
- Step 7: After the cliff, have the recipient withdraw once. Then, as the sender, **cancel** the stream. Record what returned to you and what stayed with the recipient. This is the clawback right from the Streaming Payments section, demonstrated.

**Lab — add Part 4 — Sybil-test your own airdrop (10 min):**
1. Create a third Phantom account. Attempt to claim/receive the same airdrop with it (re-run the CSV with the new address added).
2. It works — nothing stopped you. Write three sentences: which of the four Sybil defenses from the chapter would have stopped this, what it would have cost you to implement, and what it would cost a legitimate classmate in friction.

---

### Chapter 7 — Utility Without Code

**Small factual corrections (replace only the quoted text; nothing else in the chapter changes)**

Three of the four gating platforms the chapter names no longer work for a Solana community, and the chapter's lab is built on one of them. Verified August 2026: **Holder.xyz has been sunset** (its site announces the product is discontinued); **Grape Protocol's domain (grapes.finance) is for sale**; **Guild.xyz supports 60+ EVM chains and not Solana**. Matrica is live. The two live, Solana-capable Discord/Telegram gating platforms are **Collab.Land** (Discord and Telegram; Solana SPL tokens and NFT collections; free tier for small servers) and **Matrica** (Discord and Telegram; paid plans from ~$35/month).

- "How Token-Gating Platforms Work": replace the four platform paragraphs (Holder.xyz, Grape Protocol, Guild.xyz, Matrica) with two: **Collab.Land** — the most widely installed gating bot; supports Discord and Telegram; a "Token Gating Rule" (TGR) checks an SPL token balance or an NFT collection on Solana; several TGRs can map to one role; members verify by connecting Phantom through the bot's link. **Matrica** — Solana-native; Discord and Telegram; rules on SPL balances, NFT collections, and NFT traits; paid. Keep the six-step "Each platform follows the same pattern" list unchanged — it is still accurate.
- The `fig-ch07-gating-platforms` figure caption and alt text: replace the four names with "Collab.Land and Matrica."
- "🔬 Hands-On Lab: Build One Real Door" → "Choosing Your Platform": replace "**Discord with Holder.xyz**" with "**Discord with Collab.Land** — free for small servers, Solana supported, the most widely used gating bot." Keep the Telegram/Matrica option as written (delete "or Collabland" from that line, since Collab.Land is now the Discord path).
- "Step-by-Step: Discord Token Gating with Holder.xyz" → retitle "…with Collab.Land" and replace **Phase 2** with:
  1. Go to `https://collab.land` → **Add to Discord**, choose your server, and authorize the bot (it needs Manage Roles and Read Members). The bot posts a **Let's Go** verification button in a `#collabland-join` channel it creates.
  2. Open the Collab.Land **Command Center** (`https://cc.collab.land`), sign in with Discord, select your server.
  3. Click **TGRs** → **Add TGR**. Set: **Chain:** Solana · **Token type:** SPL fungible token · **Token address:** your Chapter 3 mint address · **Min balance:** 10 (for testing) · **Role:** Token Holder. Save.
  4. In Discord, drag the **Collab.Land** bot role above the **Token Holder** role in Server Settings → Roles, or the bot cannot assign it.
  Replace **Phase 3** step 2 with: "Have them click **Let's Go** in `#collabland-join`, choose **Phantom**, and sign the verification message. The Token Holder role is assigned within a minute." Phase 1, Phase 4, and the Telegram/Matrica alternative stay as written.
- "🔗 Key Tools Referenced" table: delete the Holder.xyz, Grape Protocol, and Guild.xyz rows; add "**Collab.Land** | Discord and Telegram token-gating for Solana | collab.land"; keep Matrica, Phantom, Solana Explorer. Delete the "Collabland" row if it duplicates.
- Glossary: replace the **Holder.xyz** and **Grape Protocol** entries with **Collab.Land** ("The most widely used token-gating bot for Discord and Telegram; on Solana it verifies SPL token balances and NFT holdings and assigns roles automatically") and keep the rest.

**Pointer — in "The Pricing Problem", append to the bullet "Dollar-denominated price, token payment":** "…using a price oracle such as Pyth (Chapter 5, *Oracles*)."
No other DeFi content in this chapter.

**New subsection A — append to "Payments in Your Own Token":**

`### The Rail: Solana Pay`

Cover: Solana Pay is an open payment specification — a URL/QR format (`solana:<recipient>?amount=…&spl-token=<mint>&label=…`) that any Solana wallet can scan to pay in SOL, USDC, or *your* SPL token, settling on-chain in under a second with no card network. This is the point-of-sale integration that Ch. 2 (Starbucks on-chain) and Ch. 8 (loyalty check-in) assume. Shopify has offered Solana Pay as a checkout option since 2023 (shopifydocs.solanapay.com), settling in USDC; other commerce plugins exist. Connect to Ch. 5's stablecoin subsection: most merchants request USDC and let customers pay from any token via a swap in the wallet.

**Addition B — in "On-Chain Utility vs. Traditional Loyalty Mechanics", after the paragraph beginning "The honest limitation…":** add two sentences: embedded wallets and passkey sign-in (Ch. 1) are closing the connect-wallet gap; the 2026 pattern is that the customer never sees a seed phrase and the token lives in a wallet created by the app.

Add glossary entry: Solana Pay.

**Lab — add `Part 2 — Get Paid` after the existing Discord/Telegram lab (which becomes Part 1; apart from the Collab.Land replacement above, do not edit its steps):**

Part 2 — Get paid in your token (15 min)
1. Construct a Solana Pay request for your token: `solana:<your primary wallet address>?amount=5&spl-token=<your mint address>&label=<YourToken>%20Coffee&message=Thanks`.
2. Turn it into a QR code with any QR generator, or paste the URL into a classmate's phone.
3. The classmate opens Phantom mobile → scan → approves. Confirm the 5 tokens arrived (Solscan).
4. Repeat with `spl-token=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v` (USDC) and `amount=0.01`. Write two sentences: which of the three pricing approaches in this chapter did each request implement, and which would a real shop use?

---

### Chapter 8 — Your First Program

**Small factual corrections (replace only the quoted text; nothing else in the chapter changes)**
- Glossary "BPF": add "Solana's runtime has since moved to SBF (Solana Bytecode Format), a fork of eBPF; the concept is unchanged."

**Addition A — show the code.** In "Step 2: Load the Counter Template", after the file list, insert the full `lib.rs` of the Counter template as a `rust` code block with inline comments written for a business reader. Use the template's actual code from Solana Playground; annotate at minimum: the `declare_id!` line (this is the Program ID), the `#[program]` module (this is the instruction list — the checklist in *Reading, Not Writing, Code* step 3), each `pub fn` (one instruction each), the `#[derive(Accounts)]` structs (the account list every instruction must declare), `Signer<'info>` (who must sign), `#[account(init, payer = …, space = …)]` (a data account is created and someone pays rent — Ch. 3), and the `#[account] pub struct Counter { pub count: u64 }` (the state, living in an account, not in the program — the chapter's central idea). Keep the annotations in comments so the block compiles unchanged.

**New section B — insert after "Instructions, Accounts, and Signers…", before "Code Is Law":**

`## How a Program Holds Your Token: PDAs and CPI`

Cover:
1. **Program Derived Address (PDA)**: an address computed from the program ID plus chosen seeds, for which *no private key exists*. Only the program can sign for it. This is how a vesting contract (Ch. 6), a liquidity pool (Ch. 5), a multisig vault (Ch. 11), or an escrow "holds" tokens: the tokens sit in a token account owned by a PDA, and the program's rules are the only way they move. Analogy: a safe with no key, only a rulebook bolted to the door.
2. **Cross-Program Invocation (CPI)**: a program calling another program. Your check-in program does not reinvent token transfers; it calls the SPL Token program's `transfer` or `mint_to` instruction, signing as its PDA. Every DeFi "money lego" is CPI: Jupiter calls Raydium; Kamino calls the Token program; Realms executes a proposal by CPI.
3. What this means for the reader's evaluation checklist: add step 6 — *which programs does this program call, and does it hold assets in PDAs or in a human's wallet?*

**Addition C — in "Reading, Not Writing, Code", under step 5 (audit reports), insert:**

`:::{admonition} What Auditors Actually Look For` (`:class: important`) — six named vulnerability classes, one line each: **missing signer check** (an instruction that should require an owner's signature doesn't); **missing owner check** (the program trusts an account without verifying which program owns it); **account type confusion** (passing one kind of account where another was expected); **arithmetic overflow/underflow** (a balance wraps around); **arbitrary CPI** (the program calls whatever program address the caller supplies); **closed-account revival** (an account closed for rent refund is reopened with stale data). Note that Anchor's `#[account(...)]` constraints exist to prevent most of these, which is why "built with Anchor" is a (weak) positive signal. Name that public checklists of these patterns exist from Solana auditing firms (Neodyme's "Sealevel attacks" is the standard reference).

**Lab — replace "Stretch Activity: Add a Decrement Instruction" with:**

Stretch Activity — Make the program touch a token (30 min, devnet)
1. Solana Playground bundles the `solana` and `spl-token` command-line tools in its terminal (bottom panel) and the `anchor-spl` crate in its build system. Create a throwaway devnet token there: `spl-token create-token`, then `spl-token create-account <MINT>`, then `spl-token mint <MINT> 100`. Record the mint address.
2. Gate the check-in: add to the `Increment` accounts struct a `token_account: Account<'info, TokenAccount>` with an Anchor constraint requiring `token_account.owner == user.key()` and `token_account.amount >= 1`, and import `anchor_spl::token::TokenAccount`. Rebuild and redeploy.
3. In the Test panel, run `increment` passing your token account. It succeeds. Run it passing an empty token account (create one with `spl-token create-account` for a second mint, or an account with 0 balance). It fails with a constraint error. Screenshot both transactions on Solana Explorer.
4. Write three sentences: which vulnerability class from the auditor box would you have introduced by omitting the `owner` constraint, and what could an attacker have done?

Keep the original "students who do not wish to modify code" escape hatch.

---

### Chapter 9 — NFTs and Memberships

**Small factual corrections (replace only the quoted text; nothing else in the chapter changes)**
- "Credentials and Certificates": delete "Metaplex supports this with a `isMutable: false` flag and the ProgrammableNFT standard." Replace with: "Non-transferability is enforced either by a Programmable NFT rule set that blocks transfers or, for fungible or semi-fungible credentials, by the Token-2022 Non-Transferable extension (Chapter 3). The metadata `isMutable` flag controls whether the description and image can change — it has nothing to do with transfer."
- "Fungible vs. Non-Fungible": scope the definition — "Under the Metaplex Token Metadata standard used in this lab, an NFT is an SPL token with supply of one plus a metadata account."
- "Royalties": move the sentence "For this course, we will use Metaplex Core (the 2025 standard)…" into a new `:::{admonition} Two Metaplex Standards` box explaining that **Token Metadata** wraps an SPL mint (one mint + one metadata account per NFT), while **Metaplex Core** is a newer single-account asset standard with built-in plugins for royalties, freezing, and transfer delegates and lower minting cost. Metaplex's own Candy Machine tooling is now developer tooling (a CLI and SDK — "Core Candy Machine"), so the lab uses a no-code launchpad and describes both standards.
- **The lab's minting tool is dead.** `studio.metaplex.com` returns a 404 (verified August 2026); Metaplex no longer offers a no-code Candy Machine UI. Replace it throughout Part 3 with **LaunchMyNFT** (`https://www.launchmynft.io`), a live no-code Solana NFT launchpad whose collections are recognized by Magic Eden and Tensor. Rewrite Part 3 as:
  1. Go to `https://www.launchmynft.io` → **Create** → connect Phantom (mainnet).
  2. Choose **Upload your own assets**. Upload `gold.png` (and, if you like, `silver.png` and `bronze.png` as separate items) with a name for each ("Gold Member Pass #1").
  3. Fill in the collection settings: **Collection name**, **Symbol** (`GPASS`), **Description**, **Royalty** 5%, **Supply** 5, **Mint price** 0 SOL, mint start **now**.
  4. Review the fee summary LaunchMyNFT shows (a small per-collection deployment fee in SOL plus network rent), then **Deploy** and approve the transactions in Phantom.
  5. On your collection's mint page, mint 2–3 passes to your own wallet. Confirm they appear in Phantom under **Collectibles**.
  6. Copy the **collection address** from the collection page (or from one pass's Solscan page under "Collection"). You need it for Part 4.
  Update the `fig-ch09-candy-machine` figure caption to describe "the launchpad's minting program" rather than Candy Machine Studio, and delete the `:::{note}` that begins "Candy Machine is Metaplex's minting infrastructure" or reword it to describe Candy Machine as the developer-facing tool the launchpad wraps.
- Prerequisites and Lab Part 4: replace every "Underdog Protocol" / `app.underdogprotocol.com` reference with **Collab.Land** (the Chapter 7 Discord tool after that chapter's correction). Rewrite Part 4 as: in the Collab.Land Command Center → **TGRs** → **Add TGR**, create a second rule: **Chain** Solana · **Token type** NFT collection · **Collection address** (from Part 3) · **Min balance** 1 · **Role** Gold Member. You now have two independent, automatically maintained roles: **Token Holder** (2,000 tokens, from Chapter 7) and **Gold Member** (holds a Gold pass). Create a `#gold-lounge` channel visible only to Gold Member. Then observe the two-factor check directly: a wallet holding the pass but not the tokens gets `#gold-lounge` but not `#holders-only`; a wallet holding tokens but no pass gets the reverse; only a wallet with both sees both. Add one sentence to the chapter text: Discord roles combine as OR, so a true AND gate (pass *and* balance for a single door) is enforced in your own app or backend that reads both — which is exactly what the chapter's "the benefit is delivered by your backend" paragraph on royalties already says. Keep the existing "To test a failing case" paragraph.
- Glossary: replace the **Candy Machine UI (Studio)** entry with **LaunchMyNFT** ("A no-code Solana NFT launchpad: upload assets, set supply, price and royalty, deploy, and mint from a hosted page; collections are recognized by Magic Eden and Tensor").

**New box — insert in "Storage: IPFS vs. Arweave" after the Arweave paragraph:**

`:::{admonition} Compressed NFTs` — for 10,000 tickets or receipts, per-NFT rent is prohibitive; **compressed NFTs** (Metaplex Bubblegum) store the collection in a Merkle tree so minting costs a fraction of a cent each, at the cost of needing an indexer (RPC provider) to read them. This is the right tool for the "receipt at point of sale" and "ticket" use cases in this chapter.

**Lab — add Part 7 — Read a compressed collection (5 min):** on Solscan, open any large Solana NFT collection minted as cNFTs (search "compressed" in the NFT section or use a collection the instructor supplies) and note the mint cost of one asset vs. the ~0.01 SOL of your LaunchMyNFT mint. Record both.

---

### Chapter 10 — On-Chain Analytics

**Additions**
- "The Analytics Stack": add a fourth tool subsection **Dune — the query layer**: Dune indexes Solana and lets anyone write SQL over transactions or fork public dashboards; for this course, read rather than write. This makes the index card true.
- "Liquidity Depth": add one sentence: "For the chain-wide version of this number see DeFiLlama (Chapter 5, *The DeFi Map*)."
- "Privacy in a Transparent World" box: add one sentence naming Token-2022 confidential transfers (Ch. 3) as the practical, non-ZK-research answer available today.

**New section — insert before "📊 Hands-On Lab", after "Comparative Analysis":**

`## Read a Token in 60 Seconds: The Buyer's Check`

Consolidate, as a numbered checklist with where to look: (1) mint authority and freeze authority revoked? — Solscan token page (Ch. 3); (2) LP locked or burned, and how much? — RugCheck / DexScreener (Ch. 5); (3) top-10 concentration, excluding pool addresses — Solscan holders (this chapter); (4) deployer wallet history — click the creator address on Solscan; has it deployed other tokens, and what happened to them?; (5) Token-2022 extensions that concentrate power (permanent delegate, freeze) — Solscan extensions panel (Ch. 3); (6) is the volume organic? — this chapter's wash-trade test; (7) is there a published team, allocation, and audit? — Ch. 12. Close with: the whole check takes one minute and would have caught most rug pulls in the last three years.

**Lab — extend "📊 Hands-On Lab":**
- Step 1a (5 min): open `https://dune.com`, search "Solana" dashboards, open any public dashboard showing daily active wallets or DEX volume, and record one number and its date. Note that you did not need an account or code.
- Step 1b (5 min): open `https://defillama.com/chain/Solana`. Record total TVL and the top three protocols by TVL, and label each as DEX, lending, or liquid staking (all defined in Chapter 5, *Beyond the Pool*). Compare to the numbers you recorded in Chapter 5's Part E.
- Step 2a (10 min): run the 60-second Buyer's Check on your own token and on your benchmark token; put both in a two-column table. Optional: open `https://app.bubblemaps.io`, load your benchmark token, and screenshot the holder cluster map — connected bubbles are wallets funded from the same source (the Sybil and wash-trade fingerprint).
- Add the Buyer's Check table to the dashboard deliverable.

---

### Chapter 11 — Governance and Treasury

**Small factual corrections (replace only the quoted text; nothing else in the chapter changes)**
- Quadratic voting is defined inconsistently. Body ("your second costs two tokens, your third costs three") and glossary ("second costs 4, third costs 9") are both wrong as stated. Replace both with: "*n* votes cost *n²* tokens in total, so each additional vote costs more than the last (the *n*th vote costs 2*n*−1): 1, 3, 5… Ten votes cost 100 tokens; a hundred votes cost 10,000."
- "Uniswap: Governance as Brand": replace "Uniswap's UNI token launched with $6.43 per UNI and an initial market cap of hundreds of millions of dollars" with "Uniswap's UNI token began trading near $3 on September 17, 2020 and roughly doubled within a day, giving it a market cap in the billions."

**New section A — insert after "Multisignature Wallets…", before "Governance Attacks":**

`## Managing the Treasury, Not Just Guarding It`

Cover: what the vault should hold (the Ch. 4 guidance of 50–70% in stablecoins or blue-chip assets, restated as policy); **runway** = stable assets ÷ monthly burn, and the rule that runway is counted in stablecoins only; a written **spending policy** (who can propose, size thresholds that need a vote vs. the multisig alone, cross-ref the proposal threshold in Realms); **diversification** via scheduled, announced conversions; and the founder's dilemma of **selling your own token** for operations — never market-sell into your own thin pool (Ch. 5); use OTC sales to aligned buyers, time-weighted execution, or announced schedules so the market prices it in (Ch. 10 exchange-inflow signal). Add: protocol-owned liquidity as a treasury asset (Ch. 5).

**New section B — insert after "The Decentralization Spectrum", before "Activity: Form the DAO":**

`## The Legal Wrapper: A DAO Is Not Yet a Legal Person`

Cover: an unincorporated DAO is, in several U.S. rulings, treated as a general partnership — every token-voting member potentially liable for the whole (the CFTC's action against Ooki DAO is the reference case); the available wrappers and what each buys — Wyoming DAO LLC (limited liability, on-chain governance recognized in the operating agreement), Marshall Islands DAO LLC, Cayman Islands foundation company (no members; common for protocol foundations), Swiss association; the wrapper holds the treasury bank account, signs contracts, and pays taxes, while on-chain governance directs it. Cross-ref Ch. 12 for entity choice and the Howey "efforts of others" prong.

Add glossary entries: Legal Wrapper, DAO LLC, Foundation Company, General Partnership Liability.

**Lab — extend "Activity: Form the DAO":**
- Part 1, Step 7: In Squads, open **Settings → Members** and walk through (without executing) adding a fourth signer and raising the threshold to 3-of-4. Screenshot the proposal screen. This is the succession step from Ch. 12.
- Part 2, Step 6: In Realms → your DAO → **Params/Config**, screenshot the governance parameters and identify the proposal threshold, vote duration, and any execution delay (time lock). If a time lock is configurable, set one of 1 hour and note what changes in Part 3.
- New Part 4 — Treasury policy (15 min): write a half-page treasury policy for your token: target stablecoin %, monthly burn estimate, runway in months, spending thresholds (multisig alone / Realms vote), and how you would convert 10% of the treasury's token holdings to USDC without moving the price (name the method). Submit with the executed-proposal screenshot.

---

### Chapter 12 — Legal, Risk, and Running It for Real

**New subsection A — insert inside "The Securities Question", after "How Token Design Shifts the Answer":**

`### If It Is a Security: The Exemption Map`

Cover: concluding that a token is a security is a compliance path, not a dead end. The standard exemptions from registration, one paragraph each with what they permit and cost: **Regulation D 506(c)** (accredited investors only, general solicitation allowed, resale restricted — the most common token-sale route); **Regulation S** (offshore buyers only); **Regulation Crowdfunding** (small raises from the public via a registered portal, with caps); **Regulation A+** (larger public raises with SEC qualification). Name that on-chain transfer restrictions for these (holding periods, accredited-only) map directly to Token-2022 default-frozen and permanent-delegate extensions (Ch. 3) — this is how compliant RWA tokens work (Ch. 2).

**New section B — insert after "The Securities Question", before "Disclosure and Transparency":**

`## Money Transmission, AML, and FinCEN`

Cover: securities law is one regulator; FinCEN (Treasury's financial-crimes unit) is another. Under U.S. rules, an entity that accepts and transmits value on behalf of others is a **money services business** and must register with FinCEN, run an AML program, and perform KYC; most states additionally require a money-transmitter license. FinCEN's guidance distinguishes users (you, spending your own token) from **exchangers and administrators**; an issuer that redeems tokens for fiat, runs a custodial wallet, or operates a swap desk for customers can cross into MSB territory. Practical rules for the reader: self-custody and peer-to-peer transfers are not transmission; running a hosted wallet or an on/off-ramp is; sanctions screening (OFAC) applies to everyone — which is why USDC has a freeze authority (Ch. 1).

Add glossary entries: FinCEN, Money Services Business (MSB), AML, KYC (move from Ch. 1 or cross-ref), OFAC.

**New box C — insert at the end of "The Launch Checklist as a Living Document":**

`:::{admonition} Regulatory Snapshot — as of August 2026` (`:class: note`) — a dated box so the chapter's securities section, written against the 2022–2024 enforcement era, reads correctly today. Contents, as bullets:
- **SEC posture.** In 2025 the SEC moved from enforcement-first to guidance and rulemaking: it formed a Crypto Task Force, dropped or paused most pending cases against exchanges, and its Division of Corporation Finance issued staff statements that most **memecoins** (February 2025) and most **protocol staking** arrangements — solo, delegated, and custodial staking on proof-of-stake networks (May 2025) — are not securities offerings. Staff statements are not rules and do not bind the courts; the Howey analysis in this chapter is still the law.
- **Stablecoins.** The **GENIUS Act** (signed July 18, 2025) is the first federal stablecoin statute: only licensed "permitted payment stablecoin issuers" may issue; reserves must be 1:1 in cash and short-term Treasuries with monthly public disclosure; holders redeem at par. Implementing rules were proposed by the OCC and Treasury in early 2026; the regime takes full effect by early 2027.
- **Market structure.** The **Digital Asset Market Clarity Act** (H.R. 3633), which would divide oversight of digital assets between the SEC and the CFTC and define when a token is a "digital commodity," passed the House in July 2025 and cleared the Senate Banking Committee in May 2026; as of August 2026 it awaits a Senate floor vote scheduled for September 2026. Until it is enacted, the Howey test and FinCEN rules above are the operative framework.
- **European Union.** **MiCA** has been fully in force since December 30, 2024; any project offering tokens or services to EU residents needs a licensed crypto-asset service provider and, for stablecoins, an authorized issuer.

Add a closing line: "Update this box every term; the dates above are the last verification."

**Addition D — "The Threat Landscape": append one sentence at the end of the section:**
"DeFi-specific risks — oracle manipulation, bridge exploits, liquidation cascades, composability failure — are covered in Chapter 5, *DeFi Risk*; treat every protocol you integrate as part of your attack surface."

**Addition E — "The Professional Launch Checklist", Pre-Launch → Legal:** add "[ ] Tax treatment of the airdrop, contributor payments, and treasury sales reviewed (Chapter 6)" and "[ ] MSB/money-transmitter analysis completed if you custody, redeem, or exchange for customers."

**Lab — extend "🔬 Hands-On Lab: Red-Team Your Own Project":**
- Individual Analysis, add item 6: **Buyer's Check yourself** — run Ch. 10's 60-second check on your token and paste the result into your one-page explainer's Risks section.
- Add item 7: **Phishing drill** — write the exact Discord message a scammer would send your holders, then write the pinned security rule that defeats it.
- Add item 8: **Regulator drill** — in one paragraph each, answer "Is this a security?" (Howey), "Are you a money transmitter?" (FinCEN section), and "What did your airdrop recipients owe in tax?" (Ch. 6 box).

---

## 4. Accuracy corrections (all verified August 2026)

| Location | Issue | Action |
|---|---|---|
| Ch. 0, "The Trust Problem" | Enron "$700 billion" | ~$74B |
| Ch. 0, "The Revolution…" | "In the United States… 1.8 billion adults globally" | Rewrite; ~1.4B (Global Findex) |
| Ch. 0/1/index | "65,000 TPS" | Qualify as theoretical |
| Ch. 1, "Phantom" | "open-source"; "3 million users" | Remove "open-source"; "more than 15 million monthly active users" |
| Ch. 3, "Squarespace Analogy" | "Solana Token Creator by Orca" | No such product; use Solana Compass Token Creator |
| Ch. 5, glossary "Raydium" | Serum order-book claim | Remove (Serum defunct 2022) |
| Ch. 9, "Credentials" | `isMutable: false` = soulbound | Wrong; fixed above |
| Ch. 9 | Core vs. Token Metadata mixed | Fixed above |
| Ch. 11 | Quadratic voting, two wrong definitions | Fixed above |
| Ch. 11 | "$6.43 per UNI" at launch | Opened near $3, doubled within a day |
| Ch. 3 vs. Ch. 6 | ATA rent $0.30 vs. $0.50; 10 SOL vs. $5,000 | Use one SOL price ($100) |
| Ch. 6 | Lab on devnet with a mainnet-only token | Resolved above |
| Ch. 9 | "Underdog Protocol" gate from Ch. 7 | Replaced with Collab.Land above |
| Ch. 7 | Holder.xyz (sunset), Grape Protocol (domain for sale), Guild.xyz (EVM-only) | Replaced with Collab.Land + Matrica above |
| Ch. 9 | studio.metaplex.com (404) | Replaced with LaunchMyNFT above |
| Ch. 5 | "under $1 in total transaction fees" / "$20" budget | Raydium charges 0.15 SOL to create a pool; corrected above |
| Ch. 5 lab | Phantom native staking | Requires 1 SOL minimum; lab uses Marinade for small amounts |
| index.md | Ch. 5 link 404; Dune and FinCEN promises | Fixed above |

---

## 5. New images needed (one list for the author)

`ch00-live-networks.png` (mempool.space vs. Solana explorer side by side) · `ch01-embedded-wallets.png` · `ch02-memecoin-actor-table.png` · `ch03-token2022-extensions-table.png` · `ch04-demand-vs-supply-inflection.png` · `ch05-cpmm-vs-clmm.png` · `ch05-sandwich-attack.png` · `ch05-bonding-curve-migration.png` · `ch05-rugcheck-annotated.png` · `ch05-defi-stack-overview.png` (the five legos) · `ch05-stablecoin-backing-models.png` · `ch05-staking-yield-decomposition.png` · `ch05-lending-market-health-factor.png` · `ch05-oracle-flow.png` · `ch05-liquidation-cascade.png` · `ch06-tax-events.png` · `ch07-solana-pay-qr-flow.png` · `ch08-pda-and-cpi.png` · `ch08-annotated-lib-rs.png` · `ch08-vulnerability-classes.png` · `ch09-compressed-nft-tree.png` · `ch10-buyers-check.png` · `ch11-treasury-runway.png` · `ch11-legal-wrappers.png` · `ch12-exemption-map.png` · `ch12-msb-decision-tree.png` · `ch12-regulatory-snapshot.png`

---

## 6. Sites used across the labs (for the resources page)

| Purpose | Site |
|---|---|
| Hash / block / chain / distributed demos | andersbrownworth.com/blockchain |
| Bitcoin blocks and fees, live | mempool.space |
| Solana explorer, live cluster stats | explorer.solana.com · solscan.io |
| Devnet SOL | faucet.solana.com |
| Wallet | phantom.com |
| Swap / aggregator | jup.ag |
| DEX / pools | raydium.io (also orca.so, meteora.ag) |
| Launchpads (observe) | pump.fun · raydium.io (LaunchLab) |
| Token risk check | rugcheck.xyz |
| Trading dashboard | dexscreener.com |
| Market intelligence | birdeye.so |
| Holder clustering (optional) | app.bubblemaps.io |
| Query dashboards | dune.com |
| DeFi TVL map | defillama.com/chain/Solana |
| Staking | Phantom built-in · marinade.finance · jito.network · solanacompass.com · validators.app |
| Lending | app.kamino.finance · app.marginfi.com |
| Oracle feeds | pyth.network/price-feeds |
| Payments spec | solanapay.com |
| Vesting / airdrops | app.streamflow.finance · airdrop.to |
| Token gating | collab.land (cc.collab.land) · matrica.io |
| Program IDE | beta.solpg.io |
| NFT minting / marketplaces | launchmynft.io · magiceden.io · tensor.trade |
| Multisig / governance | app.squads.so · app.realms.today |
| Token creators | tools.smithii.io (Token Creator; Tax Token Creator for Token-2022 transfer fees) · solanacompass.com/tools/create-solana-token |

*End of specification.*
