---
title: "Give It Something to Do — Utility Without Code"
subtitle: "A Token Without a Job Is Just a Speculative Bet"
short_title: "Utility Without Code"
description: "Every token needs a reason to exist beyond being traded. This chapter covers utility sinks, token-gating, tiered benefits, payments in your own token, and the engagement loop — and shows you how to build a real gated community without writing a line of code."
label: ch-07-utility
tags: [token utility, token-gating, Discord, Telegram, Collab.Land, Matrica, engagement loop, loyalty mechanics, tiered benefits, Web3 community, Solana Pay]
---

# Give It Something to Do — Utility Without Code

:::{figure} ../images/ch07-explainer-infographic.png
:label: fig-ch07-infographic
:alt: Illustrated explainer infographic showing the full token utility ecosystem — utility sinks, token-gating, tiered tiers, payment flows, and the earn-hold-spend engagement loop
:width: 80%
:align: center

**Chapter 7 Explainer Infographic:** The complete map of token utility — from utility sinks and access gates to tiered status and the engagement loop. A token without a job is just a number.
:::

Every token is a bet on future usefulness. If no one can do anything with a token except sell it, the only rational behavior is to speculate on the price and exit at the right moment. That is not an economy. That is a casino.

Utility changes the calculation. The moment a token can open a door — grant access to a channel, unlock a price discount, confer voting power, or pay for a service — it has a reason to be held. Holders who want access cannot sell. Sellers who want access have to buy back in. The speculative dynamic shifts from pure price momentum to something more durable: tokens circulating through an ecosystem, doing jobs, returning to holders who need them.

This chapter is about that shift. We will work through the theory of utility sinks, explain token-gating as the simplest utility primitive, build tiered benefit structures, explore payments in your own token, and compare all of this to the loyalty mechanics that brick-and-mortar businesses have used for decades. And then — because theory without practice is worthless — you will build a real gated door: a Discord or Telegram channel that only your token holders can see.

None of this requires you to write a line of code.

---

## The Utility Sink: Why a Token Needs Somewhere to Go

Start with a thought experiment. Imagine a river with no outlet — water flows in from tributaries but has nowhere to drain. Eventually the basin floods, the pressure builds, and the system destabilizes. Now imagine the same river with lakes, wetlands, and an ocean. Water moves through. The ecosystem breathes.

A token economy works the same way. Tokens need **sinks** — places where they are consumed, locked, or removed from circulation — just as much as they need sources. Without sinks, every token ever minted eventually ends up on an exchange, creating constant downward sell pressure. The price chart for a token with no utility looks like a mountain: a sharp rise on launch excitement, a grinding decline as early holders exit, and a long flat line as the community loses faith.

:::{figure} ../images/ch07-utility-sink-diagram.png
:label: fig-ch07-utility-sink
:alt: Diagram showing token flow with and without utility sinks — left side shows tokens flooding into an exchange, right side shows tokens circulating through gating, payments, staking, and governance sinks
:width: 80%
:align: center

**Utility Sinks in Action:** Without sinks (left), all tokens eventually flow to the exchange and depress the price. With sinks (right), tokens circulate through access gates, payment flows, and staking pools — reducing sell pressure and increasing holder tenure.
:::

A utility sink is any mechanism that gives a holder a reason *not to sell*. The strongest sinks are **access-based**: if you sell your tokens, you lose something you actively want. This is categorically different from a financial incentive like staking rewards. Staking says "we will pay you to hold." Access-gating says "if you don't hold, you cannot get in." One is a bribe. The other is a lock.

The most durable token economies combine multiple sink types:

**Access sinks** — Token-gated communities, content, features, or events. Selling means losing access.

**Consumption sinks** — Tokens spent to use a service are burned or removed from supply. Every use permanently reduces the circulating float.

**Governance sinks** — Voting requires holding. Proposals require staking tokens as a deposit. Sellers lose their voice.

**Status sinks** — Tiered systems where reaching a higher level requires holding more tokens. No shortcut; you either hold or you don't qualify.

The key insight is that sinks do not have to be elaborate. A single Discord channel that only holders can see is a sink. It is small, but it is real. It creates holding behavior, and holding behavior creates price stability, and price stability creates credibility for the ecosystem.

