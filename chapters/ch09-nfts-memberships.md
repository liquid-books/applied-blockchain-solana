---
title: "Chapter 9: Ownership as an Asset — NFTs and Memberships"
subtitle: "Forget the monkey pictures. An NFT is a deed."
short_title: "NFTs and Memberships"
description: "Non-fungible tokens make unique ownership transferable, turning memberships, tickets, and credentials into assets customers can hold and resell. Learn Metaplex metadata standards, royalty mechanics, and how to build tiered membership economies on Solana."
label: ch-09-nfts-memberships
tags: [nft, solana, metaplex, membership, token-gating, royalties, secondary-market]
---

# Ownership as an Asset — NFTs and Memberships

:::{figure} ../images/ch09-explainer-infographic.png
:label: fig-ch09-explainer
:alt: Comprehensive infographic summarizing NFTs as ownership deeds, Metaplex metadata standards, membership tiers, royalties, and secondary markets on Solana
:width: 80%
:align: center

**Chapter 9 at a Glance.** NFTs are programmable deeds — not pictures. This chapter maps the full lifecycle from minting a membership pass to observing it trade on a secondary market.
:::

Every new technology arrives draped in its worst possible use case. The steam engine's first public demonstration ended in a fatal crash. The internet's early reputation was built on dial-up pornography and pyramid schemes. And NFTs, despite the infrastructure they introduced, became synonymous with cartoon apes selling for millions of dollars and then losing most of that value inside eighteen months.

That's unfortunate. Because underneath the speculation, the NFT standard solved a real problem: *how do you prove unique ownership of a digital thing on a public ledger?*

**▶ Watch: NFTs Explained in 4 minutes!** (3 min)

<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;max-width:100%;margin:1.5rem 0;">
<iframe src="https://www.youtube.com/embed/FkUn86bH34M" style="position:absolute;top:0;left:0;width:100%;height:100%;border:0;" allowfullscreen title="YouTube video"></iframe>
</div>

This chapter answers that question — and then turns it into a business tool. By the end of the session you will have designed a three-tier membership pass collection, minted it on Solana mainnet, connected those passes to the token gate you built in Chapter 7, and listed one pass on a marketplace to observe secondary-market mechanics firsthand. You will walk away holding a transferable, resalable asset that represents access to something your business actually offers.

---

## Fungible vs. Non-Fungible: When Uniqueness Matters

In Chapter 2 you created a fungible token. Every unit of that token is identical to every other unit — interchangeable, like dollar bills. One SOL equals one SOL equals one SOL. That interchangeability is a feature: it's what makes a currency spendable.

But imagine you're issuing access to the front row at your annual conference. Seat 1A is not the same as seat 47C, even though they're both "seats." A deed to a specific house on a specific lot is not the same as a deed to a different house, even if both houses cost the same. Some assets derive their entire value from *which specific thing* they represent. They are non-fungible — each one is unique.

:::{figure} ../images/ch09-fungible-vs-nonfungible.png
:label: fig-ch09-fungible-nonfungible
:alt: Side-by-side comparison diagram showing fungible tokens as identical interchangeable coins versus non-fungible tokens as unique distinct deeds with serial numbers
:width: 80%
:align: center

**Fungible vs. Non-Fungible.** Fungible tokens are interchangeable units. Non-fungible tokens carry unique identity — like serial numbers on physical assets.
:::

Under the Metaplex Token Metadata standard used in this lab, an NFT is an SPL token with supply of one plus a metadata account that describes what that single token *means*. That metadata account — maintained by Metaplex's Token Metadata program — is what transforms a raw on-chain record into something a human being can recognize as "Gold Member Pass #47."

The insight that matters for business builders: **if your product has unique instances, NFTs give those instances provable, transferable identity.** That's the whole idea, stripped of the hype.

---

## NFTs as Membership, Ticket, Credential, and Receipt

The creative and collector markets were the first to adopt NFTs because scarcity and provenance matter enormously in art. But the underlying mechanics serve every industry where unique ownership matters.

:::{figure} ../images/ch09-business-use-cases.png
:label: fig-ch09-use-cases
:alt: Four-panel infographic showing NFT use cases: membership passes, event tickets, professional credentials, and purchase receipts, each with real-world business examples
:width: 80%
:align: center

**Four Real Business Use Cases for NFTs.** Memberships, tickets, credentials, and receipts all share the need for unique, provable ownership — exactly what non-fungible tokens provide.
:::

