---
title: "Distribute It — Airdrops, Vesting, and Team Allocations"
subtitle: "Every Mechanism Encodes a Promise"
short_title: "Distribute It"
description: "A currency held by one person is not a currency. This chapter covers airdrops as customer acquisition, vesting contracts, streaming payments, Sybil defense, and batch transactions — the mechanics that turn a token into an economy."
label: ch-06-distribution
tags: [airdrop, vesting, streaming, Sybil, batch transactions, Streamflow, Solana, token distribution, allocation]
---

# Distribute It — Airdrops, Vesting, and Team Allocations

:::{figure} ../images/ch06-explainer-infographic.png
:label: fig-ch06-infographic
:alt: Illustrated explainer infographic showing the full distribution ecosystem — airdrops, vesting schedules, streaming payments, Sybil defense, and allocation pie chart for a token economy
:width: 80%
:align: center

**Chapter 6 Explainer Infographic:** The complete map of token distribution — from public airdrops and Sybil defense to locked vesting streams and team allocations. Every arrow encodes a promise to a different stakeholder.
:::

A currency held by one person is not a currency. It is a collection.

This distinction matters more than most founders realize when they launch a token. The moment you mint a million units of something and hold them in a single wallet, you have not built an economy. You have built a spreadsheet entry. The economy begins when those units are in other people's hands — when holders can trade them, stake them, use them to vote, or spend them on your platform's services. Distribution is not a marketing exercise layered on top of the technical work. Distribution *is* the technical work, and the pattern of who gets it, when, and under what conditions determines whether your economy ever trusts itself.

This chapter covers the full mechanics of distribution on Solana: airdrops as customer acquisition, vesting contracts that replace legal agreements with code, streaming payments that pay contributors by the second, Sybil attacks that undermine fairness, batch transactions that make mass distribution cheap, and the signals that markets read from allocation tables. By the end, you will have put tokens into other people's wallets, set up a live vesting stream, and calculated exactly what each new holder cost you.

---

## Airdrops as Customer Acquisition: Cost Per Holder

In traditional marketing, companies spend money to acquire customers. They buy ads, run promotions, offer discounts, sponsor events. The core metric is **cost per acquisition (CPA)** — how much does it cost to get one person to take the desired action?

An airdrop is customer acquisition with an equity twist. Instead of giving away a discount on your product, you give away fractional ownership of your protocol. The recipient becomes not just a customer but a stakeholder. Their incentive is now aligned with your success: if the token appreciates, they benefit. If the protocol grows, the token's utility increases.

This reframes the accounting entirely. When a traditional company runs a promotion, the cost is pure expense — money out, with no long-term claim on the company created. When a protocol airdrops tokens, the cost is dilution: the protocol's total token supply is now spread across more holders, each of whom holds a tiny claim on the ecosystem's future value. If the ecosystem grows, the dilution was worth it. If it doesn't, the airdrop simply distributed nothing into nothing.

:::{figure} ../images/ch06-airdrop-economics.png
:label: fig-ch06-airdrop-economics
:alt: Infographic comparing traditional customer acquisition cost versus airdrop cost-per-holder analysis, with break-even calculation and holder retention curve
:width: 80%
:align: center

**Airdrop Economics:** Traditional CPA is a pure cost. Airdrop cost-per-holder includes the opportunity cost of dilution but gains stakeholder alignment that marketing spend cannot buy.
:::

The calculation is straightforward once you frame it correctly:

```
Cost Per Holder = (Token FMV × Tokens Distributed) + Transaction Fees
                 ─────────────────────────────────────────────────────
                         Number of Unique Wallets Receiving Tokens
```

Where **FMV** is the fair market value of the token at the time of distribution. If you distribute 100 tokens to 500 wallets, and each token is worth \$0.10, you have spent \$10 per wallet in diluted value — plus a trivial amount in Solana transaction fees (more on that in a moment).