:::{admonition} The Sink Hierarchy
:class: note

Not all sinks are equal. Rank them by holder psychology:

1. **Access sinks** (strongest) — fear of losing something actively wanted
2. **Status sinks** — identity and social proof tied to holding level
3. **Consumption sinks** — economic incentive to hold for future use
4. **Governance sinks** — weakest for most holders unless governance is genuinely meaningful

Build your first utility with an access sink. It is the easiest to explain and the hardest to walk away from.
:::

---

## Token-Gating: Access as a Function of Balance

Token-gating is the simplest utility you can add to any token without writing code. The concept is elegant: a service checks a wallet's token balance, and if the balance meets a threshold, access is granted. Below the threshold, access is denied. The token is literally a key.

Think of it like a hotel loyalty card system — except instead of presenting a plastic card, you present your wallet address, and the verification happens on-chain in real time. The hotel does not trust you to say you have enough points. It checks the system. Token-gating is the same, except the system is a public blockchain and no single entity controls the records.

:::{figure} ../images/ch07-token-gating-flow.png
:label: fig-ch07-gating-flow
:alt: Flowchart showing the token-gating verification process — wallet connects, balance is checked on-chain, threshold comparison happens, and access is granted or denied with labeled steps
:width: 80%
:align: center

**Token-Gating Verification Flow:** The wallet connects, a read request goes to the Solana RPC, the balance is compared to the threshold, and the gate opens or stays shut. No code needed — the platforms handle all of this automatically.
:::

Here is why this is revolutionary in ways that traditional loyalty programs are not: the verification is **trustless and permissionless**. When American Airlines checks your AAdvantage status, they are trusting their own database — a database they fully control, can modify, and can revoke access to at any time. When a token-gating platform checks your Solana wallet, it is reading from a global ledger that no one controls. Your access is as real as your tokens. No one can blacklist your wallet from holding tokens without taking ownership of the blockchain itself.

This creates a fundamentally different relationship between the community owner and the community members. You are not *granting* access as a favor that can be revoked. You are *recognizing* ownership that already exists on-chain.

### How Token-Gating Platforms Work

Several no-code platforms make token-gating straightforward for Solana tokens:

**Collab.Land** — The most widely installed token-gating bot, supporting both Discord and Telegram. On Solana, a "Token Gating Rule" (TGR) checks an SPL token balance or an NFT collection; several TGRs can map to a single role, and members verify by connecting Phantom through the bot's link. A free tier covers small servers.

**Matrica** — Solana-native, with both Discord and Telegram integration. Rules can be built on SPL token balances, NFT collections, and NFT traits. Paid plans start at roughly \$35/month.

:::{figure} ../images/ch07-gating-platforms.png
:label: fig-ch07-gating-platforms
:alt: Comparison grid of two Solana token-gating platforms — Collab.Land and Matrica — with their key features and Discord or Telegram compatibility
:width: 80%
:align: center

**Token-Gating Platform Comparison:** Collab.Land and Matrica, the two live no-code platforms for gating Solana SPL token communities. Both read on-chain balances; they differ in rule complexity, pricing, and ecosystem integrations.
:::

Each platform follows the same pattern:

1. Community admin connects the platform to their Discord server or Telegram group and grants the bot appropriate permissions
2. Admin defines a **role** (in Discord) or **access tier** (in Telegram) tied to a minimum token balance
3. Members visit the platform's web interface and connect their Solana wallet via Phantom, Backpack, or another wallet
4. The platform reads the wallet's token balance from Solana's RPC
5. If the balance meets the threshold, the role is assigned and the member gains access
6. The platform re-checks balances on a schedule (hourly or daily). If a member sells below the threshold, the role is revoked

The entire loop runs without any manual intervention from the community admin.

:::{admonition} Choosing the Right Minimum Balance
:class: tip

The minimum balance is a design decision, not a technical one. Set it too low and gating provides no real scarcity. Set it too high and you lock out legitimate early supporters.