### Memberships

A gym membership, a wine club subscription, a co-working space access pass: all of these are currently managed in centralized databases. The business decides whether you're a member. The business decides what you're entitled to. And when you leave, the membership evaporates.

An NFT membership inverts some of that logic. The pass lives in your wallet. Your entitlements are readable by any application that checks the chain. And if the business allows it, you can sell the remaining term of your membership to someone else — treating unused subscription value like a transferable asset rather than a sunk cost.

### Event Tickets

Ticket scalping exists because current ticketing infrastructure has no elegant way to let the original issuer participate in secondary-market revenue. NFT tickets change this. When a ticket trades on a secondary market, the smart contract can route a royalty percentage back to the event organizer. The organizer earns from resales. And buyers get cryptographic proof the ticket is authentic — no Ticketmaster barcode fraud.

### Credentials and Certificates

A university diploma verifiable on-chain. A professional certification that any employer can confirm in seconds. A completion badge from an online course that lives in your wallet and travels with you across platforms. These are sometimes called "soulbound tokens" — NFTs designed to be non-transferable, proving credentials belong permanently to one holder. Non-transferability is enforced either by a Programmable NFT rule set that blocks transfers or, for fungible or semi-fungible credentials, by the Token-2022 Non-Transferable extension (Chapter 3). The metadata `isMutable` flag controls whether the description and image can change — it has nothing to do with transfer.

### Receipts and Warranties

Some brands are experimenting with minting an NFT at point of sale that functions as a digital receipt *and* warranty document. The NFT proves you bought the product. If you sell the product, the receipt (and remaining warranty) transfers with it. No lost receipts. No warranty fraud.

### The Common Thread

Notice what all four use cases share: a need to say "this specific thing belongs to this specific person, and that fact should be verifiable by anyone." That's what Metaplex's NFT standard delivers.

---

## Metadata Standards: Metaplex and Where the "Thing" Actually Lives

Here is the question that trips up most students: if an NFT is just a token on the blockchain, where does the actual content live? The image, the description, the attributes?

Not on-chain. Almost never on-chain. Storing a high-resolution image directly on Solana would cost thousands of dollars in rent. Instead, the NFT's on-chain record contains a URI — a pointer to a JSON file. That JSON file is the *metadata*. The metadata contains the name, description, image URL, and any attributes.

:::{figure} ../images/ch09-metadata-architecture.png
:label: fig-ch09-metadata
:alt: Architecture diagram showing the chain of pointers from wallet to SPL token to Metaplex metadata account to IPFS JSON file to image storage, with labels at each layer
:width: 80%
:align: center

**Where the "Thing" Actually Lives.** The blockchain holds a pointer. The metadata JSON is stored off-chain (IPFS or Arweave). The image lives at a URL referenced inside the JSON. Each layer verifiable, each layer replaceable.
:::

### The Metaplex Metadata Schema

Metaplex defines a standard JSON format that every wallet, marketplace, and dApp on Solana understands:

```json
{
  "name": "Gold Member Pass #47",
  "symbol": "GPASS",
  "description": "Holder receives Gold-tier benefits at TokenSystems events.",
  "seller_fee_basis_points": 500,
  "image": "https://arweave.net/abc123/47.png",
  "attributes": [
    { "trait_type": "Tier", "value": "Gold" },
    { "trait_type": "Benefits", "value": "VIP Lounge, Front Row, 20% Merch Discount" },
    { "trait_type": "Issued", "value": "2026-01" }
  ],
  "properties": {
    "files": [{ "uri": "https://arweave.net/abc123/47.png", "type": "image/png" }],
    "category": "image",
    "creators": [
      { "address": "YourWalletAddressHere", "share": 100 }
    ]
  }
}
```

The field `seller_fee_basis_points: 500` encodes a 5% royalty on secondary sales. Every marketplace that respects Metaplex royalties (and not all do — more on this shortly) will route 5% of any resale price back to the `creators` array.

### Storage: IPFS vs. Arweave

The metadata JSON and image need to live somewhere persistent. Two options dominate:

**▶ Watch: IPFS: Interplanetary file storage! (9 min)**

<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;max-width:100%;margin:1.5rem 0;">
<iframe src="https://www.youtube.com/embed/5Uj6uR3fp-U" style="position:absolute;top:0;left:0;width:100%;height:100%;border:0;" allowfullscreen title="YouTube video"></iframe>
</div>