The real question is not "did the airdrop cost money?" but "did we get \$10 worth of holder value from each recipient?" Holder value includes: wallet activation (the person is now using your product), trading volume generated (airdrops stimulate secondary market activity), social amplification (holders tell their networks), governance participation (if your token includes voting rights), and retention over time.

The uncomfortable truth about airdrops is that most tokens distributed for free are sold immediately. Studies of major airdrop campaigns show that 40–70% of airdrop recipients sell within the first 48 hours. This is rational behavior — free money should be harvested. The projects that convert airdrop recipients into long-term holders are the ones that gave tokens to people who were already engaged with the protocol, not random wallets from a snapshot.

:::{figure} ../images/ch06-holder-retention.png
:label: fig-ch06-holder-retention
:alt: Holder retention curve chart comparing engaged airdrop recipients (slow decay) versus random wallet recipients (rapid sell-off in first 48 hours)
:width: 80%
:align: center

**Holder Retention by Recipient Type:** Wallets with pre-existing on-chain activity retain tokens at dramatically higher rates than random wallets. The 48-hour sell-off is most severe for undifferentiated distributions.
:::

:::{admonition} The Engagement Filter
:class: tip

The single most effective airdrop strategy is to reward existing behavior, not to buy new attention. Uniswap's 2020 airdrop of UNI tokens to every wallet that had previously used the protocol produced holders who understood what they owned. Protocols that airdrop to random wallets based on simply holding ETH produce sellers.

Filter your recipient list by on-chain activity: number of transactions, protocol interactions, time since wallet creation. The more engaged the wallet, the lower the sell rate and the higher the long-term holder value.
:::

---

:::{figure} ../images/ch06-distribution-mechanisms.png
:label: fig-ch06-distribution-mechanisms
:alt: Overview diagram of three token distribution mechanisms: airdrop, vesting, and streaming payments with labeled properties and use cases
:width: 80%
:align: center

**Three Distribution Primitives:** Airdrops (broad, immediate), vesting contracts (time-locked, targeted), and streaming payments (continuous, real-time). Each serves a different stakeholder and encodes a different promise.
:::

## Vesting Contracts: Code Replaces a Legal Agreement

When a startup raises venture capital, the term sheet includes vesting schedules. A co-founder's equity might vest over four years with a one-year cliff — meaning they earn nothing in the first year, then the full first year's allocation vests at month 12, and the remaining three years vest monthly. If they leave in month 11, they get nothing. This arrangement is enforced by a legal agreement, by the company's capitalization table, and ultimately by courts.

In a token ecosystem, a **vesting contract** replaces all of that with code. The contract holds tokens on behalf of a beneficiary and releases them according to a predefined schedule. No lawyers required. No capitalization table. No court. The blockchain enforces the agreement automatically and transparently.

Here is why this matters beyond administrative convenience: a smart contract vesting schedule is **publicly verifiable**. Any market participant can read the contract and see exactly when team tokens unlock. This transparency is enormously valuable. When investors, users, and trading platforms can verify that the founding team's tokens are locked for 18 months with a two-year linear release after that, they can price that information into their decisions. When team tokens are unverified and unlocked, the market prices in the risk that founders will dump.

:::{figure} ../images/ch06-vesting-schedule.png
:label: fig-ch06-vesting-schedule
:alt: Timeline diagram showing a vesting schedule with 12-month cliff, linear monthly release over 24 months, and total allocation breakdown for team, investors, and advisors
:width: 80%
:align: center

**Vesting Timeline:** A 12-month cliff followed by 24-month linear vesting for a co-founder allocation. The contract holds the tokens; neither the recipient nor the issuer can accelerate the release.
:::

**Streamflow** is the leading vesting and streaming protocol on Solana. It provides a no-code interface for creating time-locked token releases and streaming payments. The typical workflow for setting up a team vesting stream:

1. Connect your wallet to [app.streamflow.finance](https://app.streamflow.finance)
2. Select the token you want to vest
3. Enter the recipient's wallet address
4. Set the cliff duration (the period before any tokens unlock)
5. Set the total vesting duration
6. Choose the release frequency (monthly, weekly, or by-the-second)
7. Enter the total amount to vest
8. Confirm the transaction — the tokens are locked in the Streamflow program

The contract is live. You can share the stream URL with your co-founder, with investors, with anyone — they can verify the schedule on-chain at any time. Streamflow also supports cancellation (with proper governance) and modification, but the default behavior is immutable: the tokens release on schedule regardless of anyone's wishes.

:::{admonition} The Legal Dimension
:class: warning

Vesting contracts on-chain are technically enforceable by code, but they do not replace all legal agreements. In most jurisdictions, you still need a written agreement that defines employment terms, IP ownership, and what happens in dispute scenarios. The vesting contract enforces the *schedule*; the legal agreement defines the *context*. Use both.
:::

### Why the Cliff Exists

A vesting cliff is not punitive. It is a selection mechanism. A co-founder who is not committed to the project will leave before the cliff vests — and they should leave without taking a significant allocation. The cliff aligns long-term commitment with long-term rewards. On Solana's SPL token standard, the cliff is simply a parameter in the vesting contract: no tokens can be withdrawn before the cliff timestamp, regardless of any other condition.

---

## Streaming Payments: Paying by the Second

Linear vesting (once a month, once a week) is a step forward from manual payment. But Streamflow and similar protocols support something even more granular: **streaming payments**, where a contributor is paid by the second, in real time, as they work.

Imagine a freelance developer contracted to build your protocol's interface. Instead of paying them net-30 invoices, you open a Streamflow stream: \$5,000 of tokens, streaming over 30 days. At any moment, the developer can withdraw whatever has streamed to their wallet. The first hour of the stream earns them a small fraction of the total. By day 15, they have received half. On day 30, the stream completes.

:::{figure} ../images/ch06-streaming-payments.png
:label: fig-ch06-streaming-payments
:alt: Visual diagram of a streaming payment contract showing real-time token flow from payer to payee, with a clawback window, withdrawal events, and balance at any given timestamp
:width: 80%
:align: center

**Streaming Payments:** Tokens flow continuously from the payer's locked contract to the payee's available balance. The payee can withdraw at any time; unused funds can be recovered if the engagement ends early.
:::

This changes the accountability dynamic profoundly. In a traditional contract, a freelancer is owed payment regardless of ongoing performance (within the contract terms). In a streaming arrangement:

- **The payer** retains a clawback right: if the developer stops delivering, the stream can be cancelled and remaining tokens returned
- **The payee** has immediate liquidity: they are not waiting 30 days to access earned compensation
- **Both parties** have real-time visibility: the stream balance is on-chain, not in an invoice system

For DAOs and decentralized teams where contributors are pseudonymous and legal enforcement is impractical, streaming payments are not just convenient — they are sometimes the *only* enforcement mechanism available.

:::{note}
Streaming payments on Solana are cheap because Solana's fee structure makes frequent micro-transactions viable. On Ethereum, a payment stream would require constant on-chain state updates, each costing gas. On Solana, the program architecture allows streaming to be settled efficiently with minimal fee overhead.
:::

---

## Sybil Attacks: Why "One Wallet, One Airdrop" Fails

Here is the problem with airdrops: anyone can create a new wallet in 30 seconds. If your airdrop gives 100 tokens to every wallet that signs up, a motivated attacker will create 10,000 wallets and claim 1,000,000 tokens — then sell them all, dumping the price and extracting value from everyone who played by the rules.

This is a **Sybil attack** — named after the 1973 book about a patient with multiple personality disorder. In distributed systems, a Sybil attack is when a single malicious actor controls many fake identities to manipulate a system designed around the assumption of unique participants.

:::{figure} ../images/ch06-sybil-attack.png
:label: fig-ch06-sybil-attack
:alt: Diagram illustrating a Sybil attack where one attacker controls dozens of fake wallets to claim multiple airdrop allocations, versus legitimate one-wallet-per-person recipients
:width: 80%
:align: center

**Sybil Attacks in Airdrop Campaigns:** A single attacker controlling 1,000 fake wallets can drain an airdrop that was designed to reach 1,000 unique community members. Defense requires proof of unique identity or on-chain reputation.
:::

Defending against Sybil attacks requires evidence that a wallet represents a unique, legitimate participant. Projects use several approaches:

**On-chain activity requirements.** Instead of giving tokens to any wallet that claims them, you snapshot wallets that have performed specific on-chain activities — transacted a minimum number of times, interacted with specific protocols, held assets above a minimum value for a minimum period. Creating 1,000 fake wallets with genuine on-chain history is expensive and difficult.

**Social verification.** Linking wallets to social accounts (Twitter, GitHub, Discord) does not prove uniqueness, but it raises the cost of farming. Maintaining 1,000 fake Twitter accounts is much harder than creating 1,000 wallets.

**Proof of humanity systems.** Protocols like Proof of Humanity, Worldcoin (World ID), and BrightID attempt to create on-chain attestations of unique human identity. Integrating these into an airdrop claim flow creates a strong Sybil barrier at the cost of friction for legitimate participants.

**Quadratic distribution.** Instead of giving equal amounts to each qualifying wallet, use a quadratic formula that gives diminishing returns to wallets with more activity. A whale wallet with 100x the activity gets only 10x the airdrop (square root of 100). This reduces the incentive for Sybil farming without eliminating it.

:::{admonition} The Tradeoff
:class: important

Every Sybil defense adds friction. Require too little proof and your airdrop is farmed. Require too much and legitimate users don't bother claiming. The right balance depends on the size of your distribution and the sophistication of your community. For student exercises with small amounts on devnet, Sybil defense is unnecessary — but understanding the attack is essential for designing any real distribution campaign.
:::

---

## Batch Transactions: Why Solana Makes Mass Distribution Practical

Sending tokens to 10,000 wallets on Ethereum would cost tens of thousands of dollars in gas fees at peak demand. The fee structure of Ethereum's base layer makes mass airdrops economically impractical unless the token being distributed has significant value — and even then, the fees eat meaningfully into the distribution budget.

Solana's architecture changes this calculation entirely. Transaction fees on Solana are denominated in lamports (1 SOL = 1,000,000,000 lamports), and a typical token transfer costs roughly 5,000 lamports — about \$0.001 at standard SOL prices. A batch of 10,000 transfers costs approximately \$10 in fees. This is not a rounding error in a \$100,000 marketing budget. It is genuinely negligible.

:::{figure} ../images/ch06-batch-transactions.png
:label: fig-ch06-batch-transactions
:alt: Comparison chart showing the cost of distributing tokens to 10,000 wallets on Ethereum versus Solana, with fee breakdown per transaction and total distribution cost
:width: 80%
:align: center

**Fee Comparison: Batch Airdrops on Ethereum vs. Solana.** At standard gas prices, an Ethereum airdrop to 10,000 wallets costs 1,000–5,000× more than the equivalent operation on Solana. This difference determines whether mass distribution is economically viable.
:::

Solana also supports **transaction packing** — including multiple token transfers in a single transaction. A single Solana transaction can contain instructions that send tokens to dozens of recipients simultaneously, further reducing overhead. Tools like **Airdrop.to**, **Streamflow Airdrop**, and **Disperse.app** (for Solana) provide no-code interfaces for uploading a CSV of recipients and amounts, preview the total cost, and execute the batch in a single workflow.

The practical implication: Solana makes it economically rational to distribute to a large number of small holders. This has ecosystem-level significance. Ethereum's fee structure naturally concentrates airdrops among wallets large enough to justify the gas cost. Solana's fee structure enables genuinely broad distribution — which is closer to the democratic ideal that many token projects claim to represent.

### Computing Your Distribution Cost

For any airdrop campaign, compute the full cost before committing:

```
Total Cost = (Token FMV × Total Tokens Distributed)
           + (SOL per transfer × Number of Recipients × SOL price)
           + (Rent-exempt deposit × New token accounts created)
```

The **rent-exempt deposit** requires explanation. On Solana, every account must hold a minimum SOL balance to be rent-exempt. A token account (the account that holds a specific SPL token for a specific wallet) requires approximately 0.002 SOL. If you are airdropping to wallets that have never held your token before, you must fund the creation of their token accounts — which costs ~\$0.20 per new account at SOL ≈ \$100. For 10,000 new recipients, this adds approximately \$2,000 to your distribution cost. Factor this into your CPA calculation.

:::{admonition} The Tax Line Nobody Budgets
:class: warning

Distribution has a tax dimension that almost no first-time issuer budgets for. The framing below is U.S. law; your jurisdiction differs, but the categories are broadly the same — check with a tax professional before any real distribution.

**For recipients:** an airdrop received is ordinary income at the token's fair market value on the date of receipt — this has been IRS guidance since 2019 (see *Fair Market Value (FMV)* in the glossary). Streaming payments and vesting releases to contributors are compensation, taxable when received, not when the stream was created. And adding or removing liquidity and swapping one token for another are generally taxable events in their own right.

**For reporting:** brokers now report digital-asset transactions to the IRS on **Form 1099-DA**, so the assumption that token activity is invisible is no longer even superficially true.

**For you, the issuer:** if you are paying contractors in tokens, you have the same reporting duties as if you paid them in dollars. The vesting stream in this chapter's lab is, in a real deployment, a payroll event. Budget for the paperwork alongside the rent-exempt deposits — and see Chapter 12's launch checklist, which now carries this as a pre-launch line item.
:::

:::{figure} ../images/ch06-tax-events.png
:label: fig-ch06-tax-events
:alt: Diagram mapping token distribution events — airdrop receipt, vesting release, streaming withdrawal, swap, and liquidity add or remove — to their U.S. tax treatment as ordinary income, compensation, or capital gain events, with Form 1099-DA reporting flow
:width: 80%
:align: center

**Taxable Events in Token Distribution:** Airdrops are income at fair market value on receipt; vesting and streaming releases are compensation when received; swaps and liquidity changes are generally taxable events. Brokers report on Form 1099-DA.
:::

---

## Distribution as Signaling: What the Market Reads From Your Allocation

Before a token has a price, it has an **allocation table**. The percentage of total supply allocated to different stakeholders — team, investors, treasury, community, ecosystem — is one of the most read documents in any token launch.

Markets are not naive about this. A project that allocates 60% of tokens to insiders and 40% to "community" is signaling something very different from a project that allocates 20% to insiders and 80% to community. Analysts, investors, and sophisticated users parse allocation tables the way equity analysts parse cap tables.

:::{figure} ../images/ch06-allocation-pie.png
:label: fig-ch06-allocation-pie
:alt: Two pie charts comparing a community-favorable token allocation (20% team, 15% investors, 65% community and ecosystem) versus an insider-heavy allocation (45% team, 30% investors, 25% community)
:width: 80%
:align: center

**Allocation Tables as Market Signals:** Two token projects with identical technology will receive very different market reactions based on their allocation tables. Community-favorable allocations signal long-term protocol alignment; insider-heavy tables signal short-term extraction risk.
:::

Key signals markets read from allocation tables:

**Team percentage and vesting duration.** A 20% team allocation with a 4-year vest signals long-term commitment. A 40% team allocation with a 6-month cliff and 1-year vest signals a team positioned to exit quickly. The ratio matters less than the combination of percentage and lock duration.

**Investor cliff and unlock timing.** If early investors' tokens unlock at the same time as the token goes public, expect selling pressure. Projects that survive price discovery have investor lockups that extend well past the initial listing.

**Treasury size and control.** A large treasury controlled by a multisig wallet controlled by the founding team is qualitatively different from a large treasury governed by on-chain governance. The market values decentralized control of treasury funds, because concentrated control creates exit risk.

**Ecosystem fund allocation.** Tokens earmarked for "ecosystem development" — grants, liquidity incentives, developer rewards — signal investment in growth. But if the ecosystem fund has no vesting schedule and is controlled by insiders, the label is meaningless.

:::{admonition} The Transparency Advantage
:class: tip

Every allocation category should have a corresponding on-chain vesting contract or multisig address that is publicly discoverable. Listing the contract addresses in your documentation costs nothing and eliminates the "trust us" problem. Markets discount opacity; they reward verifiability.
:::

---

## Hands-On Lab: Put Tokens in Other People's Hands

:::{note}
This lab runs on devnet because you will be sending tokens to many wallets and testing cancellation. Your Chapter 3 token exists only on mainnet. Mint a throwaway devnet token first (Chapter 3, Step 3b, or any creator switched to devnet) and use it for every step below.
:::

This lab has three components: setting up a vesting stream for a hypothetical co-founder, executing a bulk airdrop to classmates' wallets, and computing your cost per holder.

**What you need before starting:**
- Phantom wallet funded with devnet SOL (`solana airdrop 2` on devnet)
- Your token minted from Chapter 3's lab (or mint a fresh one on devnet)
- Classmates' wallet addresses (collect via shared spreadsheet)

:::{figure} ../images/ch06-lab-workflow.png
:label: fig-ch06-lab-workflow
:alt: Step-by-step workflow diagram for the Chapter 6 lab showing: connect wallet to Streamflow, create vesting stream, export recipient CSV, run batch airdrop, verify on Solscan, compute cost per holder
:width: 80%
:align: center

**Lab Workflow:** Three sequential operations — vesting stream creation, bulk airdrop execution, and cost-per-holder calculation — using Streamflow and Solscan on Solana devnet.
:::

### Part 1: Create a Vesting Stream with Streamflow

1. Navigate to [app.streamflow.finance](https://app.streamflow.finance) and switch your wallet to **devnet** mode
2. Select **Vesting** from the left navigation
3. Click **New Stream**
4. Enter:
   - **Token:** Your token mint address from Chapter 3
   - **Recipient:** A classmate's wallet address (or a second wallet you control)
   - **Amount:** 1,000 tokens
   - **Cliff duration:** 1 minute (for demonstration purposes — real cliffs are months)
   - **Total duration:** 10 minutes
   - **Release frequency:** Every second (continuous)
5. Click **Create Stream** and approve the transaction in Phantom
6. Note the stream URL — share it with your "co-founder" so they can see their vesting schedule
7. After the cliff, have the recipient withdraw once. Then, as the sender, **cancel** the stream. Record what returned to you and what stayed with the recipient. This is the clawback right from the Streaming Payments section, demonstrated.

After the cliff period, your recipient can connect their wallet to Streamflow and withdraw whatever has streamed. Watch the accumulated balance tick upward in real time.

### Part 2: Execute a Bulk Airdrop

For this exercise, use [Airdrop.to](https://airdrop.to) or the Streamflow Airdrop tool on devnet:

1. Create a CSV file with two columns: `wallet_address`, `amount`
2. Add at least 5 classmates' wallet addresses (or test addresses) with 100 tokens each
3. Upload the CSV to the airdrop tool
4. Preview the total cost: tokens distributed + SOL fees + rent-exempt deposits
5. Execute the airdrop
6. Open [Solscan.io](https://solscan.io) and search for your token mint address
7. Navigate to **Token Accounts** to see the holders list — your classmates should appear

:::{admonition} Using Solscan to Verify
:class: note

Solscan's **Token Accounts** view shows every wallet currently holding your token, sorted by balance. This is the ground truth — not your spreadsheet, not your tool's confirmation screen. If a wallet appears here, the transfer succeeded. If it doesn't, something failed. Always verify on-chain.
:::

### Part 3: Compute Your Cost Per Holder

Fill in this table with your actual numbers:

| Metric | Value |
|--------|-------|
| Total tokens distributed | \_\_\_\_\_ |
| Token price (devnet: estimate \$0.001 per token) | \_\_\_\_\_ |
| Total token value distributed (\$) | \_\_\_\_\_ |
| SOL fees paid | \_\_\_\_\_ |
| Rent-exempt deposits paid | \_\_\_\_\_ |
| Total cost in USD | \_\_\_\_\_ |
| Number of unique new holders | \_\_\_\_\_ |
| **Cost per holder** | **\_\_\_\_\_** |

If you distributed tokens to holders who were already holding your token (from previous labs), note the difference between **new** holders and **existing** holders. Only new holders count as acquisitions in your CPA calculation.

### Part 4: Sybil-Test Your Own Airdrop (10 min)

1. Create a third Phantom account. Attempt to claim/receive the same airdrop with it (re-run the CSV with the new address added).
2. It works — nothing stopped you. Write three sentences: which of the four Sybil defenses from the chapter would have stopped this, what it would have cost you to implement, and what it would cost a legitimate classmate in friction.

---

## What You Walk Away With

By the end of this lab, you have demonstrated three distinct distribution primitives:

1. **A live vesting stream** — tokens locked in a Streamflow contract, releasing to a recipient on a schedule. You have seen how code replaces a legal agreement, and you understand the cliff mechanism that protects against early departures.

2. **Tokens in other people's wallets** — a verified on-chain airdrop with results visible on Solscan. You have executed the most fundamental act in a token economy: making someone else a holder.

3. **A cost-per-holder figure** — the quantitative foundation for any distribution campaign. You know what you spent, in real terms, to acquire each holder. You can now think about whether that cost is justified by the holder's expected value to the ecosystem.

These three tools — vesting, airdrops, and cost analysis — are not decorative. They are the instruments by which a token becomes an economy.

---

## 🎯 In-Class Assignment: Design a Distribution Campaign (10 pts)

**Details and instructions will be provided in class.**

**Points:** 10

---

## Discussion: Ownership vs. Discount

:::{epigraph}
Airdrops are marketing that hands out ownership. Would you rather receive \$50 of a company's token or a \$50 discount on its product? Which one makes you a customer, and which makes you an owner — and does a company want both?
:::

This question cuts to the heart of token economics. A \$50 discount is a transaction: the company spends \$50 to acquire a customer interaction, and the relationship ends when the discount is used. A \$50 token allocation is something else. The recipient now has skin in the game. If the protocol succeeds, their \$50 becomes more. If it fails, it becomes less. They have an incentive to use the product (increasing its value), tell their network (growing the holder base), and vote on governance proposals (shaping the protocol's future).

The company's calculus is not obvious. A customer who bought at a discount has paid money — revenue that can fund operations. A holder who received tokens for free has not paid anything, but has received something with real expected value. The question is whether the holder's future engagement and amplification are worth more than the immediate revenue of a paying customer.

The most sophisticated token projects think about this as a **two-sided portfolio**. They want paying customers (revenue), and they want aligned holders (governance and network effects). The airdrop creates holders; the product creates customers. The ideal is a user who is both — someone who uses the product because it is useful *and* holds tokens because they believe in the protocol's future. That alignment is what traditional customer acquisition cannot buy.

**Discussion Guidelines**

Write a substantial response (300+ words) addressing: Which would you choose — the token or the discount — and why? Consider the difference in your relationship with the company under each scenario. Include at least one scholarly or credible citation supporting your argument (can be an economic paper, a documented case study of a major airdrop, or a credible industry analysis). Then respond substantively to at least **two** classmates — engage with their reasoning, push back where you disagree, or extend their argument with evidence they haven't considered. Simple agreement ("Great point!") does not qualify as a substantial response.

---

## Glossary

```{glossary}
Airdrop
  A distribution of tokens to a list of wallet addresses, typically at no cost to the recipient. Used for community building, user acquisition, and rewarding early adopters.

Vesting Contract
  A smart contract that holds tokens and releases them to a beneficiary according to a predefined schedule. Replaces traditional legal vesting agreements with on-chain enforcement.

Cliff
  In a vesting schedule, the period before any tokens unlock. A 12-month cliff means the beneficiary receives no tokens for the first year, then receives the first tranche at month 12.

Streaming Payment
  A vesting or payment arrangement where tokens are released continuously over time — by the second — rather than in discrete tranches. Supported by protocols like Streamflow on Solana.

Sybil Attack
  An attack on a system that relies on unique participants, where a single malicious actor creates many fake identities to gain a disproportionate share of rewards (e.g., claiming multiple airdrops from one person).

Quadratic Distribution
  An airdrop formula where the amount received scales with the square root of the recipient's qualifying activity, reducing rewards for high-activity wallets and limiting the incentive for Sybil farming.

Cost Per Holder (CPH)
  The total cost of a token distribution (token FMV distributed + fees) divided by the number of unique wallets receiving tokens. The token equivalent of cost per acquisition in traditional marketing.

Batch Transaction
  A Solana transaction that includes multiple transfer instructions, allowing tokens to be sent to many recipients in a single atomic operation. Reduces per-transfer overhead.

Rent-Exempt Deposit
  On Solana, every account must maintain a minimum SOL balance to avoid rent. Creating a new token account for a recipient requires paying this deposit (~0.002 SOL), which is returned if the account is later closed.

Allocation Table
  A document showing how the total token supply is distributed across stakeholder categories (team, investors, treasury, community, ecosystem). Widely analyzed as a signal of project integrity and insider alignment.

Token Account
  On Solana's SPL token standard, a token account is a separate on-chain account that holds a specific token for a specific wallet. Each wallet must have a unique token account for each SPL token it holds.

Fair Market Value (FMV)
  The price at which a token would trade between willing buyers and sellers, both reasonably informed. Used in cost-per-holder calculations and tax accounting for token distributions.

Streamflow
  A vesting and streaming payment protocol on Solana that provides no-code interfaces for creating time-locked token releases and real-time payment streams.

Linear Vesting
  A vesting schedule where tokens unlock at a constant rate over time (e.g., 1/24th of the total each month for two years), as opposed to a cliff-only schedule that releases everything at once.

Treasury Multisig
  A multi-signature wallet controlling a project's treasury funds, requiring approval from multiple keyholders before funds can be moved. Standard governance infrastructure for decentralized protocols.

Taxable Event
  Any transaction that triggers a tax obligation. In U.S. treatment, receiving an airdrop, receiving vested or streamed tokens as compensation, swapping tokens, and adding or removing liquidity are generally taxable events.

Form 1099-DA
  The U.S. IRS information return on which brokers report customers' digital-asset transactions, analogous to the 1099-B for securities. Its existence means on-chain activity is reported to tax authorities, not merely visible on the ledger.
```

---

## Key Takeaways

:::{card} Chapter 6 Summary
- **Distribution creates the economy.** Tokens held by one entity have no economy; distribution is the act that creates one.
- **Airdrops are acquisition, not charity.** The cost-per-holder framework makes the economics legible and comparable to traditional marketing.
- **Vesting contracts encode promises in code.** Public, verifiable vesting schedules signal commitment and reduce the market's discount for insider token risk.
- **Streaming payments enable new accountability structures.** Real-time payment streams replace invoice cycles and provide natural clawback rights.
- **Sybil attacks are the adversarial norm.** Any distribution system worth meaningful value will be attacked; defense requires on-chain reputation or identity verification.
- **Solana's fee structure enables mass distribution.** The economics that make broad airdrops viable on Solana do not exist on most other chains.
- **Allocation tables are market signals.** The structure of your token distribution — who gets what, when, with what lock conditions — tells the market who you are and what you intend.
:::

<!-- NEW IMAGES NEEDED: ch06-tax-events.png (diagram mapping distribution events — airdrop receipt, vesting release, streaming withdrawal, swap, liquidity add/remove — to their U.S. tax treatment, with Form 1099-DA reporting flow) -->