A practical starting point for a classroom or small community: set the minimum at whatever amount represents roughly 1–5% of your total supply divided by your expected community size. If you have 1,000,000 tokens and want a community of 100 people, a minimum of 1,000 tokens means the gated community requires 10% of supply to be collectively held by members — a meaningful sink.
:::

---

## Tiered Benefits: Turning Holdings Into Status

Single-tier gating is binary: you are in or you are out. Tiered gating is a spectrum: the more you hold, the more you get. This transforms a simple access gate into a **status system** — one of the most powerful behavioral mechanisms in human psychology.

Every loyalty program that has ever worked relies on tiers. Airlines give you Silver, Gold, Platinum, Executive Platinum. Credit cards give you Green, Gold, Platinum, Centurion. Coffee chains give you Green, Gold. The specifics vary, but the psychology is constant: once you reach a tier, you will pay a behavioral premium to keep it. Frequent fliers take unnecessary flights in December just to retain status. Coffee drinkers buy extra lattes in the last week of the year just to keep their Gold card.

Token-gating can replicate this psychology with a crucial advantage: the tiers are transparent and trustless. You cannot sweet-talk your way to Platinum. Your wallet balance either qualifies or it doesn't.

:::{figure} ../images/ch07-tier-system.png
:label: fig-ch07-tier-system
:alt: Infographic showing a four-tier token holder system with bronze, silver, gold, and platinum levels, their minimum token requirements, and the exclusive benefits unlocked at each tier
:width: 80%
:align: center

**Tiered Token Holder System:** Four status levels tied to wallet balances, each unlocking progressively exclusive benefits. The status hierarchy creates holding incentives at every level of the community.
:::

Here is how to design a tiered system for your token:

**Step 1: Define the tiers.** Four levels is the standard. Two is too flat. Six is too complex. Four gives you enough differentiation that moving up feels meaningful, without the cognitive overhead of managing eight separate benefit sets.

**Step 2: Set the thresholds.** Each threshold should require roughly 3–5× the previous one. This is the "tier jump" — enough of a gap that reaching the next level is a genuine accomplishment, but not so large that it feels unattainable from the tier below.

**Step 3: Assign benefits.** The benefits must be *genuinely desirable* and, where possible, exclusive. "Access to a private Discord channel" is meaningful. "A special badge" is not, by itself, a reason to hold more tokens. Consider mixing:

- **Access benefits**: private channels, early access to announcements, exclusive AMAs
- **Economic benefits**: discounts on your product or service, early access to future token sales
- **Social benefits**: your name on a leaderboard, recognition in announcements, a unique role color in Discord
- **Voice benefits**: priority weighting in governance votes, the ability to submit governance proposals

**Step 4: Tie benefits to the current balance, not the historical peak.** This is critical. If you reward historical peaks, holders can reach a tier, sell all their tokens, and keep the benefits forever. If you gate on the current balance with continuous checking, holding the tokens is an ongoing requirement.

A simple example for a course token:

| Tier | Minimum Balance | Benefits |
|------|----------------|----------|
| Explorer | 100 tokens | Access to the holders-only Discord channel |
| Builder | 500 tokens | Early access to new course material + Explorer benefits |
| Architect | 2,000 tokens | Monthly live Q\&A session + Builder benefits |
| Founder | 10,000 tokens | Co-creator credit in course, private 1:1 office hour per semester + Architect benefits |

This structure creates four distinct groups of holders, each with a clear path upward and a clear reason to stay.

:::{admonition} The Tier Migration Moment
:class: important

The most powerful moment in a tiered system is when a member crosses a threshold for the first time. This is your **tier migration moment** — and it should be celebrated publicly. When a member reaches Architect tier, announce it in the community. Tag them. Make it a visible achievement.

This does two things simultaneously: it rewards the holder with social recognition (amplifying the status benefit), and it signals to other community members that the tier is real and attainable. Milestone announcements are free marketing for your tier system.
:::

---

## Payments in Your Own Token: Pricing, Volatility, and the Convert-Immediately Reality

Beyond access, tokens can serve as a payment medium. Instead of charging customers in dollars, you charge them in your token. This creates demand — to buy your service, users must first acquire your token — and it creates circulation, which is a form of activity that keeps the economy alive.