- **IPFS via NFT.Storage or Pinata**: Content-addressed storage. Your file is identified by a hash of its contents. Free tiers exist. The risk: if no node is "pinning" your file, it can disappear.
- **Arweave**: Pay once, stored permanently. Arweave's economic model is designed around perpetual storage. Bundlr (now Irys) makes Arweave uploads easy and cheap — a 1 MB file costs fractions of a cent. For production memberships where the metadata must exist forever, Arweave is the standard choice.

:::{admonition} Compressed NFTs
:class: tip

For 10,000 tickets or receipts, per-NFT rent is prohibitive. **Compressed NFTs** (Metaplex Bubblegum) store the collection in a Merkle tree so minting costs a fraction of a cent each, at the cost of needing an indexer (RPC provider) to read them. This is the right tool for the "receipt at point of sale" and "ticket" use cases in this chapter.
:::

:::{figure} ../images/ch09-compressed-nft-tree.png
:label: fig-ch09-compressed-nft-tree
:alt: Diagram of a compressed NFT collection stored as a Merkle tree, contrasting per-NFT rent for standard NFTs with fraction-of-a-cent minting for compressed NFTs read via an indexer
:width: 80%
:align: center

**Compressed NFTs.** A standard NFT pays rent for its own accounts; a compressed collection stores thousands of assets in one Merkle tree, cutting mint cost to a fraction of a cent — read back through an indexer rather than directly from account state.
:::

For our lab, we will use LaunchMyNFT, which handles metadata upload automatically.

---

## Royalties: Programmable Resale Economics and Their Limits

The royalty concept sounds like a revolution: creators earn a percentage every time their asset trades hands. A musician mints 1,000 concert passes. Every time one resells, 7% flows back automatically. The artist participates in the secondary market forever.

:::{figure} ../images/ch09-royalty-flow.png
:label: fig-ch09-royalty
:alt: Flow diagram showing NFT secondary sale price split into royalty percentage going back to creator and net amount going to seller, with marketplace fee also deducted, labeled percentages and arrows
:width: 80%
:align: center

**How NFT Royalties Flow.** On every secondary sale, the marketplace splits the price: seller receives the bulk, creator receives the royalty percentage encoded in metadata, marketplace keeps its fee.
:::

### The Honest Truth About Royalty Enforcement

Here is where the analogy breaks down, and intellectual honesty requires saying so: **royalties encoded in NFT metadata are not technically enforceable.** They are a convention, not a protocol-level rule.

In 2022–2023, a wave of NFT marketplaces (Blur, most notably) launched with zero-royalty trading to attract volume. Creators saw royalty revenue collapse. The community response was Metaplex's **Programmable NFTs (pNFTs)** and the **Token-2022 Transfer Hook** standard — both of which allow creators to encode rules that marketplaces *must* enforce or the transfer will fail at the protocol level.

For membership passes — where the issuer has ongoing control of the backend system granting benefits — there is an even simpler solution: **the benefit is delivered by your backend, not enforced by the chain alone.** If someone buys your pass on a secondary market without paying the royalty, your backend can simply check whether the sale was royalty-compliant before granting access. You control the door; you can demand the toll was paid.

:::{admonition} Two Metaplex Standards
:class: note

Metaplex maintains two NFT standards, and you will encounter both. **Token Metadata** — the standard this chapter's schema and lab use — wraps an SPL mint: one mint plus one metadata account per NFT. **Metaplex Core** is a newer single-account asset standard with built-in plugins for royalties, freezing, and transfer delegates, and a lower minting cost. For this course, we will use Metaplex Core (the 2025 standard) which supports transfer delegates and lifecycle hooks, giving creators meaningful programmatic control over transfers. Metaplex's own Candy Machine tooling is now developer tooling (a CLI and SDK — "Core Candy Machine"), so the lab uses a no-code launchpad and describes both standards.
:::

---

## Combining a Fungible Token and an NFT: Tiered Economies

Here is where the concepts from the whole course converge. You have a fungible token (your SPL token from Chapter 3). You have a token gate (Chapter 7). Now add an NFT membership pass.

The architecture is a tiered economy:

1. **The Pass** (NFT) — proves your tier. Bronze, Silver, or Gold.
2. **The Token** (SPL fungible) — the currency that flows through the system.
3. **The Gate** — checks both the pass and the token balance before granting access to benefits.

