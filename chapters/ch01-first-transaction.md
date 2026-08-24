---
title: "Your First Transaction in 20 Minutes (Keys, Wallets, and What 'Owning' Means)"
subtitle: "The Radical Redefinition of Ownership in the Blockchain Era"
short_title: "Your First Transaction"
description: "On a blockchain, ownership is not a record about you — it is a key you hold. This chapter guides students through installing a wallet, securing a seed phrase, acquiring SOL, and executing their first real transaction on Solana."
label: ch-01-first-transaction
tags: [wallet, keys, Phantom, Solana, SOL, seed phrase, transaction, Solscan, ownership, custody]
---

# Your First Transaction in 20 Minutes (Keys, Wallets, and What "Owning" Means)

:::{figure} ../images/ch01-explainer-infographic.png
:label: fig-ch01-infographic
:alt: Illustrated explainer infographic showing public/private keys, wallet anatomy, Solana transaction flow, and the concept of self-custody ownership
:width: 80%
:align: center

**Chapter 1 Explainer Infographic:** The complete map of ownership on Solana — from cryptographic key pairs to funded wallets to verified transactions on the block explorer.
:::

You do not own the money in your bank account.

This is not a provocation. It is a legal fact. When you deposit money at a bank, you become an unsecured creditor of that institution. The bank records a liability to you — an obligation to return your funds on demand. That obligation is backed by regulatory requirements, deposit insurance (in the United States, up to \$250,000 through the FDIC), and the bank's solvency. When all of those mechanisms function correctly, the arrangement works. But you are not holding anything. You are holding a *claim* — a legal right to demand value from an institution that, in turn, holds assets of its own.

The same is true of your brokerage account. Of your PayPal balance. Of your airline miles. Of any digital asset held "on your behalf" by any institution. The institution controls the database. The institution decides when you can access it, how much you can withdraw, what identification you must provide, and — in extremis — whether to freeze, suspend, or seize your account.

Tonight — in approximately 20 minutes — you will own something in a fundamentally different sense. You will hold a cryptographic key to which no institution has access. The asset secured by that key cannot be frozen, seized, or denied to you by any bank, any government, or any company — because no bank, government, or company controls the record. The record is on a distributed ledger with tens of thousands of nodes, and only your private key can move what is behind it.

That is what self-custody means. And understanding it, at a technical level, changes how you think about property, about institutions, and about what it means to own something in the digital age.

---

## Why Ownership Is a Solved Problem — and Why It Isn't

In the physical world, ownership is enforced by a combination of possession and legal recognition. You own your car because you possess it (or at least the keys to it) and because a government record — a title — records your name as the owner. If someone steals your car, the combination of physical evidence and legal record provides a mechanism for recovery. If someone falsifies the title record, the legal system provides (in theory) a remedy.

Digital ownership before blockchain was always a weakened form of ownership. You "owned" your music in your iTunes library — until Apple decided to change its licensing terms. You "owned" your virtual items in an online game — until the game was shut down. You "owned" your files in a cloud storage service — until the company was acquired, went bankrupt, or changed its terms. In each case, what you actually owned was a *license* or *permission*, contingent on the continued goodwill and solvency of a corporate platform.

Blockchain ownership is categorically different. On a blockchain, "owning" an asset means that a cryptographic private key you control can authorize the transfer of that asset. No institution intervenes. No permission is required. No account can be frozen. The protocol enforces the property right directly.

:::{figure} ../images/ch01-ownership-comparison.png
:label: fig-ch01-ownership-comparison
:alt: Side-by-side comparison showing traditional custodial ownership (institution as intermediary) versus blockchain self-custody (private key as direct access)
:width: 80%
:align: center

**Two Models of Digital Ownership:** Custodial ownership (left) means trusting an institution to honor your claim. Self-custody (right) means holding the cryptographic key that directly controls the asset — no intermediary required.
:::

The trade-off is real and important, and we will explore it in detail. But let us first understand the mechanism.

---

## Public and Private Keys: The Mailbox Analogy

Every wallet in a blockchain system is built on a **cryptographic key pair** — a public key and a private key. Understanding the relationship between them is the single most important technical concept in this chapter.

Here is the most useful analogy: your public key is like a mailbox on a public street. Anyone can see it. Anyone can put something into it. Your address is publicly known, and there is nothing wrong with that — the openness is the point. Your private key is like the only key to the lock on that mailbox. Only someone with that key can open the mailbox and take out what is inside.

On a blockchain:
- Your **public key** (or the address derived from it) is what you share with others so they can send assets to you. It is safe to publish it, post it online, put it on a business card.
- Your **private key** is what you use to authorize outgoing transactions — to "sign" a message saying "I, the holder of this key, authorize the transfer of X amount of asset Y to address Z." Anyone with your private key can do this. Which means anyone with your private key has full control of everything associated with it.

