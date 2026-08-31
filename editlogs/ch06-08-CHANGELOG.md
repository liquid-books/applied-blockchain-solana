# Change Log — Chapters 6–8 (Edit Spec 2026-08)

Editor: additive-edit subagent · Date: 2026-08-31 · Scope: `chapters/ch06-distribute.md`, `chapters/ch07-utility.md`, `chapters/ch08-first-program.md`
SOL price constant used: **SOL ≈ $100** (per author correction to spec).

All changes are (a) insertions at spec-named locations or (b) corrections quoted in the spec. No other prose was touched.

---

## Chapter 6 — Distribute It (`ch06-distribute.md`)

### Corrections

1. **"Computing Your Distribution Cost", rent-exempt deposit paragraph** — ATA rent aligned to SOL ≈ $100:
   - OLD: "which costs ~\$0.50 per new account at current SOL prices. For 10,000 new recipients, this adds approximately \$5,000 to your distribution cost."
   - NEW: "which costs ~\$0.20 per new account at SOL ≈ \$100. For 10,000 new recipients, this adds approximately \$2,000 to your distribution cost."

### Insertions

2. **New admonition after "Computing Your Distribution Cost"** — `:::{admonition} The Tax Line Nobody Budgets` (`:class: warning`). First line of inserted text: "Distribution has a tax dimension that almost no first-time issuer budgets for." Covers: airdrops as ordinary income at FMV on receipt (IRS guidance since 2019, cross-ref FMV glossary entry); streaming/vesting releases as compensation taxable when received; liquidity adds/removes and swaps as taxable events; Form 1099-DA broker reporting; issuer's reporting duties when paying contractors in tokens; cross-ref Ch. 12 launch checklist.

3. **New figure after the tax admonition** — `fig-ch06-tax-events` (`../images/ch06-tax-events.png`) with descriptive alt text; filename added to NEW IMAGES NEEDED comment at chapter end.

4. **Top of "Hands-On Lab: Put Tokens in Other People's Hands"** — devnet resolution note inserted as `:::{note}`: "This lab runs on devnet because you will be sending tokens to many wallets and testing cancellation. Your Chapter 3 token exists only on mainnet. Mint a throwaway devnet token first (Chapter 3, Step 3b, or any creator switched to devnet) and use it for every step below."

5. **Lab Part 1 (Streamflow), new Step 7 appended** (existing steps 1–6 unchanged): "After the cliff, have the recipient withdraw once. Then, as the sender, **cancel** the stream. Record what returned to you and what stayed with the recipient. This is the clawback right from the Streaming Payments section, demonstrated."

6. **Lab, new "Part 4: Sybil-Test Your Own Airdrop (10 min)"** appended after Part 3: create a third Phantom account, re-run the CSV with the new address, observe nothing stops it, write three sentences on which Sybil defense would have stopped it and its cost/friction.

7. **Glossary — two new entries appended** (after "Treasury Multisig"): **Taxable Event**, **Form 1099-DA**.

8. **End of chapter** — `<!-- NEW IMAGES NEEDED: ch06-tax-events.png (...) -->` comment.

---

## Chapter 7 — Utility Without Code (`ch07-utility.md`)

### Sanctioned replacements (three named platforms dead as of Aug 2026: Holder.xyz sunset, Grape Protocol domain for sale, Guild.xyz EVM-only)

1. **Frontmatter tags** —
   - OLD: `[token utility, token-gating, Discord, Telegram, Holder.xyz, Grape, engagement loop, loyalty mechanics, tiered benefits, Web3 community]`
   - NEW: `[token utility, token-gating, Discord, Telegram, Collab.Land, Matrica, engagement loop, loyalty mechanics, tiered benefits, Web3 community, Solana Pay]`

2. **"How Token-Gating Platforms Work"** — the four platform paragraphs (Holder.xyz, Grape Protocol, Guild.xyz, Matrica) replaced with two:
   - **Collab.Land** — most widely installed gating bot; Discord and Telegram; TGR checks SPL balance or NFT collection on Solana; multiple TGRs per role; verify via Phantom through the bot's link; free tier for small servers.
   - **Matrica** — Solana-native; Discord and Telegram; rules on SPL balances, NFT collections, NFT traits; paid from ~$35/month.
   - The six-step "Each platform follows the same pattern" list kept unchanged.