:::{figure} ../images/ch09-tiered-economy.png
:label: fig-ch09-tiered
:alt: Three-tier pyramid diagram showing Bronze Silver Gold membership NFT passes on left connecting to SPL token flows in center and gated benefits on right, with escalating rewards at each tier
:width: 80%
:align: center

**Tiered Economy Architecture.** The NFT pass establishes your tier. The fungible token is the currency. The token gate reads both and delivers escalating benefits — a complete membership economy in three moving parts.
:::

### A Concrete Example: TokenSystems Academy

Imagine you run a professional development platform for blockchain builders. Here's a tiered economy design:

:::{list-table} TokenSystems Academy Tier Structure
:header-rows: 1
:label: tbl-ch09-tiers

* - Tier
  - NFT Pass
  - SPL Token Requirement
  - Benefits
* - Bronze
  - Bronze Academy Pass
  - Hold 100 LEARN tokens
  - Community forum, recorded sessions
* - Silver
  - Silver Academy Pass
  - Hold 500 LEARN tokens
  - Live sessions, office hours access
* - Gold
  - Gold Academy Pass
  - Hold 2,000 LEARN tokens
  - 1-on-1 mentorship, early access, governance voting
:::

The pass proves your tier. The token balance proves your stake. Both together unlock the benefit. If you sell your Gold pass on a secondary market, the new holder gets Gold benefits *if they also hold the required token balance.* This design creates demand for both the pass and the token simultaneously — each amplifies the value of the other.

### Why This Works

Fungible tokens are great for *degree* — how much of something you hold. NFTs are great for *kind* — which specific thing you hold. Combining them means you can say "hold at least this much of this currency, and hold specifically this type of pass" — richer conditions than either instrument alone.

---

## Secondary Markets: Why Resale Value Is a Feature, Not a Bug

Traditional membership businesses fear transferability. A gym signs you to a 12-month contract, wants to keep you locked in, and loses nothing when you cancel because they capture the full year up front. The idea of you selling your remaining months to a stranger seems threatening — it disrupts their control of the member roster.

:::{figure} ../images/ch09-secondary-market-mechanics.png
:label: fig-ch09-secondary
:alt: Marketplace interface diagram showing NFT membership pass listing price secondary sale flow with buy now offer and royalty distribution breakdown
:width: 80%
:align: center

**Secondary Market Mechanics.** A membership pass listed on Magic Eden or Tensor shows the floor price, recent sales, and royalty settings — giving both buyers and sellers transparent information that centralized membership markets never offered.
:::

Reframe it: **resale value is the most powerful marketing tool a membership business can offer.**

If your Gold membership pass holds its value — or appreciates — on the secondary market, every member is incentivized to join early and stay. The membership becomes an investment as well as a service relationship. Members who no longer need the benefits recover value rather than feeling like they wasted money. And the marketplace listing is itself advertising: anyone browsing Magic Eden or Tensor for blockchain-related passes might discover your community for the first time.

### The Marketplaces

Two marketplaces dominate Solana NFT trading in 2026:

- **Magic Eden** (magiceden.io): The largest Solana NFT marketplace by volume. Supports collection listings, offers, and royalty enforcement via their royalty toggle. Has expanded to Bitcoin Ordinals and Ethereum, but Solana remains their home.
- **Tensor** (tensor.trade): Preferred by power traders. Offers advanced tools like sweep buying, bulk listing, and AMM-style liquidity pools for NFT collections. Lower-fee structure, higher sophistication barrier.

For the lab, you will list one pass on Magic Eden because the interface is designed for accessibility and you will observe the listing mechanics in real time.

---

## 🔬 Hands-On Lab: Mint a Membership Pass Collection

### Overview

You will design a three-tier membership NFT collection using a no-code launchpad, mint passes on Solana mainnet, connect the tiers to your Chapter 7 token gate, and list one pass on a marketplace.

:::{figure} ../images/ch09-lab-workflow.png
:label: fig-ch09-lab
:alt: Step-by-step workflow diagram showing four stages of the lab: design metadata, upload to Arweave via Sugar, mint via Candy Machine, connect to token gate and list on marketplace
:width: 80%
:align: center

**Lab Workflow.** Four stages from metadata design to live marketplace listing. Each stage builds on the previous, culminating in a real, tradeable membership pass.
:::