The mechanics are simple enough: you price your service in tokens, accept token payments, and the tokens move from the buyer's wallet to yours (or to a treasury wallet). But underneath that simple mechanic is a set of economic challenges that every founder building a token payment system must understand.

:::{figure} ../images/ch07-payment-flow.png
:label: fig-ch07-payment-flow
:alt: Diagram showing token payment flow from customer wallet through service access point to treasury or burn mechanism, with volatility risk labeled
:width: 80%
:align: center

**Token Payment Flow:** The customer acquires tokens on the open market, spends them on the service, and the tokens arrive in your treasury. The volatility problem sits between acquisition and payment.
:::

### The Pricing Problem

When you charge \$50 for a service in dollars, the price is stable. When you charge 500 tokens for the same service, the dollar value of those 500 tokens fluctuates with the token's market price. If the token doubles overnight, you effectively charged \$100. If it halves, you charged \$25.

There are three standard approaches to this problem:

**Fixed token price** — You always charge 500 tokens regardless of the token's market value. This is simple but creates wild swings in your dollar revenue. It works if you primarily care about token circulation rather than consistent revenue.

**Dollar-denominated price, token payment** — You price services in dollars (e.g., \$50) and then calculate the token equivalent at the moment of payment using a price oracle. The customer always pays the dollar equivalent. This protects your revenue but requires real-time price data — using a price oracle such as Pyth (Chapter 5, *Oracles*).

**Hybrid: fixed token, dollar floor** — You charge a fixed number of tokens but require a minimum dollar equivalent. If the token's value drops below a floor, you adjust the token price. Protects against severe downside while still using tokens as the primary unit.

For most early-stage token projects, the answer is to accept and immediately convert. The honest truth about token payments is that most businesses — even mature Web3 businesses — do not hold the tokens they receive as payment. They accept the tokens to create demand, then immediately sell them for stablecoins or dollars to cover operating expenses. The demand creation is the point, not the token accumulation.

This is not a failure of the token model. It is the model working correctly. The business creates demand by requiring tokens to access its services. That demand gives the token value. The business then captures some of that value by converting tokens to stable currency. The token economy does not require the business to take on token price risk in order to function.

:::{figure} ../images/ch07-convert-immediately.png
:label: fig-ch07-convert
:alt: Side-by-side comparison showing hold strategy versus convert-immediately strategy for token payment recipients, with risk and revenue stability analysis
:width: 80%
:align: center

**Hold vs. Convert:** Most businesses that accept token payments convert immediately to stablecoins or fiat. The demand-creation benefit is real; the need to hold price risk is not. Separating these two decisions makes token payments practical.
:::

### Why Accept Tokens At All If You Convert Immediately?

This question gets to the heart of token utility design. If you convert immediately, are you really "accepting tokens" in any meaningful sense?

Yes — because the demand event is real. Every time a customer purchases tokens on the open market to pay for your service, they are adding buying pressure to the token's price. If 100 customers each buy 500 tokens per month to access your service, that is 50,000 tokens of monthly buying pressure, regardless of what you do with the tokens afterward. The market does not know or care that you sold them five minutes after receiving them. It only sees 50,000 tokens of demand.

The mechanism creates a **demand floor**: as long as your service is desirable and priced in your token, there is predictable, repeatable buying pressure supporting the token's market price. That floor is the economic value you are building.

### The Rail: Solana Pay

Everything above describes the economics of accepting your token. **Solana Pay** is the rail that actually moves it at a point of sale. It is an open payment specification — a URL and QR-code format that any Solana wallet can read:

```
solana:<recipient>?amount=…&spl-token=<mint>&label=…
```

Encode a request like that into a QR code, and any customer with Phantom (or another Solana wallet) scans it and pays in SOL, USDC, or *your* SPL token, settling on-chain in under a second with no card network in between. This is the point-of-sale integration that Chapter 2's Starbucks-on-chain thought experiment and Chapter 8's loyalty check-in program both assume exists.

It is not hypothetical infrastructure. Shopify has offered Solana Pay as a checkout option since 2023 (shopifydocs.solanapay.com), settling in USDC, and other commerce plugins exist. In practice, this connects directly to Chapter 5's stablecoin discussion: most merchants request USDC — the stable unit of account — and let customers pay from any token they hold via a swap in the wallet. The customer spends your token; the merchant receives dollars; the demand event still happened.