3. **`fig-ch07-gating-platforms` caption and alt** —
   - OLD alt: "Comparison grid of four Solana token-gating platforms — Holder.xyz, Grape Protocol, Guild.xyz, and Matrica…" / OLD caption: "Four no-code platforms…"
   - NEW alt: "Comparison grid of two Solana token-gating platforms — Collab.Land and Matrica…" / NEW caption: "Collab.Land and Matrica, the two live no-code platforms… Both read on-chain balances; they differ in rule complexity, pricing, and ecosystem integrations."

4. **Lab "Choosing Your Platform"** —
   - OLD: "**Discord with Holder.xyz** — Best choice if your classmates are already on Discord. Free tier available, clean UI, automatic role management." → NEW: "**Discord with Collab.Land** — free for small servers, Solana supported, the most widely used gating bot."
   - OLD: "**Telegram with Matrica or Collabland**" → NEW: "**Telegram with Matrica**" (Collab.Land is now the Discord path).
   - OLD: "We will walk through the Discord + Holder.xyz path in detail." → NEW: "…Discord + Collab.Land path…"

5. **Lab section retitle** — "Step-by-Step: Discord Token Gating with Holder.xyz" → "Step-by-Step: Discord Token Gating with Collab.Land". Phase 1 unchanged.

6. **Lab Phase 2 replaced** (per spec script): Collab.Land Add-to-Discord + bot authorization + `#collabland-join` Let's Go button; Command Center (cc.collab.land) sign-in; TGRs → Add TGR (Chain Solana · SPL fungible · Ch. 3 mint address · Min balance 10 · Role Token Holder); drag bot role above Token Holder role.

7. **Lab Phase 3, step 2 replaced** —
   - OLD: "Have them go to holder.xyz, connect their wallet, and verify their holding. The Token Holder role should be assigned automatically."
   - NEW: "Have them click **Let's Go** in `#collabland-join`, choose **Phantom**, and sign the verification message. The Token Holder role is assigned within a minute."
   - Phases 1, 4 and the Telegram/Matrica alternative unchanged.

8. **Phase 4 screenshot bullet** — OLD: "The Holder.xyz rule configuration screen" → NEW: "The Collab.Land TGR configuration screen".

9. **`fig-ch07-holder-setup` caption and alt** — Holder.xyz dashboard wording → Collab.Land Command Center TGR wording.

10. **"🔗 Key Tools Referenced" table** — Holder.xyz, Grape Protocol, and Guild.xyz rows deleted; duplicate "Collabland" row deleted; new row added: "**Collab.Land** | Discord and Telegram token-gating for Solana | collab.land". Matrica, Phantom, Solana Explorer kept.

11. **Glossary** — **Holder.xyz** and **Grape Protocol** entries replaced with a single **Collab.Land** entry: "The most widely used token-gating bot for Discord and Telegram; on Solana it verifies SPL token balances and NFT holdings and assigns roles automatically." All other entries kept.

### Insertions

12. **"The Pricing Problem", dollar-denominated bullet** — appended: "— using a price oracle such as Pyth (Chapter 5, *Oracles*)."

13. **New subsection appended to "Payments in Your Own Token"** — `### The Rail: Solana Pay`. First line: "Everything above describes the economics of accepting your token." Covers the `solana:<recipient>?amount=…&spl-token=<mint>&label=…` URL/QR spec, sub-second on-chain settlement with no card network, connection to Ch. 2 Starbucks-on-chain and Ch. 8 loyalty check-in, Shopify checkout since 2023 (shopifydocs.solanapay.com), and Ch. 5 stablecoin connection (merchants request USDC, customers pay from any token via wallet swap). Includes new figure `fig-ch07-solana-pay` (`../images/ch07-solana-pay-qr-flow.png`).

14. **"On-Chain Utility vs. Traditional Loyalty Mechanics", after "The honest limitation…" paragraph** — two sentences appended: "That said, embedded wallets and passkey sign-in (Chapter 1) are closing the connect-wallet gap. The 2026 pattern is that the customer never sees a seed phrase and the token lives in a wallet created by the app."

15. **Lab restructure (headings only)** — new heading `### Part 1 — Build the Gate` inserted before "Choosing Your Platform"; existing lab steps otherwise unedited beyond the Collab.Land replacement.

16. **New lab "Part 2 — Get Paid in Your Token (15 min)"** inserted after the Telegram/Matrica alternative, before "Walk Away With": construct a Solana Pay request for the student's token, QR-encode it, classmate pays 5 tokens via Phantom mobile scan, verify on Solscan, repeat with USDC mint and amount 0.01, two-sentence write-up mapping to the chapter's three pricing approaches.

17. **Glossary — new entry appended**: **Solana Pay**.