### Prerequisites

- Phantom wallet with at least 0.05 SOL on mainnet (to cover minting fees)
- Your SPL token from Chapter 3 (the fungible token your members will hold)
- Your Collab.Land token gate from Chapter 7 (or a new one created following Chapter 7 instructions)
- A laptop with a browser — no code editor required for the core lab

### Part 1 — Design Your Three-Tier Collection

Before touching any tool, design your collection on paper (or a doc):

**Tier Design Template:**

| Field | Bronze | Silver | Gold |
|-------|--------|--------|------|
| Name | `[YourBrand] Bronze Pass #001` | `[YourBrand] Silver Pass #001` | `[YourBrand] Gold Pass #001` |
| Description | Entry-level community access | Mid-tier with live sessions | Full access + mentorship |
| Image Style | Bronze metallic card | Silver metallic card | Gold metallic card |
| Attribute: Tier | Bronze | Silver | Gold |
| Attribute: Supply | 100 | 50 | 20 |
| Token Requirement | 100 tokens | 500 tokens | 2,000 tokens |

Keep supply intentional. Scarcity matters for the secondary market: Gold passes should be rare enough that their floor price reflects real exclusivity.

### Part 2 — Create Images for Each Tier

For this lab, you will create three simple pass images — one per tier. Options:

**Option A (No Code):** Use Canva (canva.com). Create a 1:1 square image (1000×1000px). Design a membership card aesthetic with:
- Your brand name
- The tier name (Bronze / Silver / Gold)
- A color palette matching the tier (warm browns for Bronze, cool grays for Silver, rich golds for Gold)

**Option B (AI-generated):** Use any image generation tool (Gemini, DALL-E, Midjourney) with this prompt framework:
> "A premium digital membership card for [YourBrand]. [Tier] tier. Metallic [bronze/silver/gold] aesthetic. Minimalist, professional, dark background. Card shows membership tier and brand name. Square format."

Save each as a PNG file: `bronze.png`, `silver.png`, `gold.png`.

### Part 3 — Deploy Your Collection with LaunchMyNFT