The mathematics behind this (elliptic curve cryptography) ensures that knowing the public key tells you nothing about the private key — even though the two are mathematically linked. You can derive a public key from a private key, but you cannot reverse the process. This is the one-way property we introduced with hashing in Chapter 0, applied to the ownership layer.

:::{figure} ../images/ch01-public-private-keys.png
:label: fig-ch01-public-private-keys
:alt: Diagram showing the mailbox analogy for public and private keys — public key as open mailbox address, private key as the lock key, with arrows showing send/receive and authorize flows
:width: 80%
:align: center

**Public and Private Keys:** The public key is your address — safe to share openly. The private key is your authorization mechanism — share it with no one, ever. Lose it, and the assets secured by it are gone permanently.
:::

**▶ Watch: Asymmetric Encryption — Simply Explained (4 min)**

<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;max-width:100%;margin:1.5rem 0;">
<iframe src="https://www.youtube.com/embed/AQDCe585Lnc" style="position:absolute;top:0;left:0;width:100%;height:100%;border:0;" allowfullscreen title="YouTube video"></iframe>
</div>

:::{admonition} Where the Analogy Breaks Down
:class: note

The mailbox analogy is excellent for intuition, but it breaks down in one important way: with a physical mailbox, a skilled locksmith might pick the lock. With a properly generated cryptographic private key, there is no such attack. The number of possible private keys is approximately 10⁷⁷ — more than the estimated number of atoms in the observable universe. A brute-force attack on a randomly generated private key would, at the speed of every computer on earth running simultaneously, take longer than the current age of the universe many times over. The security is mathematical, not physical, and that distinction matters.
:::

---

## What a Wallet Actually Is (And Isn't)

The word "wallet" is one of the most persistent misnomers in the blockchain industry. A wallet does not hold your assets. Your assets live on the blockchain — they are entries in the distributed ledger, not files on your device. What a wallet holds — and what it manages — is your **private key**.

Think of a wallet as a key manager and a transaction interface:

1. **Key Storage:** It generates and securely stores your private key (usually never showing it to you directly — you see the seed phrase instead, which we will discuss momentarily).
2. **Address Generation:** It derives your public address from your private key and displays it so you can receive assets.
3. **Transaction Signing:** When you want to send an asset, the wallet uses your private key to cryptographically sign the transaction — proving that you, the key holder, authorized the transfer — without ever transmitting the private key itself.
4. **Blockchain Interface:** It queries the blockchain to show you your current balances and transaction history.

The wallet is a window into the blockchain and a signing mechanism. The assets are always on the chain. This distinction matters practically: if you lose your phone with your wallet app, you have not lost your assets. You have lost your key. If you have your seed phrase backed up (more on that shortly), you can restore your key on a new device and your assets will be there, untouched.

:::{figure} ../images/ch01-wallet-anatomy.png
:label: fig-ch01-wallet-anatomy
:alt: Diagram showing the anatomy of a blockchain wallet — key storage, address generation, transaction signing, and blockchain interface components
:width: 80%
:align: center

**Wallet Anatomy:** A wallet does not contain your assets — they live on the blockchain. The wallet is a key manager: it generates addresses, signs transactions, and serves as your interface to on-chain balances.
:::

**▶ Watch: How Bitcoin Wallets Work (Public & Private Key Explained) (4 min)**

<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;max-width:100%;margin:1.5rem 0;">
<iframe src="https://www.youtube.com/embed/GSTiKjnBaes" style="position:absolute;top:0;left:0;width:100%;height:100%;border:0;" allowfullscreen title="YouTube video"></iframe>
</div>

---

## The Seed Phrase: Twelve Words That Are Everything

When you create a new wallet, the software generates a random **seed phrase** — a sequence of 12 or 24 ordinary English words (from a standard list of 2,048 words) like:

> *chimney horizon bluebird vessel autumn flame quartz ocean marble temple drift signal*

This phrase is a human-readable encoding of your master private key. From this seed phrase, the wallet software can deterministically derive your private key, your public key, and your addresses — every time, forever, on any compatible wallet software.

This means:
- **Your seed phrase IS your private key**, in a form easier for humans to write down accurately
- **Anyone with your seed phrase has full control of all assets in that wallet** — there is no recovery process, no institution to call, no dispute mechanism
- **If you lose your seed phrase AND lose access to your wallet device**, your assets are permanently inaccessible. Not to you — not to anyone. Ever.

:::{admonition} The Custody Paradox
:class: warning

