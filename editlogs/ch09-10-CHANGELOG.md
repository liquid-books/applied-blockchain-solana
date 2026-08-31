# Change Log — Chapters 9 & 10 (EDIT-SPEC-2026-08)

All changes per `EDIT-SPEC-2026-08.md`. Additive-only except where the spec explicitly sanctioned replacements (dead tools verified Aug 2026: studio.metaplex.com 404, Underdog Protocol replaced with Collab.Land). SOL price constant: $100 per author correction — no dollar figures in these two chapters required it.

---

## Chapter 9 — `chapters/ch09-nfts-memberships.md`

### Corrections (old → new)

1. **"Fungible vs. Non-Fungible" — definition scoped.**
   - Old: "On Solana, a non-fungible token is technically a SPL token with a supply of exactly one, combined with a metadata account that describes what that single token *means*."
   - New: "Under the Metaplex Token Metadata standard used in this lab, an NFT is an SPL token with supply of one plus a metadata account that describes what that single token *means*."

2. **"Credentials and Certificates" — isMutable/soulbound fix.**
   - Old: "Metaplex supports this with a `isMutable: false` flag and the ProgrammableNFT standard."
   - New: "Non-transferability is enforced either by a Programmable NFT rule set that blocks transfers or, for fungible or semi-fungible credentials, by the Token-2022 Non-Transferable extension (Chapter 3). The metadata `isMutable` flag controls whether the description and image can change — it has nothing to do with transfer."

3. **"Storage: IPFS vs. Arweave" — lab tool reference.**
   - Old: "For our lab, we will use the Metaplex Candy Machine UI, which handles metadata upload automatically."
   - New: "For our lab, we will use LaunchMyNFT, which handles metadata upload automatically."

4. **Prerequisites — gate tool.**
   - Old: "Your Underdog Protocol token gate from Chapter 7…"
   - New: "Your Collab.Land token gate from Chapter 7…"

5. **Lab Overview.**
   - Old: "…using Metaplex's no-code tools…"
   - New: "…using a no-code launchpad…"

6. **`fig-ch09-candy-machine` caption/alt updated** (same image file retained).
   - Old caption: "**Metaplex Candy Machine Architecture.** The Candy Machine program sits on Solana and enforces your collection's rules — supply, price, dates, allowlists — without any custom code from you. The Studio UI is the control panel."
   - New caption: "**The Launchpad's Minting Program.** The launchpad's minting program sits on Solana and enforces your collection's rules — supply, price, dates — without any custom code from you. The launchpad's web interface is the control panel." Alt text updated to match.

7. **Candy Machine `:::{note}` reworded** (per spec: "reword it to describe Candy Machine as the developer-facing tool the launchpad wraps").
   - Old: "Candy Machine is Metaplex's minting infrastructure. It handles the mechanics of a fair launch: setting supply, price, mint dates, and allowlists. The Studio UI wraps all of that in a browser-based workflow."
   - New: "Candy Machine is Metaplex's minting infrastructure — now developer-facing tooling (a CLI and SDK) that launchpads like LaunchMyNFT wrap in a browser-based workflow. It handles the mechanics of a fair launch: setting supply, price, mint dates, and allowlists."

8. **Lab Part 3 — full sanctioned rewrite** (studio.metaplex.com is 404).
   - Old: "### Part 3 — Upload Metadata via Metaplex Candy Machine UI" pointing to studio.metaplex.com with 7 Studio-UI steps.
   - New: "### Part 3 — Deploy Your Collection with LaunchMyNFT" pointing to launchmynft.io with the 6 spec-scripted steps (Create → connect Phantom mainnet; Upload your own assets; collection settings incl. Symbol GPASS, Royalty 5%, Supply 5, Mint price 0 SOL; fee summary + Deploy; mint 2–3 passes; copy collection address for Part 4).

9. **Lab Part 4 — full sanctioned rewrite** (Underdog Protocol → Collab.Land TGRs).
   - Old: Underdog Protocol dashboard (app.underdogprotocol.com), "NFT Collection Gate" with AND condition, plus the two-factor test paragraph.
   - New: Collab.Land Command Center (cc.collab.land) → TGRs → Add TGR (Chain Solana · Token type NFT collection · Collection address from Part 3 · Min balance 1 · Role Gold Member); two independent roles (Token Holder from Ch. 7 + Gold Member); `#gold-lounge` channel; the two-factor observation (pass-only vs. tokens-only vs. both); the OR-vs-AND sentence (true AND gate enforced in your own backend, tying to the royalties paragraph). The existing "To test a failing case" paragraph is kept verbatim.