**Navigate to:** [launchmynft.io](https://www.launchmynft.io) — a live no-code Solana NFT launchpad whose collections are recognized by Magic Eden and Tensor.

:::{figure} ../images/ch09-metaplex-candy-machine.png
:label: fig-ch09-candy-machine
:alt: NFT launchpad minting architecture diagram showing collection config, Solana minting program, hosted mint page, and user wallets
:width: 80%
:align: center

**The Launchpad's Minting Program.** The launchpad's minting program sits on Solana and enforces your collection's rules — supply, price, dates — without any custom code from you. The launchpad's web interface is the control panel.
:::

:::{note}
Candy Machine is Metaplex's minting infrastructure — now developer-facing tooling (a CLI and SDK) that launchpads like LaunchMyNFT wrap in a browser-based workflow. It handles the mechanics of a fair launch: setting supply, price, mint dates, and allowlists.
:::

**Steps:**

1. Go to `https://www.launchmynft.io` → **Create** → connect Phantom (mainnet).

2. Choose **Upload your own assets**. Upload `gold.png` (and, if you like, `silver.png` and `bronze.png` as separate items) with a name for each ("Gold Member Pass #1").

3. Fill in the collection settings: **Collection name**, **Symbol** (`GPASS`), **Description**, **Royalty** 5%, **Supply** 5, **Mint price** 0 SOL, mint start **now**.

4. Review the fee summary LaunchMyNFT shows (a small per-collection deployment fee in SOL plus network rent), then **Deploy** and approve the transactions in Phantom.

5. On your collection's mint page, mint 2–3 passes to your own wallet. Confirm they appear in Phantom under **Collectibles**.

6. Copy the **collection address** from the collection page (or from one pass's Solscan page under "Collection"). You need it for Part 4.

### Part 4 — Connect Tiers to Your Token Gate

Return to the Collab.Land Command Center (`https://cc.collab.land`) — the Chapter 7 Discord tool — and sign in with Discord.

**Create a second Token Gating Rule:**

In the Command Center, open **TGRs** → **Add TGR** and set:

- **Chain:** Solana
- **Token type:** NFT collection
- **Collection address:** (paste the collection address from Part 3)
- **Min balance:** 1
- **Role:** Gold Member

You now have two independent, automatically maintained roles: **Token Holder** (2,000 tokens, from Chapter 7) and **Gold Member** (holds a Gold pass). Create a `#gold-lounge` channel visible only to Gold Member.

Then observe the two-factor check directly: a wallet holding the pass but not the tokens gets `#gold-lounge` but not `#holders-only`; a wallet holding tokens but no pass gets the reverse; only a wallet with both sees both.

Discord roles combine as OR, so a true AND gate (pass *and* balance for a single door) is enforced in your own app or backend that reads both — which is exactly what the chapter's "the benefit is delivered by your backend" paragraph on royalties already says.

**To test a failing case:** Create a second wallet with no NFTs and visit the gate. You should be denied access. This confirms the gate is reading on-chain state correctly.

### Part 5 — List on a Marketplace

Navigate to [magiceden.io](https://magiceden.io).

1. Click "My Items" (top right, after connecting your wallet)
2. Your minted Gold passes should appear
3. Click a pass → "List for Sale"
4. Set a price (even 0.001 SOL is fine — this is for observation, not profit)
5. Sign the transaction

:::{tip}
Once listed, observe the collection page. Magic Eden will show: floor price, number listed, 24h volume, royalty setting, and recent sales. This is the secondary market in real time — even for a brand-new collection with only your listing.
:::

**Screenshot** your listing and the collection page analytics for your lab report.

### Part 6 — Observe and Reflect

Leave your pass listed for the duration of the class session. Note:

- Did anyone view it? (Magic Eden shows view counts)
- Does the collection appear in search results?
- What is the difference between the "list price" and the "buy now" price?
- Where does the royalty percentage appear in the listing interface?

### Part 7 — Read a Compressed Collection (5 min)

On Solscan, open any large Solana NFT collection minted as cNFTs (search "compressed" in the NFT section or use a collection the instructor supplies) and note the mint cost of one asset vs. the ~0.01 SOL of your LaunchMyNFT mint. Record both.

---

## 🎯 In-Class Assignment: Design Your Membership Economy (10 pts)

**Details and instructions will be provided in class.**

**Points:** 10

---

## 💬 Discussion: The Gym Membership Question

If a gym membership were an NFT, you could sell the remaining months to a stranger. The gym loses control of who its members are — someone the gym never vetted, never onboarded, never built a relationship with suddenly holds an active membership. But the gym gains a liquid product: memberships with real resale value attract customers who see purchasing as an investment, not a sunk cost.

:::{figure} ../images/ch09-discussion-illustration.png
:label: fig-ch09-discussion
:alt: Split illustration showing traditional gym membership locked to one person on the left versus NFT gym membership as a transferable asset on a marketplace on the right, with pros and cons labeled
:width: 80%
:align: center

**Transferable Membership: Two Sides.** Traditional memberships are locked. NFT memberships are liquid. The business gains a marketing mechanism and secondary-market revenue; it trades away roster control and relationship continuity.
:::

**Would businesses embrace or resist transferable memberships — and which customers benefit most?**

Consider both sides:

**The Case for Transferability:**
- Members who no longer need the service recover value rather than eating the cost — more willing to commit to annual plans
- Secondary market listings are free advertising — new buyers discover your brand browsing a marketplace
- Royalties let the business participate in every resale — revenue that doesn't exist in traditional subscriptions
- Early adopters and power users have a financial incentive to join before prices rise

**The Case Against:**
- The business loses the ability to vet members — safety-sensitive services (gyms, clubs, professional networks) have real screening needs
- Relationship continuity breaks — every resale resets the customer relationship
- Pricing power erodes — if secondary prices drop below the primary price, you've signaled your membership isn't worth what you charged
- Legal complexity — are membership terms transferable? Does the new holder inherit the old member's obligations?

**Discussion Guidelines:**

Write a substantive post (minimum 300 words) that takes a clear position AND acknowledges the strongest counterargument. Cite at least one credible source — a news article, academic paper, or documented industry case — that supports your reasoning. A position without evidence is an opinion; with evidence it becomes an argument.

After posting, respond to at least **two peers** with substantive feedback. "I agree" is not feedback. Identify something specific in their argument you found compelling *and* one assumption they made that you'd push back on. Quality of engagement matters more than quantity.

Do not simply list pros and cons without committing. The best posts make a decision and defend it.

---

## 📖 Glossary

:::{glossary}
Non-Fungible Token (NFT)
  A blockchain token with a supply of exactly one, carrying unique metadata that distinguishes it from every other token. On Solana, implemented via the Metaplex Token Metadata program.

Metaplex
  The primary NFT standard and tooling ecosystem on Solana. Defines the metadata schema, Candy Machine minting infrastructure, and Programmable NFT rules that wallets and marketplaces understand.

Candy Machine
  Metaplex's minting program. Handles the mechanics of a fair NFT launch — supply cap, pricing, mint dates, allowlists, and metadata reveal — without custom smart contract code.

Metadata URI
  A URL stored in the on-chain NFT account that points to a JSON file describing the token's name, image, description, and attributes. The actual content lives off-chain.

IPFS (InterPlanetary File System)
  A decentralized content-addressed storage network. Files are identified by their content hash rather than a server address. Commonly used for NFT metadata storage; pinning required for persistence.

Arweave
  A permanent decentralized storage network. Pay once at upload, stored forever. The preferred storage solution for production NFT metadata where permanence matters.

Seller Fee Basis Points
  The royalty percentage encoded in Metaplex metadata. `500` = 5%. Marketplaces that honor royalties pay this fraction of every secondary sale to the creator.

Programmable NFT (pNFT)
  A Metaplex NFT standard (2023+) that encodes transfer rules at the protocol level. Marketplaces cannot bypass royalties or restrictions without the transfer failing on-chain.

Token Gate
  An access control system that reads a user's wallet to verify they hold specific tokens or NFTs before granting access to content, events, or services.

Floor Price
  The lowest listed price for any NFT in a given collection on a secondary market. The most widely watched metric for collection health.

Royalty
  A percentage of a secondary sale price routed to the original creator, encoded in NFT metadata. Enforceability varies by marketplace.

Tiered Economy
  A membership structure combining NFT passes (defining tier membership) with fungible token requirements (proving stake level) to gate escalating benefits.

Soulbound Token
  An NFT designed to be permanently non-transferable — proving a credential or achievement belongs to one specific wallet forever.

Magic Eden
  The largest Solana NFT marketplace by trading volume (2026). Supports royalties, collection analytics, and offers.

Tensor
  A Solana NFT trading platform preferred by sophisticated traders, offering AMM liquidity, bulk tools, and lower fees than Magic Eden.

LaunchMyNFT
  A no-code Solana NFT launchpad: upload assets, set supply, price and royalty, deploy, and mint from a hosted page; collections are recognized by Magic Eden and Tensor.

Transfer Hook
  A Solana Token-2022 feature allowing custom logic to execute on every transfer — enabling royalty enforcement and transfer restrictions at the protocol level.
:::

---

## 🏁 Walk Away With

By completing this chapter you now hold:

1. **A minted NFT membership pass collection** — real assets on Solana mainnet representing tiered access to a service
2. **A functioning token gate** reading both NFT and token balance — two-factor membership verification
3. **A live marketplace listing** — your first participation in secondary-market mechanics
4. **A mental model** for designing tiered economies that combine fungible currencies with non-fungible passes

The bigger takeaway is structural. Every business that sells access — subscriptions, event tickets, professional networks, loyalty programs — is currently built on centralized databases that they control entirely. NFT-based memberships redistribute some of that control to members: their pass lives in their wallet, their benefits are readable by any application, and their unused subscription value is recoverable. That's a meaningfully different relationship between a business and its customers — one that some businesses will embrace and many will resist, but none should ignore.

---

## Chapter Summary

- **NFTs are deeds**, not pictures. They prove unique ownership of a specific digital record.
- **Metaplex** is the standard. The Token Metadata program defines what NFTs mean on Solana.
- **Metadata lives off-chain** — pointed to by a URI in the on-chain account. IPFS or Arweave for storage.
- **Royalties are conventions**, not guarantees. Programmable NFTs and Transfer Hooks move toward protocol-level enforcement.
- **Combining NFTs with fungible tokens** creates tiered economies richer than either instrument alone.
- **Secondary markets are marketing.** Resale value attracts buyers who see membership as investment, not expense.
- **Metaplex Candy Machine** lets you launch a membership collection without writing code.

<!-- NEW IMAGES NEEDED: ch09-compressed-nft-tree.png (compressed NFT Merkle tree vs standard per-NFT rent, indexer read path) -->