Here is the trade-off in its starkest form: self-custody gives you ownership that no institution can take from you. It also gives you sole responsibility for not losing it. Approximately 20% of all Bitcoin ever mined — currently worth hundreds of billions of dollars — is estimated to be permanently inaccessible because the private keys were lost. This is not a software bug or a system failure. It is the intended behavior of a trustless system.

The question of whether self-custody is appropriate for you, for your users, or for your business is serious and consequential. We will return to it in the Discussion section at the end of this chapter.
:::

### How to Handle a Seed Phrase (Non-Negotiable Rules)

For this course, you will be working with a small amount of real value — approximately \$20 of SOL. Here are the rules for handling your seed phrase:

1. **Write it on paper.** Not digitally. Not in a notes app. Not in a screenshot. Not in a cloud document. Paper.
2. **Write it accurately.** Every word, in exact order, spelled correctly.
3. **Store it somewhere physically secure.** Not next to your laptop. Not photographed on your phone.
4. **Never, ever share it.** Not with your professor. Not with a "support" representative. Not with anyone. Legitimate services never ask for your seed phrase.
5. **Test it.** After writing it down, verify you can read every word clearly. Seed phrases are case-insensitive but spelling-sensitive.

---

## Addresses: Your Public Identifier on Solana

On Solana, addresses are 32-44 character base-58 encoded strings derived from public keys. A Solana address looks like this:

```
7XJvSp3ETmq2zHkAFpMGbXNp9GwKL3DU4UqTLdJG2eBj
```

This address is public. Share it freely with anyone who needs to send you SOL or SPL tokens (Solana's token standard). It is derived mathematically from your public key, which is derived from your private key. The derivation only works in one direction — from private to public to address — never in reverse.

Solana wallets can generate multiple addresses from a single seed phrase (using **derivation paths**). This is useful if you want to organize funds into separate wallets without managing multiple seed phrases. For this course, you will use two addresses: a primary wallet and a backup wallet.

:::{figure} ../images/ch01-address-derivation.png
:label: fig-ch01-address-derivation
:alt: Diagram showing the one-way derivation chain from seed phrase to private key to public key to Solana address, with the key insight that the process cannot be reversed
:width: 80%
:align: center

**Address Derivation:** One seed phrase generates one private key, which generates one public key, which generates a Solana address. The process is deterministic (same inputs always produce the same outputs) and one-directional (you cannot reverse any step).
:::

---

## The Anatomy of a Solana Transaction

When you send SOL from one address to another, what actually happens? Let us walk through the technical anatomy of a Solana transaction — not as an abstraction, but as a sequence of real events you can observe on the block explorer.

**Step 1: Instruction construction.** Your wallet software assembles a transaction object. For a simple SOL transfer, this contains: the sender's address, the recipient's address, the amount in lamports (a lamport is 0.000000001 SOL — named after computer scientist Leslie Lamport), and any additional instructions (like token program calls for SPL token transfers).

**Step 2: Fee estimation.** Every Solana transaction requires a transaction fee, paid in SOL. Solana's fees are among the lowest in the blockchain industry — typically 0.000005 SOL, or about \$0.0008 at current prices. This makes Solana economically viable for applications that would be cost-prohibitive on networks like Ethereum, where transaction fees can range from \$5 to \$200 depending on network congestion.

**Step 3: Recent blockhash.** The wallet fetches the hash of a recent block from the network. This hash is embedded in the transaction and serves two purposes: it proves the transaction was created recently (preventing replay attacks) and it links the transaction to the current state of the blockchain.

**Step 4: Signing.** Your wallet uses your private key to create a cryptographic signature over the entire transaction object. This signature mathematically proves that the holder of the private key corresponding to the sender's address authorized this specific transaction. The signature is attached to the transaction.

**Step 5: Broadcast.** The signed transaction is broadcast to the Solana network — specifically to a validator node, which then propagates it to other validators.

**Step 6: Consensus and confirmation.** Solana validators process the transaction through their consensus mechanism (Tower BFT, which we will not detail here). Once a supermajority of validators have confirmed the transaction, it is finalized. On Solana, finality typically arrives within 400–800 milliseconds. This is not a rough estimate — it is a system architecture achievement that makes Solana categorically different from slower networks.

**Step 7: Ledger update.** The transaction is included in a block, which is added to the chain. The ledger state updates: the sender's balance decreases, the recipient's balance increases. Every node on the network now reflects the new state.

:::{figure} ../images/ch01-transaction-lifecycle.png
:label: fig-ch01-transaction-lifecycle
:alt: Flowchart diagram showing all seven steps of a Solana transaction lifecycle from instruction construction through signing, broadcast, consensus, and final ledger update
:width: 80%
:align: center

**Solana Transaction Lifecycle:** From the moment you click "Send" to finality on the ledger — seven steps, typically completed in under one second.
:::

---

## Why Solana? The Economics and Architecture of Speed

The blockchain landscape in 2026 includes dozens of active Layer-1 networks and hundreds of Layer-2 solutions. Understanding why this course focuses on Solana requires a brief comparative analysis.

### The Ethereum Challenge

Ethereum is the most widely used programmable blockchain, with the largest developer ecosystem and the longest track record. It introduced smart contracts, DeFi, and NFTs to the mainstream. For these reasons, it deserves respect.

But Ethereum has two characteristics that make it impractical for many real-world business applications:

**Cost:** Ethereum's gas fees — the cost of executing transactions and smart contract operations — are priced in ETH and fluctuate based on network congestion. During periods of high activity, simple token transfers have cost \$50–\$200 per transaction. For a business trying to serve customers with sub-\$10 transaction values, this is a fundamental economic barrier.

**Speed:** Ethereum's base layer processes approximately 15–30 transactions per second, with finality taking 12–15 minutes. (Ethereum's Layer-2 solutions improve this significantly, but add complexity for developers and users.) For applications requiring real-time settlement — point-of-sale, gaming, supply chain tracking — this latency is prohibitive.

