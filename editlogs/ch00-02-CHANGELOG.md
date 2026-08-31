# Change Log — Chapters 0–2 + index.md (Edit Spec 2026-08)

All edits per `EDIT-SPEC-2026-08.md`. Additive only; no existing prose rewritten except the quoted corrections listed below. Book-wide SOL price constant: **$100** (per author correction of 2026-08-31 superseding the spec's original $200).

---

## chapters/ch00-what-is-a-blockchain.md

### Corrections (old → new)

1. **"The Trust Problem"** — "Seven hundred billion dollars in shareholder value evaporated" → "Roughly \$74 billion in shareholder value evaporated" (Enron's peak market value was ~$70B).
2. **"The Revolution You Just Understood"** — "In the United States today, approximately 1.8 billion adults globally lack access to formal banking." → "Globally, about 1.4 billion adults lack access to formal banking (World Bank Global Findex)."
3. **`fig-ch00-global-impact` caption** — "1.8 billion adults lack formal banking access." → "About 1.4 billion adults lack formal banking access." (consistency with correction 2).
4. **"Consensus: How the Network Agrees"** — "…can process 65,000 transactions per second and complete them in 400 milliseconds" → "…can process a theoretical ceiling of 65,000 transactions per second (sustained real-world throughput is in the low thousands) and complete them in 400 milliseconds" (global TPS qualifier).
5. **Glossary** — deleted the duplicate second "Genesis Block" entry ("The first block in a blockchain — the origin of the entire chain.") at the end of the glossary block. The full first entry remains.

### Insertions

1. **Section:** `Alternative Chains — Different Tradeoffs` admonition — appended one bridge paragraph. First line: "Because these networks are separate ledgers, moving value between them requires a **bridge**: assets are locked on chain A, and a "wrapped" representation is minted on chain B…" (covers pooled value, Wormhole 2022 / Ronin 2022 hacks, Wormhole as Solana's primary bridge, cross-ref to Ch. 12 threat landscape).
2. **Section:** new `## 🔬 Hands-On Lab: See a Blockchain Work (30 minutes)` inserted immediately before `## 🎯 Activity: The NAAT Canvas`. First line: "Before the NAAT canvas, you will manipulate a hash, break a chain, and watch two live networks produce blocks." Contains Parts 1–5 (Hashes / A block / Break a chain / Distributed copies / Two live networks), figure directive `fig-ch00-live-networks` (`../images/ch00-live-networks.png`), and the one-page PDF deliverable.
3. **End of file** — HTML comment `NEW IMAGES NEEDED: ch00-live-networks.png`.

---

## chapters/ch01-first-transaction.md

### Corrections (old → new)

1. **"Phantom: Solana's Primary Wallet"** — "It is free, open-source, non-custodial, and integrates…" → "It is free, non-custodial, and integrates…" (Phantom is closed-source; audited).
2. **"Phantom: Solana's Primary Wallet"** — "…has grown to over 3 million active users." → "…has grown to more than 15 million monthly active users."
3. **Glossary "Phantom"** — "Free, open-source, and compatible…" → "Free and compatible…" (same open-source fix).
4. **"The Ethereum Challenge" (Speed paragraph)** — after the Layer-2 parenthetical, added two sentences: "In fairness, Ethereum's Layer-2 networks (Base, Arbitrum) are the realistic 2026 comparison on fees and speed, and on those metrics they are competitive with Solana. The book's argument for Solana rests on a single integrated execution layer — one chain, one fee market, one state — with no bridging between L1 and L2 for users or developers to manage."
5. **"The Anatomy of a Solana Transaction" Step 2** — "typically 0.000005 SOL, or about \$0.0008 at current prices." → "typically 0.000005 SOL, or about \$0.0005 at SOL ≈ \$100 (the price assumption used for dollar figures throughout this book)." (SOL ≈ $100 alignment).
6. **Comparison table** — "Avg. transaction fee … ~\$0.0008" → "~\$0.0005"; "Throughput (TPS) … 65,000+" → "65,000 (theoretical ceiling; sustained real-world throughput is in the low thousands)" (global TPS qualifier + $100 alignment).
7. **Activity Step 4** — "0.01 SOL (approximately \$1.50 at most price levels…)" → "0.01 SOL (approximately \$1 at SOL ≈ \$100…)".
8. **"The Revolution You Just Participated In"** — "…for \$0.0008 in fees" → "…for \$0.0005 in fees".

### Insertions

1. **Section:** "Custody Models: Self-Custody vs. Custodial Wallets" — new fourth subsection `### Embedded Wallets` after the Hardware Wallets subsection (before the custody-spectrum figure). First line: "A fourth model has become standard in consumer applications: the **embedded wallet** — a wallet created and managed inside an app by a wallet-as-a-service provider (Privy, Dynamic, and the embedded SDKs offered by major wallet vendors)." Two paragraphs (passkey login, no seed phrase; convenience/recoverability vs. app provider as quasi-custodian; cross-ref Ch. 7 UX). Includes figure directive `fig-ch01-embedded-wallets` (`../images/ch01-embedded-wallets.png`).
2. **End of "Custody Models" section** (after the custody-spectrum figure) — one pointer sentence: "Stablecoins such as USDC add a second custody question — the issuer's — covered in Chapter 5, *Beyond the Pool*."
3. **Glossary** — new entry `Embedded Wallet` (after Multisig): "A wallet created and managed inside an application by a wallet-as-a-service provider (e.g., Privy, Dynamic)…"
4. **End of file** — HTML comment `NEW IMAGES NEEDED: ch01-embedded-wallets.png`.

---

## chapters/ch02-design-your-token.md

### Corrections / sanctioned format conversion

1. **Glossary** — converted from bold-prose format (`**Term** — definition`) to the fenced ```{glossary}``` directive used by every other chapter. Every existing definition's wording preserved verbatim; only formatting changed (14 entries: Burn, Deflationary Token, Decimals, Fungible, Inflationary Token, Mint Authority, NAAT Framework, Non-Fungible, Reputation Token, Soulbound Token, SPL Token, Token Brief, Token Sink, Velocity).

### Insertions

1. **Section:** new `## The Hardest Version of the Test: Memecoins` inserted after "The 'Why Would Anyone Want This?' Test" and before "Activity: Write Your Token Brief". First line: "There is a category of token that fails everything this chapter teaches and still, sometimes, succeeds: the **memecoin**." Covers: definition (value = attention; Solana dominant since 2023; BONK, WIF), honest actor-table run (fails Failure Pattern 1 by construction; coordination game, not a business), three takeaways for business students (liquidity/distribution with zero utility; utility bolted on afterward is the reverse of this book's method; launch mechanics → Ch. 5), and a "Where the Analogy Breaks Down" line (collectible, not currency; Ch. 9's NFT lens). Includes figure directive `fig-ch02-memecoin-actor-table` (`../images/ch02-memecoin-actor-table.png`).
2. **"Access" subsection** — appended one DePIN paragraph after the Helium example. First line: "Helium is the archetype of a broader category: **DePIN** (decentralized physical infrastructure networks)…" (Helium = coverage, Hivemapper = mapping; both appear in this chapter's lab).
3. **"Ownership" subsection** — new admonition box after the RWA paragraph: `:::{admonition} How a Real-World Asset Becomes a Token` (`:class: note`). First line: "The pattern behind every legitimate RWA token has three parts." (SPV holds asset; token = claim on the entity; on-chain transfer restrictions; cross-refs Ch. 3 *Token-2022: Default Frozen / Permanent Delegate* and Ch. 12 exemptions).
4. **"🔬 Hands-On Lab"** — new `### Part 0: Run the Test on a Memecoin (Individual, 15 minutes)` inserted before Part 1. First line: "Open `https://dexscreener.com`, select the **Solana** chain filter, sort by 24h volume." (5 steps: DexScreener pick, record metrics, Solscan holders, actor table, three-sentence verdict).
5. **Glossary** — two new entries appended: `Memecoin` and `DePIN`.
6. **End of file** — HTML comment `NEW IMAGES NEEDED: ch02-memecoin-actor-table.png`.

---

## index.md

### Corrections (old → new)

1. **Chapter 5 card link** — `./chapters/ch05-raydium-liquidity.md` → `./chapters/ch05-liquidity-raydium.md` (live link 404 fix; verified against actual filename).
2. **"Why Solana"** — "Solana processes **65,000 transactions per second**…" → "Solana processes **a theoretical ceiling of 65,000 transactions per second** (sustained real-world throughput is in the low thousands)…" (global TPS qualifier); "…fees of approximately **\$0.0008** per transaction" → "**\$0.0005**" ($100 alignment).
3. **"What This Book Is", Chapter 5 line** — "Created a live liquidity pool on a decentralized exchange (Chapter 5)" → "Created a live liquidity pool on a decentralized exchange, for the cost of a pool-creation fee and a few dollars of liquidity (Chapter 5)" (per spec's Ch. 5 corrections: Raydium's 0.15 SOL pool-creation fee supersedes the old "$20" framing).

### Insertions

1. **"Why Solana"** — new sentence after the performance paragraph: "Dollar figures throughout this book assume SOL ≈ \$100. Recompute with the current price."

### Explicitly NOT touched (per task instructions)

- Ch. 10 card text ("Dune Analytics, Solscan…") — stays; promise fulfilled by another agent's Ch. 10 edits.
- Ch. 12 card text ("FinCEN compliance") — stays; promise fulfilled by another agent's Ch. 12 edits.

---

## Notes for the author

- SOL price constant applied as **$100** everywhere (author correction of 2026-08-31; spec commit 81e8bc6). Fee figure recomputed: 0.000005 SOL × $100 = $0.0005.
- New images needed (also listed as HTML comments at the end of each chapter file): `ch00-live-networks.png`, `ch01-embedded-wallets.png`, `ch02-memecoin-actor-table.png`.