:::{figure} ../images/ch07-solana-pay-qr-flow.png
:label: fig-ch07-solana-pay
:alt: Flow diagram of a Solana Pay transaction — merchant encodes a payment request URL into a QR code, customer scans it with Phantom mobile, approves, and tokens settle on-chain to the merchant wallet in under a second
:width: 80%
:align: center

**The Solana Pay Flow:** A payment request URL becomes a QR code; the customer scans and approves in their wallet; settlement is on-chain in under a second, with no card network between buyer and seller.
:::

---

## On-Chain Utility vs. Traditional Loyalty Mechanics

At this point, it is worth stepping back and asking a harder question: is this actually better than traditional loyalty programs? Airlines, hotels, and credit card companies have had tiered access, exclusive benefits, and engagement loops for decades. What does the blockchain add?

The honest answer is: for the user experience, often not much — and sometimes less. Phantom wallet is not more convenient than swiping a Marriott Bonvoy card. Blockchain transactions take time. Gas fees (even tiny ones on Solana) are friction. The token-gating verification step adds a connect-wallet flow that many users find unfamiliar.

What blockchain adds is *structural*, not experiential:

:::{figure} ../images/ch07-loyalty-comparison.png
:label: fig-ch07-loyalty-comparison
:alt: Side-by-side comparison table of traditional loyalty programs versus token-based loyalty, showing portability, ownership, transparency, interoperability, and cost columns
:width: 80%
:align: center

**Loyalty Mechanics Compared:** Traditional programs win on UX. Token-based programs win on portability, true ownership, and composability. The revolution is structural, not cosmetic.
:::

**Portability** — Traditional loyalty points are owned by the airline, hotel, or bank. They can expire, be devalued, or be revoked at any time. Your Marriott points are a liability on Marriott's balance sheet, not an asset on yours. Token-based loyalty benefits are owned by the holder's wallet and can be sold, transferred, or held indefinitely. The relationship between holder and benefit is peer-to-peer, not corporate-to-customer.

**Transparency** — An airline's loyalty tier algorithm is a black box. No one outside the company knows exactly how miles are calculated, why some routes earn differently than others, or what the true redemption value of a mile will be in three years. A token-gating system is fully transparent: the threshold is public, the wallet balance is public, and the access decision is deterministic. No algorithmic opacity, no customer service disputes.

**Composability** — A traditional loyalty program is a walled garden. Your Delta SkyMiles are valuable only within Delta's ecosystem. A token can be designed to provide utility across multiple platforms simultaneously. Hold 500 tokens and you get Discord access, a discount code on the website, and early access to a partner platform — all from the same wallet balance, verified by different services reading the same on-chain data.

**Transferability** — You cannot sell your airline status. You cannot give your hotel points to your business partner's account without complex workarounds. Token-based status transfers with the wallet. This creates secondary markets for access — which sounds strange until you realize it means community membership has genuine market value.

The honest limitation is that traditional loyalty programs have one massive advantage: the infrastructure works at scale, is familiar to consumers, and is integrated into booking flows, POS systems, and customer service workflows that have been refined over 30 years. Token-gating is still early. The UX gaps are real. Building for token utility today means accepting some friction that traditional programs have already solved — in exchange for structural properties that traditional programs can never offer. That said, embedded wallets and passkey sign-in (Chapter 1) are closing the connect-wallet gap. The 2026 pattern is that the customer never sees a seed phrase and the token lives in a wallet created by the app.

:::{admonition} The Maturity Curve
:class: seealso

The best way to think about on-chain loyalty is not as a replacement for traditional programs but as the infrastructure for a new category. Email newsletters replaced physical mail not because email was more tangible, but because it was cheaper, faster, and programmable. Token-gating will replace traditional loyalty programs not because the wallet UX is better, but because the ownership model is fundamentally different — and ownership at scale changes everything.
:::

---

## The Engagement Loop: Earn, Hold, Spend, Repeat