### The Solana Architecture

Solana was designed from the ground up to solve these problems. Its key architectural innovations:

**Proof of History (PoH):** Solana's most novel contribution is a cryptographic clock — a verifiable delay function that creates a historical record proving that events occurred at a specific point in time. This allows validators to process transactions in parallel without needing to communicate with each other to establish ordering, which is the key bottleneck in traditional blockchain architectures.

**Tower BFT:** Solana's consensus mechanism builds on PBFT (Practical Byzantine Fault Tolerance) to leverage the PoH clock. Validators can vote on proposed blocks much faster because the ordering is pre-established.

**Gulf Stream:** Solana's mempool-less transaction forwarding protocol. Rather than holding pending transactions in a pool, transactions are forwarded to the next expected validator before the current block is even finalized, reducing confirmation times.

**Turbine:** Solana's block propagation protocol, inspired by BitTorrent, that breaks blocks into small packets for efficient transmission across the network even as block sizes grow.

The result of these architectural choices:

| Metric | Bitcoin | Ethereum | Solana |
|--------|---------|----------|--------|
| Throughput (TPS) | 7 | 15-30 | 65,000+ |
| Block time | ~10 min | ~12 sec | ~400 ms |
| Avg. transaction fee | ~\$1-5 | ~\$1-50 | ~\$0.0008 |
| Finality | ~60 min | ~12-15 min | ~400-800 ms |
| Energy per tx | ~700 kWh | ~0.03 kWh | <0.001 kWh |

:::{figure} ../images/ch01-blockchain-comparison.png
:label: fig-ch01-blockchain-comparison
:alt: Visual comparison chart of Bitcoin, Ethereum, and Solana across five metrics: throughput, block time, transaction fees, finality, and energy consumption per transaction
:width: 80%
:align: center

**Blockchain Performance Comparison:** Solana's architectural innovations — Proof of History, Tower BFT, Gulf Stream, and Turbine — produce performance characteristics that make it economically viable for a much wider range of business applications.
:::

### Solana's Trade-offs

No architecture is without trade-offs. Solana's speed and low fees come with costs:

**Centralization pressure:** Running a Solana validator requires substantial hardware (128GB RAM, multiple high-performance NVMe drives, a 12-core CPU minimum). This creates economic barriers that tend toward a smaller, more capital-intensive validator set compared to networks with lower hardware requirements.

**Outage history:** Solana has experienced several network-wide outages (most notably in September 2021, January 2022, and May 2022) — instances where the network halted and required validators to coordinate a restart. These events, while resolved, highlight that Solana's design makes different trade-offs than older, more conservative networks.

**Ecosystem maturity:** Solana's developer tooling, documentation, and ecosystem are mature but younger than Ethereum's. Some developer resources remain less polished than their Ethereum equivalents.

For the purposes of this course — building real token economies with real business models — Solana's speed, low fees, and rich ecosystem of DeFi protocols, DEXes, and developer tools make it the most practical choice. The \$20 of SOL you are about to acquire will last you the entire course; the same budget on Ethereum would be consumed by fees in a single session.

---

## Reading a Block Explorer: Your Window Into the Chain

A **block explorer** is a website that lets you read the blockchain — every block, every transaction, every address balance — in a human-readable format. It is the equivalent of reading the village notebook. Everything is public, searchable, and verifiable.

For Solana, the primary block explorer is **Solscan** (solscan.io). The Solana Foundation also provides its own explorer at **explorer.solana.com**.

When you execute your first transaction in the Activity section, you will look up your transaction on Solscan and annotate what you see. Let us preview what a transaction page shows:

**Transaction Signature:** A 87-88 character base-58 string that uniquely identifies the transaction. This is the transaction's hash — its cryptographic fingerprint. If you share this with anyone, they can look up the complete transaction history.

**Status:** Confirmed ✓ (or Failed ✗). Unlike a bank transfer that might "process for 3-5 business days," a Solana transaction either succeeds or fails within seconds — and you can see the result immediately.

**Block:** Which block number contains this transaction. The block also shows the timestamp — the exact moment (to the millisecond) when the transaction was finalized.

**From and To:** The sending and receiving addresses. Because addresses are pseudonymous (not explicitly linked to real-world identities), these addresses might be yours, might be an exchange's, might be a smart contract. But the addresses are permanent and public.

**Amount:** How many lamports (and their SOL equivalent) were transferred.

**Fee:** The transaction fee paid to validators. For SOL transfers, typically 5,000 lamports (0.000005 SOL).

**Program:** Which Solana program (smart contract) processed the transaction. For simple SOL transfers, this is the System Program. For token transfers, it is the SPL Token Program.

:::{figure} ../images/ch01-solscan-annotated.png
:label: fig-ch01-solscan-annotated
:alt: Annotated screenshot of a Solana transaction page on Solscan, with callouts explaining the transaction signature, status, block, from/to addresses, amount, fee, and program fields
:width: 80%
:align: center

**Solscan Transaction Anatomy:** Every transaction on Solana is public and permanently recorded. The block explorer is your audit trail — show this to any counterparty to prove a payment was made.
:::

---

## Custody Models: Self-Custody vs. Custodial Wallets

Before you proceed to the Activity, it is important to understand that the self-custody model you are about to practice is not the only model — and for many use cases, it is not the right model.

### Self-Custody (Non-Custodial)

In the self-custody model, you hold your private key. No institution has access. The upside is absolute ownership. The downside is absolute responsibility. If you lose your seed phrase, your assets are permanently inaccessible. If someone steals your seed phrase, your assets are permanently lost. There is no customer support, no dispute resolution, no recovery.

Self-custody is appropriate for:
- Technically sophisticated users who understand the risks
- Holdings large enough to justify hardware wallet investment (more on hardware wallets in a moment)
- Use cases where censorship resistance is a core requirement (activists in authoritarian regimes, for example)
- Development and testing

### Custodial Wallets

In the custodial model, a third party (a crypto exchange like Coinbase, Kraken, or Binance) holds your private key on your behalf. You log into their platform with a username and password. They maintain the key and execute transactions on your instruction.

The upside is familiarity and recovery options — you can reset a forgotten password. The downside is that you are back in the traditional ownership model: you own a *claim* against the custodian, not the assets themselves. Exchanges can be hacked (Mt. Gox, 2014: \$460 million lost; FTX, 2022: \$8 billion customer funds lost in bankruptcy). Exchanges can freeze accounts. Exchanges can fail.

The industry wisdom, which has become a cultural maxim: **"Not your keys, not your coins."**

### Hardware Wallets

For serious asset holdings, self-custody users typically use a **hardware wallet** — a physical device (Ledger, Trezor) that stores the private key in a secure enclave, never exposing it to internet-connected devices. When signing a transaction, you physically confirm on the device. The private key never leaves the hardware. This is the gold standard for self-custody security, and the recommended approach for holdings above ~\$1,000.

:::{figure} ../images/ch01-custody-spectrum.png
:label: fig-ch01-custody-spectrum
:alt: Diagram showing the custody spectrum from fully custodial (exchange wallet) through software self-custody (Phantom) to hardware self-custody (Ledger), with security and convenience trade-offs labeled
:width: 80%
:align: center

**The Custody Spectrum:** Security and convenience trade off directly. For this course, a software wallet (Phantom) with proper seed phrase security is appropriate for the small amounts involved.
:::

---

## Phantom: Solana's Primary Wallet

**Phantom** (phantom.app) is the most widely used Solana wallet, available as a browser extension (Chrome, Firefox, Edge, Brave) and as a mobile app (iOS, Android). It is free, open-source, non-custodial, and integrates with virtually every Solana DeFi protocol, DEX, and NFT marketplace you will encounter in this course.

Phantom launched in 2021 and has grown to over 3 million active users. It has been audited by multiple security firms, is maintained by a well-funded company, and has a track record of responsible security disclosures. For a software wallet used with small amounts and as a learning tool, it is the appropriate choice for this course.

:::{admonition} Security Note
:class: warning

Always download wallet software directly from the official source — phantom.app — not through third-party links, ads, or Discord messages. Phishing attacks that direct users to counterfeit wallet websites are among the most common crypto theft vectors. Check the URL carefully before entering any sensitive information.
:::