10. **Glossary swap.**
    - Old entry: "Candy Machine UI (Studio) — Metaplex's browser-based no-code interface for creating and deploying Candy Machine NFT collections without writing smart contract code."
    - New entry: "LaunchMyNFT — A no-code Solana NFT launchpad: upload assets, set supply, price and royalty, deploy, and mint from a hosted page; collections are recognized by Magic Eden and Tensor."

### Insertions

11. **"Royalties" section — new `:::{admonition} Two Metaplex Standards` box** (class: note), explaining Token Metadata (wraps an SPL mint; one mint + one metadata account per NFT) vs. Metaplex Core (single-account standard with plugins for royalties, freezing, transfer delegates; lower mint cost). The existing sentence "For this course, we will use Metaplex Core (the 2025 standard)…" was moved into this box per spec, plus the sentence that Candy Machine is now developer tooling ("Core Candy Machine") and the lab uses a no-code launchpad.
    - First line of inserted block: ":::{admonition} Two Metaplex Standards"

12. **"Storage: IPFS vs. Arweave" — new `:::{admonition} Compressed NFTs` box** (class: tip) after the Arweave paragraph: per-NFT rent prohibitive at 10,000 tickets/receipts; Bubblegum Merkle tree; fraction-of-a-cent mints; indexer needed; right tool for receipt/ticket use cases.
    - First line: ":::{admonition} Compressed NFTs"

13. **New figure directive** `fig-ch09-compressed-nft-tree` (`../images/ch09-compressed-nft-tree.png`) after the Compressed NFTs box, with descriptive alt and bold caption.

14. **New lab step — "### Part 7 — Read a Compressed Collection (5 min)"** after Part 6: read any large cNFT collection on Solscan, compare mint cost vs. the ~0.01 SOL LaunchMyNFT mint, record both.

15. **End-of-chapter comment:** `<!-- NEW IMAGES NEEDED: ch09-compressed-nft-tree.png (...) -->`

---

## Chapter 10 — `chapters/ch10-onchain-analytics.md`

### Insertions

1. **"The Analytics Stack" — new fourth tool subsection "### Dune — The Query Layer"** appended after the DexScreener subsection: Dune indexes Solana, anyone can write SQL or fork public dashboards; for this course, read rather than write. (Makes the index card true.)
   - First line: "### Dune — The Query Layer"

2. **"Liquidity Depth" — one sentence added** before the "Where to read it" line: "For the chain-wide version of this number see DeFiLlama (Chapter 5, *The DeFi Map*)."

3. **"Privacy in a Transparent World" box — one sentence appended:** "Token-2022 confidential transfers (Chapter 3) are the practical, non-ZK-research answer available today."

4. **New section "## Read a Token in 60 Seconds: The Buyer's Check"** inserted after "Comparative Analysis," before the Hands-On Lab. Contains a new figure directive `fig-ch10-buyers-check` (`../images/ch10-buyers-check.png`) and the 7-item numbered checklist with where-to-look for each (mint/freeze authority — Solscan/Ch. 3; LP lock — RugCheck/DexScreener/Ch. 5; top-10 concentration excl. pools — Solscan holders/this chapter; deployer history — creator address on Solscan; power-concentrating Token-2022 extensions — Solscan extensions panel/Ch. 3; organic volume — wash-trade test; published team/allocation/audit — Ch. 12). Closing line: "The whole check takes one minute and would have caught most rug pulls in the last three years."
   - First line: "## Read a Token in 60 Seconds: The Buyer's Check"

5. **Lab — new "### Step 1a: Read a Dune Dashboard (5 min)"** after Step 1: dune.com, search Solana dashboards, record one number and its date; no account or code needed.

6. **Lab — new "### Step 1b: Read the DeFi Map (5 min)"** after Step 1a: defillama.com/chain/Solana, record total TVL and top three protocols, label each (DEX/lending/liquid staking, defined in Chapter 5, *Beyond the Pool*), compare to Chapter 5 Part E.

7. **Lab — new "### Step 2a: Run the Buyer's Check (10 min)"** after Step 2: run the check on own token and benchmark, two-column table; optional Bubblemaps holder-cluster screenshot (connected bubbles = wallets funded from the same source — the Sybil and wash-trade fingerprint).

8. **Lab "Walk Away With" deliverable — Buyer's Check table added:** new bullet "**A Buyer's Check table** — the 60-second check run on your token and your benchmark, side by side, included with the dashboard."
   - Consequential one-word adjustment: "These two artifacts are…" → "These artifacts are…" (the list now has three items; noted for author review).

9. **End-of-chapter comment:** `<!-- NEW IMAGES NEEDED: ch10-buyers-check.png (...) -->`

---

## New images requested

- `ch09-compressed-nft-tree.png`
- `ch10-buyers-check.png`

(The existing `ch09-metaplex-candy-machine.png` was retained; only its caption/alt were updated. The author may wish to regenerate it without Metaplex Studio branding.)