Every sustainable token economy needs a flywheel — a cycle of behaviors that reinforces itself over time. The classic engagement loop for a utility token looks like this:

**Earn** → **Hold** → **Spend** → **Repeat**

:::{figure} ../images/ch07-engagement-loop.png
:label: fig-ch07-engagement-loop
:alt: Circular diagram showing the token engagement loop with four stages — earn, hold, spend, repeat — with arrows connecting each stage and labeled examples of each behavior
:width: 80%
:align: center

**The Token Engagement Loop:** Tokens earned through participation are held for access benefits, spent on services or governance, and the cycle repeats. Each rotation deepens the holder's investment in the ecosystem's health.
:::

Let us walk through each stage in the context of a real community:

**Earn**: Holders acquire tokens through participation — completing courses, contributing content, referring new members, winning competitions, or providing liquidity. The earning mechanism should reward genuine value creation, not just financial commitment. When earning is tied to behavior the community values, it creates a natural selection effect: the most active members accumulate the most tokens.

**Hold**: Holders keep their tokens to maintain access to tiered benefits. The holding phase is where the utility sink operates. Every holder who is actively using their gated benefits is a holder who has a reason not to sell. Holding is not passive; it is the continuous act of choosing to keep access over cashing out.

**Spend**: Holders spend tokens to use premium services, vote in governance, unlock exclusive content, or pay for community services. Spending tokens into a treasury or burning them through a consumption mechanism keeps the circulating supply in check. The key insight is that spending should feel like an exchange of value, not a cost. When you spend tokens to access a live Q\&A with an expert you genuinely wanted to meet, the spend feels like a purchase of something real — not a fee.

**Repeat**: After spending, holders have an incentive to earn more tokens to restore their balance. This brings them back into the earning phase, and the cycle continues. Communities that design this loop well create persistent engagement: members return not because of a push notification but because they have something at stake in the ecosystem's health.

The most important design principle for the loop is **leakage prevention**. Tokens that exit the loop entirely — sold to an exchange and never returned — represent permanent loss of engagement. Your goal is not to prevent selling entirely (that is impossible and creates its own perverse incentives), but to ensure that for every token that leaves the loop through selling, new value creation pulls another token back in through earning.

---

## 🎯 In-Class Assignment: Token Utility Architecture (10 pts)

**Details and instructions will be provided in class.**

**Points:** 10

---

## 🔬 Hands-On Lab: Build One Real Door

This is where the chapter becomes real. You are going to build one actual token gate — a community channel that only your token holders can access. You will invite classmates, verify that gating works for holders, verify that it fails for non-holders, and document the proof.

No code required. Just configuration.

### Part 1 — Build the Gate

### Choosing Your Platform

You have two primary options:

**Discord with Collab.Land** — free for small servers, Solana supported, the most widely used gating bot.

**Telegram with Matrica** — Better for mobile-first communities. Matrica supports Solana natively. Slightly more configuration overhead.

We will walk through the Discord + Collab.Land path in detail. The Telegram setup is structurally identical — the platform documentation covers the differences.

### Step-by-Step: Discord Token Gating with Collab.Land

**Phase 1: Prepare Your Discord Server**

1. Create a new Discord server (or use an existing test server). Name it after your token project.
2. Create a new text channel called `#holders-only`. Do not set any permissions yet.
3. Create a new role called `Token Holder`. Give this role access to `#holders-only`. Remove @everyone's access to that channel.
4. Test that an account without the `Token Holder` role cannot see `#holders-only`. If they can, the permissions are not set correctly.

**Phase 2: Configure Collab.Land**