---

## 🎯 Activity: Your First Solana Transaction

This activity has five steps. Set aside 20-30 minutes with your phone and computer. You will need approximately \$25 in US dollars to complete it (which you will retain as SOL and a learning asset).

### Step 1: Create Your Primary Wallet (5 minutes)

1. Go to **phantom.app** on your desktop browser
2. Click "Download" and install the browser extension for your browser
3. Open the extension and click "Create a new wallet"
4. Phantom will display your 12-word seed phrase. **STOP HERE.**
   - Get a piece of paper and a pen
   - Write down every word, in order, accurately
   - Double-check your spelling against what Phantom shows
   - Store this paper somewhere physically secure — NOT at your desk
5. Confirm the seed phrase by selecting the words in order when prompted
6. Set a wallet password (this protects the extension on your device — it is NOT your seed phrase)
7. Note your wallet address (copy it and paste it somewhere you can reference)

**Your primary wallet is ready.**

### Step 2: Create Your Backup Wallet (3 minutes)

You will send SOL *from* your primary wallet *to* this backup wallet. Having two wallets reinforces the mechanics.

1. In Phantom, click your account icon (top center of the extension)
2. Click "Add / Connect Wallet"
3. Select "Create new wallet"
4. Write down this second seed phrase on a *different* piece of paper
5. Note the backup wallet's address

### Step 3: Acquire SOL (5-10 minutes)

The easiest path for US-based students:

**Option A: Buy directly in Phantom (US debit/credit card)**
1. In Phantom, click "Buy"
2. Select "Solana (SOL)"
3. Purchase approximately \$25 worth of SOL
4. Phantom routes through MoonPay or Coinbase Pay — you will need to complete a brief identity verification
5. SOL typically arrives within 5–15 minutes

**Option B: Via Coinbase**
1. Create or log into your Coinbase account (coinbase.com)
2. Buy \$25 of SOL
3. Send it to your Phantom primary wallet address
4. Note: Coinbase sends SOL on the Solana network; confirm "Solana" network is selected before withdrawing

**Option C: Via a peer (if a classmate already has SOL)**
1. Give them your primary wallet address
2. Have them send you 0.1 SOL
3. Verify receipt on Solscan

Wait until your SOL has arrived in your primary wallet and is visible in Phantom before proceeding.

### Step 4: Send SOL Between Your Wallets (3 minutes)

1. In Phantom (showing your primary wallet), click "Send"
2. Paste your backup wallet address in the recipient field
3. Enter an amount: 0.01 SOL (approximately \$1.50 at most price levels — a trivial amount that will demonstrate the mechanics)
4. Review the transaction details — note the fee shown (should be <\$0.01)
5. Click "Send"
6. Phantom will show a confirmation screen — click "Confirm"
7. Watch the transaction status. It should change from "Processing" to "Confirmed" within 1-2 seconds

### Step 5: Find Your Transaction on Solscan (5 minutes)

1. Open Solscan.io in your browser
2. In the search bar, paste your primary wallet address
3. You will see your account page showing your SOL balance, token holdings, and transaction history
4. Click on the most recent transaction (the 0.01 SOL transfer you just made)
5. On the transaction page, take a screenshot
6. Annotate the screenshot (you can use Preview, Paint, or any annotation tool) to label:
   - The transaction signature
   - The "From" address (your primary wallet)
   - The "To" address (your backup wallet)
   - The amount transferred
   - The transaction fee
   - The block number and timestamp
   - The "Confirmations" field (should say "Finalized")

**Save this annotated screenshot.** It is your deliverable for this chapter.

:::{figure} ../images/ch01-activity-workflow.png
:label: fig-ch01-activity-workflow
:alt: Step-by-step visual guide showing the five activity steps: create primary wallet, create backup wallet, acquire SOL, send between wallets, and verify on Solscan
:width: 80%
:align: center

**Activity Workflow:** Five steps from wallet creation to verified on-chain transaction. Each step builds on the previous, giving you direct experience with the full self-custody workflow.
:::

---

## Advanced: Reading Your Full Account on Solscan

Once you have completed the basic activity, take an additional 5 minutes to explore what Solscan shows about your wallet:

**Portfolio tab:** Shows all tokens in your wallet, not just SOL. Right now this is just SOL, but by Chapter 3, this will include your own token.

**Transactions tab:** Your complete transaction history — every send, receive, and program interaction, with timestamps and signatures. This is your permanent, public, irrevocable record. Note that transactions cannot be deleted. They cannot be redacted. Whatever you put on the blockchain is there forever.

**DeFi Activities tab:** Once you start interacting with DeFi protocols in Chapter 5, this tab will show liquidity positions, staking rewards, and swap histories.