18. **End of chapter** — `<!-- NEW IMAGES NEEDED: ch07-solana-pay-qr-flow.png (…); ch07-gating-platforms.png (UPDATE…); ch07-holder-setup.png (UPDATE…) -->` comment.

---

## Chapter 8 — Your First Program (`ch08-first-program.md`)

### Corrections

1. **Glossary "BPF (Berkeley Packet Filter)"** — appended: "Solana's runtime has since moved to SBF (Solana Bytecode Format), a fork of eBPF; the concept is unchanged."

### Insertions

2. **Addition A — "Step 2: Load the Counter Template", after the file list** — full `lib.rs` of the standard Solana Playground Anchor Counter template inserted as a `rust` code block with business-reader inline comments. First line of inserted text: "Here is the full `lib.rs`, annotated for a business reader." Annotations cover (all in comments; code compiles unchanged): `declare_id!` (the Program ID), the `#[program]` module (the instruction list / evaluation-checklist step 3), each `pub fn` (one instruction each), the `#[derive(Accounts)]` structs (the declared account list, shown as "Account Inputs" on Explorer), `Signer<'info>` (who must sign), `#[account(init, payer = user, space = 8 + 8)]` (data account created, payer covers Ch. 3 rent), and `#[account] pub struct Counter { pub count: u64 }` (state lives in an account, not the program — the chapter's central idea).

3. **New section inserted after "Instructions, Accounts, and Signers…", before "Code Is Law"** — `## How a Program Holds Your Token: PDAs and CPI`. First line: "Two more concepts complete the picture of how programs interact with tokens…" Covers: PDA (address computed from program ID + seeds, no private key exists, only the program can sign; how vesting contracts / pools / multisig vaults / escrows hold tokens; safe-with-no-key-only-a-rulebook analogy; Streamflow tie-back); CPI (a program calling another program; check-in program would call SPL Token `transfer`/`mint_to` signing as its PDA; Jupiter→Raydium, Kamino→Token program, Realms proposal execution); and evaluation-checklist step 6 (*which programs does this program call, and does it hold assets in PDAs or in a human's wallet?*). Includes new figure `fig-ch08-pda-cpi` (`../images/ch08-pda-and-cpi.png`).

4. **Addition C — "Reading, Not Writing, Code", after step 5 (audit reports)** — `:::{admonition} What Auditors Actually Look For` (`:class: important`): six vulnerability classes, one line each (missing signer check; missing owner check; account type confusion; arithmetic overflow/underflow; arbitrary CPI; closed-account revival); note that Anchor's `#[account(...)]` constraints prevent most of these ("built with Anchor" is a weak positive signal); Neodyme's "Sealevel attacks" named as the standard public reference.

### Sanctioned replacement

5. **"Stretch Activity: Add a Decrement Instruction" replaced with "Stretch Activity — Make the Program Touch a Token (30 min, devnet)"** (per spec script):
   - OLD (full text): "If you are comfortable with the code, try adding a `decrement` instruction using `increment` as a template. The only change needed is replacing `+= 1` with `-= 1`. Rebuild and redeploy. Run decrement and verify the count drops on Explorer."
   - NEW: 4 numbered steps — (1) create a throwaway devnet token in the Playground terminal (`spl-token create-token` / `create-account` / `mint <MINT> 100`); (2) gate the check-in with a `token_account: Account<'info, TokenAccount>` constrained to `token_account.owner == user.key()` and `token_account.amount >= 1`, importing `anchor_spl::token::TokenAccount`; rebuild and redeploy; (3) run `increment` with a funded token account (succeeds) and an empty one (constraint error); screenshot both on Explorer; (4) three sentences on which auditor-box vulnerability class omitting the `owner` constraint would introduce.
   - The escape-hatch sentence kept verbatim: "Students who do not wish to modify code: the deploy-and-test loop above, with the template unchanged, is the complete activity. You have deployed a real program."

6. **End of chapter** — `<!-- NEW IMAGES NEEDED: ch08-pda-and-cpi.png (…); ch08-annotated-lib-rs.png (…); ch08-vulnerability-classes.png (…) -->` comment.

---

## New images requested (consolidated)

- `ch06-tax-events.png`
- `ch07-solana-pay-qr-flow.png`
- `ch07-gating-platforms.png` (update existing: Collab.Land + Matrica only)
- `ch07-holder-setup.png` (update existing: Collab.Land Command Center)
- `ch08-pda-and-cpi.png`
- `ch08-annotated-lib-rs.png`
- `ch08-vulnerability-classes.png`