1. Go to [collab.land](https://collab.land) → **Add to Discord**, choose your server, and authorize the bot (it needs Manage Roles and Read Members). The bot posts a **Let's Go** verification button in a `#collabland-join` channel it creates.
2. Open the Collab.Land **Command Center** ([cc.collab.land](https://cc.collab.land)), sign in with Discord, select your server.
3. Click **TGRs** → **Add TGR**. Set: **Chain:** Solana · **Token type:** SPL fungible token · **Token address:** your Chapter 3 mint address · **Min balance:** 10 (for testing) · **Role:** Token Holder. Save.
4. In Discord, drag the **Collab.Land** bot role above the **Token Holder** role in Server Settings → Roles, or the bot cannot assign it.

**Phase 3: Verify the Gate Works**

1. Share your server invite link with a classmate who holds your token (above the minimum).
2. Have them click **Let's Go** in `#collabland-join`, choose **Phantom**, and sign the verification message. The Token Holder role is assigned within a minute.
3. Confirm they can see and post in `#holders-only`.
4. Share the server invite with a classmate who does NOT hold your token.
5. Have them attempt to verify — they should receive a message that their balance is insufficient.
6. Confirm they cannot see `#holders-only`.

**Phase 4: Document the Proof**

Take screenshots of:
- The Collab.Land TGR configuration screen
- A successful verification (holder gaining access)
- A failed verification (non-holder denied)
- The `#holders-only` channel visible to the holder but not to the non-holder

Write a one-paragraph description of your setup: what token, what threshold, what the gated channel provides, and what you would add if this were a real production community.

:::{figure} ../images/ch07-holder-setup.png
:label: fig-ch07-holder-setup
:alt: Screenshot-style diagram showing the Collab.Land Command Center TGR configuration with SPL token address, minimum balance field, role assignment, and Discord channel permission setup
:width: 80%
:align: center

**Collab.Land Configuration Walkthrough:** The Command Center connects your token's mint address to a Discord role and sets the minimum balance threshold. The bot handles all on-chain verification and role management automatically.
:::

### Telegram Alternative: Matrica Setup

If your community is Telegram-based, the flow is equivalent:

1. Create a Telegram group or supergroup. Add Matrica's bot (`@MatricaLabsBot`).
2. In the Matrica dashboard at [matrica.io](https://matrica.io), connect your Telegram group and define an access rule: SPL token minimum balance.
3. Members verify by sending a verification command to the bot, which guides them through connecting their Solana wallet.
4. Members below the threshold are restricted from posting or are automatically removed from the group, depending on your settings.

The gating logic is identical. Only the interface differs.

### Part 2 — Get Paid in Your Token (15 min)

1. Construct a Solana Pay request for your token: `solana:<your primary wallet address>?amount=5&spl-token=<your mint address>&label=<YourToken>%20Coffee&message=Thanks`.
2. Turn it into a QR code with any QR generator, or paste the URL into a classmate's phone.
3. The classmate opens Phantom mobile → scan → approves. Confirm the 5 tokens arrived (Solscan).
4. Repeat with `spl-token=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v` (USDC) and `amount=0.01`. Write two sentences: which of the three pricing approaches in this chapter did each request implement, and which would a real shop use?

---

## Walk Away With

By the end of this chapter, you have:

- **A mental model for utility sinks** — you understand why tokens need somewhere to go besides an exchange, and you can identify the four types of sinks in any token economy
- **Working token-gating knowledge** — you understand how balance-based access verification works, which platforms implement it for Solana, and what the tradeoffs are between them
- **A tiered benefit framework** — you can design a four-tier status system with meaningful thresholds and desirable benefits at each level
- **A clear view of token payments** — you understand the volatility problem, the three pricing approaches, and why accept-and-convert is a legitimate and common strategy
- **A real gated community** — you have built at least one actual token gate, verified it works for holders and fails for non-holders, and documented the proof

The token now does something. It opens a door. Everything that follows in this course — governance, NFTs, analytics, and eventually code — builds on this foundation. A token with no utility is a speculative instrument. A token that opens doors is a tool.

---

## 💬 Discussion Question

A token-gated community is exclusive by design. Exclusivity drives value — scarcity creates desirability, insiders feel special, and the community signal is meaningful precisely because not everyone can enter. But exclusivity also creates insiders and outsiders. The people outside the gate may be the ones who most need access to the community's resources, networks, or knowledge.

When does gating build a community and when does it just build a wall?

Consider: a university professor gates a study group behind holding 50 tokens — a trivial amount for students with disposable income, an impossible amount for a student working three jobs. Is the gate neutral? Does it matter if the professor airdrops tokens to students who demonstrate financial need? Does the public verifiability of the blockchain make this kind of discrimination more or less acceptable than opaque traditional gatekeeping?

There is no clean answer. The discussion is the point.

:::{admonition} Discussion Guidelines
:class: note

**Main Response (Due by Day 3):** Write a substantive response (minimum 300 words) that takes a clear position. Include at least one scholarly or credible citation — a peer-reviewed paper, a credible journalism piece, or a documented case study. Generic opinions without evidence will not receive full credit.

**Peer Responses (Due by Day 7):** Respond to at least TWO classmates with substantive engagement — more than "I agree" or "great point." Engage with their evidence, challenge their assumptions, or extend their argument with new evidence of your own.
:::

---

## 📖 Glossary

```{glossary}
utility sink
  Any mechanism that gives a token holder a reason not to sell. Sinks include access gates, consumption burns, governance deposits, and status thresholds. Without sinks, all tokens eventually flow to exchanges.

token-gating
  A method of restricting access to digital spaces, content, or services based on a wallet's token balance. The gate is enforced by a platform that reads on-chain data rather than by a centralized database.

minimum balance
  The threshold a wallet must meet or exceed to qualify for a token-gated benefit. Balances below the threshold result in access denial; balances at or above the threshold grant access.

tiered benefits
  A structured system in which progressively higher token holdings unlock progressively more exclusive benefits. Tiers create status differentiation and holding incentives at multiple levels of the community.

access sink
  A token sink specifically tied to ongoing access. Selling tokens below the minimum balance removes the holder's access to gated content or communities, creating a direct cost to selling.

consumption sink
  A token sink in which tokens are burned or permanently removed from circulation as they are spent on services. Consumption sinks reduce total supply over time, creating deflationary pressure.

engagement loop
  The cyclical pattern of token behavior: earn tokens through participation, hold them for access benefits, spend them on services or governance, and earn again. A well-designed loop keeps holders active and reduces token leakage.

Collab.Land
  The most widely used token-gating bot for Discord and Telegram; on Solana it verifies SPL token balances and NFT holdings and assigns roles automatically.

SPL token
  A fungible token built on Solana's Token Program. The Solana equivalent of an ERC-20 token on Ethereum. SPL tokens are the standard token type used for token-gating on Solana.

price oracle
  An on-chain data feed that provides current market prices for tokens. Used in dollar-denominated token payment systems to calculate the token equivalent of a fixed dollar price at the moment of transaction.

accept-and-convert
  A payment strategy in which a business accepts token payments and immediately converts them to stablecoins or fiat currency. Preserves the demand-creation benefit of token payments while eliminating price risk.

composability
  The ability of separate systems or protocols to read and build on each other's data. Token-based utility is composable because multiple platforms can read the same on-chain wallet balance and enforce independent rules simultaneously.

role (Discord)
  A permission group in a Discord server. Token-gating platforms assign Discord roles to wallets that meet minimum balance requirements, and those roles control channel access and other server permissions.

portability (token benefits)
  The property of token-based benefits that allows them to transfer with the wallet rather than being tied to a user account controlled by a company. Token-based loyalty benefits are owned by the holder, not the platform.

Solana Pay
  An open payment specification: a URL and QR-code format (`solana:<recipient>?amount=…&spl-token=<mint>&label=…`) that any Solana wallet can scan to pay in SOL, USDC, or any SPL token, settling on-chain in under a second with no card network.
```

---

## 🔗 Key Tools Referenced

| Tool | Purpose | URL |
|------|---------|-----|
| **Collab.Land** | Discord and Telegram token-gating for Solana | collab.land |
| **Matrica** | Solana-native Discord and Telegram gating | matrica.io |
| **Phantom** | Solana wallet — used for member verification | phantom.com |
| **Solana Explorer** | Verify token mint address and holder balances | explorer.solana.com |

<!-- NEW IMAGES NEEDED: ch07-solana-pay-qr-flow.png (Solana Pay QR payment flow — request URL to QR code to Phantom mobile scan to on-chain settlement); ch07-gating-platforms.png (UPDATE existing image: comparison grid now shows only Collab.Land and Matrica); ch07-holder-setup.png (UPDATE existing image: Collab.Land Command Center TGR configuration instead of Holder.xyz dashboard) -->