**NFT tab:** Your NFT holdings — relevant for Chapter 9.

Take a moment to appreciate what you are looking at: a complete, publicly auditable record of every economic action associated with this address, available to anyone in the world, with no institution in the middle. This is what radical transparency looks like. It is both powerful and, in some contexts, concerning — which is part of why the discussion question at the end of this chapter matters.

---

## The Bigger Picture: What Changes When Ownership Is a Key

We opened this chapter with the observation that you do not own the money in your bank account — you hold a claim. Let us return to that observation now, with the mechanics of self-custody fully in hand, and examine what actually changes.

**For individuals in stable, regulated economies:** The practical difference between custodial bank ownership and blockchain self-custody is primarily philosophical for most everyday transactions. Your FDIC-insured bank deposits are, for practical purposes, safe. The inconveniences (transfer times, fees, account restrictions) are real but manageable. Self-custody adds responsibility and risk; the sovereignty it provides is valuable to some users and unimportant to others.

**For individuals in unstable or authoritarian economies:** The difference is concrete and urgent. When inflation erodes a currency by 50% per year (as in Venezuela and Argentina in recent years), holding savings in a dollar-pegged stable coin on Solana is a genuine hedge against monetary policy failure. When a government freezes political dissidents' bank accounts (as Canada briefly did with trucker protest supporters in 2022, and as authoritarian regimes do routinely), self-custody becomes the only form of economic autonomy available. These are not edge cases. They are the lived experience of hundreds of millions of people.

**For businesses:** Self-custody in a business context introduces questions of governance and liability. If the private key is held by one employee and that employee leaves, is killed in an accident, or is coerced, the company's assets could be permanently inaccessible or stolen. Business blockchain deployments typically use **multi-signature** (multisig) wallets — where transactions require M of N keyholders to sign (for example, 3 of 5 partners must approve). We will design a multisig treasury in Chapter 11.

:::{figure} ../images/ch01-global-use-cases.png
:label: fig-ch01-global-use-cases
:alt: World map with call-out boxes showing real-world use cases of self-custody wallets in Venezuela, Argentina, Ukraine, and among the globally unbanked population
:width: 80%
:align: center

**Self-Custody in the Real World:** Blockchain self-custody is not just a technical preference — for hundreds of millions of people in economies with monetary instability or authoritarian restrictions, it is a meaningful form of financial sovereignty.
:::

---

## The Revolution You Just Participated In

You have just done something that was technically impossible for most of human history, and impossible for most adults even 15 years ago: you have established unmediated digital ownership.

The private keys sitting in your Phantom wallet — secured by the seed phrases on your two pieces of paper — represent a form of ownership that does not require anyone's permission, does not depend on any institution's solvency, and cannot be frozen, restricted, or confiscated without your cooperation. This is not a minor feature. It is a categorical change in the nature of digital property.

The global addressable market for financial services that blockchains can disrupt runs into the trillions of dollars annually. The remittance market alone — international money transfers by migrant workers back to their home countries — generates \$45 billion in fees per year. A Solana transaction that accomplishes the same transfer in 400 milliseconds for \$0.0008 in fees does not disrupt that market incrementally. It makes the existing fee structure indefensible.

Cross-border business payments — currently routed through Swift with 2-5 day settlement and fees of 2-4% — are experiencing the same compression. Payments companies like Circle (issuer of the USDC stablecoin) and Stripe have integrated Solana-based settlement precisely because the economics are too compelling to ignore at scale.

The 20 minutes you spent in this chapter's activity are the foundation for understanding all of it.

---

## 🚀 Walk Away With

- ✅ **Primary Phantom wallet** with seed phrase secured on paper
- ✅ **Backup Phantom wallet** with seed phrase secured on separate paper
- ✅ **Funded primary wallet** (approximately \$20 of SOL)
- ✅ **Annotated transaction screenshot** from Solscan, showing all transaction fields labeled
- ✅ **Conceptual understanding** of the difference between custodial and non-custodial ownership, with the ability to explain it using the mailbox analogy

Bring your annotated Solscan screenshot to the next class. We will use your wallet addresses in Chapter 2 when we design the first version of your token.

---

## 💬 Discussion Question

:::{admonition} Discussion Prompt
:class: seealso

Holding your own keys means no one can freeze your funds — and no one can recover them if you lose the phrase.

Is that trade worth it for most people? For a business? Who should be allowed to make that choice for others?

Consider:
- **The consumer protection question:** Traditional banking comes with fraud protection, dispute resolution, and deposit insurance. These are not incidental features — they are why most people trust banks with their savings. A system that eliminates the ability to freeze, reverse, or recover funds is also a system without these protections. Should financial systems without consumer protections be legal? Should they be accessible to retail investors without financial literacy requirements?

- **The governance question:** Several countries have considered or implemented requirements that custodial crypto wallets implement Know Your Customer (KYC) and Anti-Money Laundering (AML) compliance. The EU's MiCA regulation (Markets in Crypto-Assets) imposes regulatory requirements on crypto service providers. Do these regulations, which apply to custodians but not to self-custody, make sense? Who benefits and who is disadvantaged?

- **The power asymmetry question:** When a government or corporation decides to freeze accounts, they typically target the politically or economically marginal. Who, concretely, would benefit most from uncensorable ownership? Who might be harmed by it?

- **The business liability question:** A company that loses its private key loses its assets, permanently, with no legal recourse. Is that an acceptable business risk? How does it change corporate governance requirements?

**Your response should:**
- Be at least 250 words
- Take a clear position — not "it depends" but an actual argument
- Include at least one citation from a credible source (academic paper, law review article, news outlet, industry report)
- Respond to at least TWO peers with substantive engagement — challenge or extend their reasoning with specific evidence or alternative analysis

**Note:** This is an individual online assignment.
:::

---

## Glossary

```{glossary}
Private Key
  A randomly generated 256-bit secret number that authorizes transactions from a blockchain address. Whoever holds the private key controls all assets at the corresponding address. Must never be shared.

Public Key
  Derived mathematically from a private key, used to generate a blockchain address and verify digital signatures. Safe to share publicly.

Seed Phrase
  A human-readable encoding of a private key — typically 12 or 24 ordinary English words. Can be used to restore a wallet on any compatible software. Equivalent in security sensitivity to the private key itself.

Wallet
  Software (or hardware) that stores private keys, generates addresses, and interfaces with the blockchain to sign transactions and display balances. Does not "hold" assets — those live on the blockchain.

Phantom
  The primary non-custodial browser extension and mobile wallet for Solana. Free, open-source, and compatible with virtually all Solana DeFi and NFT protocols.

Address
  A public identifier on the blockchain, derived from the public key. Used to receive assets. On Solana, typically 32-44 characters in base-58 encoding.

Lamport
  The smallest unit of SOL — 0.000000001 SOL. Named after computer scientist Leslie Lamport. Transaction fees on Solana are typically 5,000 lamports (0.000005 SOL).

Self-Custody
  The practice of holding your own private keys without relying on a third-party custodian. Provides full asset sovereignty; requires personal responsibility for key security.

Custodial Wallet
  A wallet in which a third party (such as an exchange) holds the private keys on your behalf. Offers recovery options but reintroduces institutional trust requirements.

Hardware Wallet
  A physical device that stores private keys in a secure enclave, never exposing them to internet-connected computers. Examples include Ledger and Trezor. Recommended for significant asset holdings.

Multisig (Multi-Signature)
  A wallet configuration requiring M of N private keys to authorize a transaction (e.g., 3 of 5). Reduces single-point-of-failure risk for businesses and DAOs.

Non-Custodial
  A wallet or protocol in which the user holds their own private keys — no third party has custody or control of the assets.

Block Explorer
  A website providing public read access to blockchain data — blocks, transactions, addresses, and token balances. Solscan.io is the primary Solana block explorer.

Solscan
  The primary block explorer for Solana (solscan.io). Displays all account balances, transaction history, token holdings, DeFi positions, and NFT holdings for any Solana address.

Transaction Signature
  The cryptographic hash uniquely identifying a specific transaction on the blockchain. Can be used to look up any transaction permanently on a block explorer.

Finality
  The state at which a blockchain transaction is irreversible — confirmed by enough of the network that reversal would require an overwhelming majority of validator collusion. On Solana, finality arrives in approximately 400-800 milliseconds.

SPL Token
  The Solana Program Library token standard — the equivalent of Ethereum's ERC-20. All fungible tokens on Solana (including stablecoins like USDC) are SPL tokens. We will create one in Chapter 3.

Proof of History (PoH)
  Solana's cryptographic clock — a verifiable delay function that establishes a historical record of events before they are confirmed by consensus, enabling Solana's high throughput.

Gas Fee
  The fee paid on Ethereum for transaction execution, priced in Gwei (a fraction of ETH). Variable and can be extremely high during network congestion. Contrast with Solana's fixed, extremely low fees.

KYC (Know Your Customer)
  Identity verification requirements imposed on financial service providers by regulators, requiring them to confirm the identity of their customers. Applies to custodial crypto services under most jurisdictions' regulations.

MiCA (Markets in Crypto-Assets)
  The European Union's comprehensive regulatory framework for cryptocurrency, effective 2024-2025. Imposes licensing, disclosure, and conduct requirements on crypto service providers operating in the EU.
```
