---
title: "Chapter 5: Give It a Market — Liquidity on Raydium"
subtitle: "How Automated Market Makers Turn Tokens into Tradeable Assets"
short_title: "Liquidity on Raydium"
description: "Understand what liquidity means, how automated market makers work using the constant product formula, and how to create a live trading pool for your token on Raydium using a $20 budget."
label: ch-05-liquidity-raydium
tags: [solana, raydium, liquidity, AMM, DeFi, trading, token]
---

# Chapter 5: Give It a Market — Liquidity on Raydium

:::{figure} ../images/ch05-explainer-infographic.png
:label: fig-ch05-explainer
:alt: Explainer infographic showing AMM liquidity pools, the constant product formula, and the Raydium platform on Solana
:width: 80%
:align: center

*Chapter 5 at a glance:* Liquidity pools, automated market makers, the x·y=k formula, and the Raydium interface — everything you need to open a market for your token.
:::

A baseball card locked in a drawer is not an asset. It has no price. Nobody can buy it. You cannot liquidate it in an emergency or profit from its rising fame. It is a trophy with no market. Your token is in that drawer right now.

You minted it. You launched it. Maybe you even designed an elegant tokenomics model in Chapter 4. But until someone other than you can *buy and sell it at any moment*, it remains a specimen in a jar — interesting, but inert. This chapter is about building the store. Except this store has no employees, never closes, runs on math, and sets its own prices in real time.

Welcome to liquidity on Raydium.

**▶ Deep Dive: Introduction to DeFi (31 min)**

:::{youtube} vocM1bRVZmg
:align: center
:::

## What Liquidity Actually Means

The word "liquidity" sounds like finance jargon, but the idea is almost physical. Imagine trying to sell a rare piece of art versus selling a dollar bill. The dollar bill sells instantly at a known price. The painting might take months, and the final price is uncertain. The dollar bill is *liquid*. The painting is *illiquid*.

For any asset — a stock, a currency, a token — liquidity has two components: **depth** (how much can be bought or sold without moving the price significantly) and **immediacy** (how fast a transaction can complete). A liquid market has both. An illiquid market has neither.

Why does this matter? Markets without liquidity die. Here is the death spiral: without liquidity, no serious buyer shows up because the price is too unpredictable. Without buyers, no seller wants to hold the asset. Without sellers, there is nothing to buy. The asset goes to zero not because it was worthless, but because nobody could agree on a price in real time.

:::{figure} ../images/ch05-liquidity-depth.png
:label: fig-ch05-liquidity-depth
:alt: Chart comparing a deep liquidity pool versus a shallow pool and the price impact of a trade in each scenario
:width: 80%
:align: center

*Pool depth matters:* A large pool absorbs trades without significant price movement; a thin pool produces wild price swings from even small transactions.
:::

Traditional financial markets solve this with **market makers** — firms like Citadel Securities or Virtu that continuously post buy and sell quotes, standing ready to transact at any moment. They profit from the spread (the gap between the price they will buy at and the price they will sell at) and from the volume. Their presence provides the liquidity everyone else relies on.

The catch: you cannot just call Citadel and ask them to make a market in your new token. They will not take your call.

This is the promise of decentralized finance — and specifically of the automated market maker.

## Order Books vs. Automated Market Makers

Traditional exchanges operate on **order books**. You go to a stock exchange and post a limit order: "I will buy 100 shares of Company X at \$47.50." Someone else posts: "I will sell 100 shares at \$47.50." When the prices match, the trade executes. The exchange is just the ledger that records the match.

Order books work well when there are many participants willing to constantly post and update orders. They work poorly for a brand-new token with three holders. You would post your buy order and wait. And wait. Eventually you would either give up or accept a terrible price.

The **automated market maker (AMM)** solves this by replacing the order book with a *pool of assets*. Instead of matching buyers with sellers, you match buyers and sellers with a pool of capital that is always available. The pool itself becomes the counterparty for every trade.

:::{figure} ../images/ch05-orderbook-vs-amm.png
:label: fig-ch05-orderbook-vs-amm
:alt: Side-by-side comparison showing how an order book matches buyers and sellers versus how an AMM pool serves as the counterparty for every trade
:width: 80%
:align: center

*Order book versus AMM:* Traditional markets match two humans; AMMs match any human with a pool of capital that is always open.
:::

Think of it like this: an order book is a farmer's market where buyers and sellers have to physically find each other and agree on a price. An AMM is a vending machine — stocked in advance, priced automatically, open at 3 AM on a Sunday. You do not need another human on the other side. You need capital in the machine.

This analogy holds up remarkably well — except the vending machine reprices itself after every single purchase, and the profit from every transaction goes to whoever stocked the machine in the first place.

## The Constant Product Formula: Two Piles of Coins

The magic behind every AMM — Uniswap, Raydium, Orca, and hundreds of others — is a single mathematical relationship so simple it fits on a napkin:

$$x \cdot y = k$$

Here is how to understand it without calculus. Imagine two piles of coins on a table. The left pile contains your token (let us call it LEARN). The right pile contains SOL. The formula says: **the product of the two piles must always equal the same number k.**

Suppose you start with 1,000 LEARN and 10 SOL on the table. That means k = 10,000. Now a student comes along and wants to buy some LEARN with their SOL. They add 1 SOL to the right pile, bringing it to 11 SOL. To keep the product equal to 10,000, the left pile must shrink: 10,000 ÷ 11 = approximately 909 LEARN. The student received 1,000 - 909 = 91 LEARN for their 1 SOL.

The implied price per LEARN before the trade: 10 SOL ÷ 1,000 LEARN = 0.01 SOL per LEARN.
The implied price per LEARN after the trade: 11 SOL ÷ 909 LEARN ≈ 0.0121 SOL per LEARN.

The price went up. Nobody decided that. The math decided it. As more LEARN leaves the pool (because buyers are buying), each remaining token becomes slightly more expensive. As more SOL enters, each token is backed by more SOL. Supply and demand, encoded in arithmetic.

:::{figure} ../images/ch05-constant-product-formula.png
:label: fig-ch05-constant-product
:alt: Visual illustration of the x times y equals k constant product formula using two coin piles that resize as trades occur
:width: 80%
:align: center

*The constant product formula in action:* Two piles of coins linked by the rule x·y=k. As one pile grows, the other shrinks, and the ratio between them determines the price.
:::

Where the analogy breaks down: the actual curve in the formula is a hyperbola — the prices do not shift linearly with trade size. Small trades barely move the price. Enormous trades move it dramatically. This non-linear relationship is what creates **slippage**, discussed shortly.

Where the analogy is revolutionary: this formula runs autonomously on a blockchain, 24 hours a day, for any token pair that has a pool, without any employee, broker, or exchange approval. You seeded that pool. You opened that market.

## Price Discovery: Why the Pool Wins

In the traditional world, price discovery is a complex negotiation between millions of buyers and sellers, mediated by exchanges and market makers, filtered through bid-ask spreads and clearing delays. In an AMM, price discovery is instantaneous mathematics.

But here is the subtler truth: the pool's price is not arbitrary. It is anchored to reality by **arbitrageurs** — traders who profit from price differences between markets.

Suppose the LEARN pool on Raydium shows 0.01 SOL per LEARN, but Jupiter's aggregated routing finds LEARN trading at 0.012 SOL on a second pool. An arbitrageur instantly buys LEARN from the cheap pool and sells it to the expensive one, pocketing the difference. This trading continues until both pools converge to the same price. The result: all pools stay roughly in sync with each other, and the aggregate price reflects the best available information about what the market values the token at.

You, as the creator, set the *opening* price by choosing how much SOL to pair with how many tokens when you initialize the pool. But from that moment forward, the market takes over. If you seed 1,000 LEARN against 10 SOL, you have declared the token worth 0.01 SOL each. Whether the market agrees is about to be revealed in real time.

:::{figure} ../images/ch05-price-discovery.png
:label: fig-ch05-price-discovery
:alt: Diagram showing how arbitrageurs link multiple liquidity pools to maintain consistent prices across AMM markets
:width: 80%
:align: center

*Arbitrage as the invisible hand:* When prices diverge across pools, traders immediately profit by bringing them back into alignment — keeping all AMMs in sync without any central coordinator.
:::

## Slippage, Pool Depth, and the Thin Liquidity Problem

Return to the two piles of coins. Suppose instead of 1,000 LEARN and 10 SOL, you started with only 100 LEARN and 1 SOL (the same ratio, k = 100). Now the same student arrives and adds 1 SOL. The pool now has 2 SOL. To maintain k = 100, LEARN drops to 50. The student received 50 LEARN for 1 SOL — a price of 0.02 SOL per LEARN instead of 0.01.

The pool price just doubled because the pool was *thin*. That is slippage: the difference between the price you expected and the price you actually received.

:::{admonition} Definition: Slippage
:class: note

**Slippage** is the difference between the quoted price when a trade is initiated and the actual execution price when the trade settles. In an AMM, slippage is a direct function of trade size relative to pool depth. A \$1 trade in a \$10 pool causes extreme slippage. A \$1 trade in a \$10,000 pool causes negligible slippage.
:::

For practical purposes, this means: if your pool is underfunded, large trades will punish buyers with terrible prices. Sophisticated traders will see the thin pool, flag it as risky, and stay away. Your market will remain illiquid not because nobody wanted to trade but because the economics of trading were too punishing.

The practical lesson: seed your pool with as much capital as you can reasonably afford. For a classroom exercise with \$20, you will have a thin pool — and that is exactly the point. You will *observe* slippage in action when you perform your swap at the end of the activity.

## LP Tokens and Fees: How Liquidity Providers Earn

When you deposit capital into an AMM pool, you do not simply hand over your tokens. The protocol gives you **LP tokens** (Liquidity Provider tokens) in return — a claim check that represents your proportional share of the pool.

Think of it like a coat check. You deposit your coat (your LEARN and SOL), you receive a ticket (LP tokens). When you want your coat back, you return the ticket and retrieve your deposit — plus any tips the coat-check staff collected on your behalf during the evening.

The "tips" in this case are **trading fees**. Every time anyone swaps through your pool, they pay a fee — typically 0.25% of the trade value on Raydium's Standard AMM pools. That fee is distributed proportionally to all LP token holders. You are not just providing charity; you are running a micro-exchange and earning a cut of every transaction that passes through it.

:::{figure} ../images/ch05-lp-tokens-fees.png
:label: fig-ch05-lp-fees
:alt: Diagram showing the LP token lifecycle: deposit assets, receive LP tokens, fees accumulate in the pool, withdraw with LP tokens plus earned fees
:width: 80%
:align: center

*The LP token lifecycle:* You deposit two assets, receive a proportional claim (LP token), earn fees from every trade, and eventually withdraw your original capital plus accumulated fees.
:::

There is a trade-off that every liquidity provider must understand: **impermanent loss**. When you provide liquidity, you hold both assets. If one asset's price rises dramatically relative to the other, you would have been better off just holding the rising asset. The pool automatically rebalanced against you — selling your winning asset to buy the losing one as the price moved. This loss is "impermanent" because it reverses if the price returns to where it started — but in practice, prices often do not return, and impermanent loss becomes very permanent.

For a classroom token with no external price anchor, impermanent loss is not a major concern. But for real DeFi liquidity provision with established tokens, it is the central risk/reward calculation every LP must make.

:::{dropdown} Deep Dive: Impermanent Loss Math
Suppose you deposit \$100 worth of LEARN and \$100 worth of SOL into a pool (50/50 split, standard for most AMMs). If SOL's price doubles while LEARN stays flat, arbitrageurs will drain your SOL from the pool, replacing it with LEARN, until the ratio reflects the new price. You now have more LEARN and less SOL than you started with — but LEARN did not appreciate. Your pool position is worth less than if you had simply held both assets separately.

The math: if one asset rises by 4x relative to the other, you lose approximately 20% versus a simple hold. The fee income must exceed that loss for LP provision to be profitable — which is why high-volume pools with thin price ratios (like stablecoin pairs) are often the most attractive LP positions.
:::

## Centralized Exchanges as Gatekeepers vs. Decentralized Rails

Here is a question worth sitting with: if you wanted to list your token on Coinbase, what would you do?

You would apply. Coinbase has a listing team. They would review your token for legal compliance, market cap, team background, trading volume, and a dozen other criteria. If they said no — and they almost certainly would for a classroom project — your token would not appear on Coinbase. Ever. Unless circumstances changed and you reapplied.

This gatekeeping is not arbitrary. Coinbase operates under securities regulations, knows-your-customer requirements, and has been sued for listing tokens that later turned out to be unregistered securities. Their caution is rational. But the practical effect is that any token interesting enough to be new and experimental is almost by definition excluded from centralized exchanges.

:::{figure} ../images/ch05-cex-vs-dex.png
:label: fig-ch05-cex-vs-dex
:alt: Comparison diagram contrasting CEX gatekeeper model with DEX permissionless access, showing listing requirements versus open pool creation
:width: 80%
:align: center

*The gatekeeper versus the open rails:* A centralized exchange requires approval, legal review, and market maker relationships. A DEX requires only a wallet and a funded pool.
:::

Raydium requires none of this. You connect a wallet with enough SOL to cover transaction fees and pool initialization, create the pool, seed it with capital, and your token is live. Permissionless means literally that — no permission is required from any authority.

Jupiter, Solana's leading swap aggregator, will automatically find your pool and include it in its routing algorithm. Within minutes of creating your pool, anyone with a Phantom wallet can swap into your token through Jupiter's interface — exactly the same interface they use to buy SOL, USDC, or any other Solana token. Your classroom project sits next to billion-dollar assets in the same routing engine.

Is this a feature? Is this a danger? We will return to that question at the end of the chapter.

## Activity: Open the Market

This is the core lab of Chapter 5. By the end, your token will be live and tradeable, you will hold an LP position, and you will have recorded an actual price-impact observation.

:::{admonition} What You Need
:class: important

- Your Phantom wallet from Chapter 1
- Your token mint address from Chapter 3
- At minimum \$20 worth of SOL in your wallet (more is better for meaningful liquidity)
- A small amount of your token in your wallet (you will pair it with SOL)
:::

### Step 1: Connect to Raydium

Navigate to [raydium.io](https://raydium.io) and connect your Phantom wallet using the **Connect Wallet** button in the top-right corner. Select your wallet and approve the connection. You should see your wallet address and SOL balance displayed.

### Step 2: The Liquidity Math — Three Scenarios

Before you touch any interface, do the math. Your opening price is determined entirely by the ratio of tokens to SOL you deposit. 

Work through all three scenarios in your notes, then choose one:

**Scenario A — 1 SOL, 10,000 tokens**
- Opening price: 1 SOL ÷ 10,000 LEARN = 0.0001 SOL per LEARN
- At SOL = \$150, that prices your token at roughly \$0.015 each
- k = 10,000 (the pool constant for future reference)

**Scenario B — 0.5 SOL, 1,000 tokens**
- Opening price: 0.5 SOL ÷ 1,000 LEARN = 0.0005 SOL per LEARN
- At SOL = \$150, that prices your token at roughly \$0.075 each
- k = 500

**Scenario C — 0.1 SOL, 100 tokens**
- Opening price: 0.1 SOL ÷ 100 LEARN = 0.001 SOL per LEARN
- At SOL = \$150, that prices your token at roughly \$0.15 each
- k = 10

:::{admonition} Math Observation
:class: note

Notice that your token "price" is entirely a function of the ratio you choose — not any intrinsic value. A token priced at \$0.15 each is not more valuable than one priced at \$0.015 each; the total market cap depends on supply, not unit price. This is worth internalizing: opening price is a strategic choice, not a discovery.
:::

**Record your chosen scenario and the resulting price in your lab notebook.**

### Step 3: Create the Standard AMM Pool

On Raydium, navigate to **Liquidity** → **Create Pool** → **Standard AMM**.

You will see two asset selector fields:

1. **Token A:** Select SOL
2. **Token B:** Paste your token mint address into the search field

Raydium will attempt to look up your token's metadata. If your token has a proper name and symbol (set in Chapter 3), it will display correctly. If it shows only the raw mint address, that is fine — it will still work.

Enter your chosen amounts from Step 2. The interface will display:
- Your initial price (ratio of SOL to your token)
- The initial pool reserve amounts
- An estimated fee tier

### Step 4: Select Your Fee Tier

Raydium offers multiple fee tiers for Standard AMM pools. For a new token with uncertain volume, **0.25%** is the standard choice. Higher fee tiers (0.5% or 1%) are more appropriate for very volatile pairs where LPs need compensation for impermanent loss risk.

For a classroom token, stick with 0.25%.

### Step 5: Initialize the Pool

Click **Initialize Pool**. Your Phantom wallet will prompt you to approve two transactions:
1. A setup transaction (typically small — under 0.01 SOL)
2. The actual liquidity deposit

Approve both. The total cost will depend on current Solana network fees but should be under \$1 in total transaction fees for the initialization, plus whatever SOL you deposited into the pool.

:::{figure} ../images/ch05-raydium-pool-create.png
:label: fig-ch05-raydium-create
:alt: Annotated screenshot walkthrough of the Raydium Standard AMM pool creation interface showing token selection, amount entry, fee tier, and the initialize button
:width: 80%
:align: center

*Creating your pool on Raydium:* Select your token pair, enter the amounts corresponding to your chosen scenario, confirm the opening price, and initialize.
:::

After the transactions confirm, Raydium will display your LP token balance. **Copy the pool address** — you will need it for your lab write-up.

### Step 6: Perform a Test Swap on Jupiter

Navigate to [jup.ag](https://jup.ag). Connect your Phantom wallet. 

In the swap interface:
- **You Pay:** SOL (use a small amount — 0.01 SOL is sufficient)
- **You Receive:** Search for your token by mint address

Jupiter will find your newly created Raydium pool and display a quoted rate. **Record the quoted price before executing the swap.**

Execute the swap. After it confirms, return to Jupiter and get a new quote for the same trade. **Record the new quoted price.**

You have just observed slippage and price impact in a live market. The price moved because your pool is small and the trade consumed a meaningful percentage of the pool's depth.

:::{figure} ../images/ch05-jupiter-swap.png
:label: fig-ch05-jupiter-swap
:alt: Annotated diagram of the Jupiter swap interface showing the token input, output, price quote, and slippage indicator for a newly created token
:width: 80%
:align: center

*Your token on Jupiter:* After pool creation, Jupiter automatically routes trades through your pool. The price shown is derived directly from the constant product formula applied to your pool's current reserves.
:::

### What to Record in Your Lab Notebook

| Item | Value |
|------|-------|
| Token mint address | |
| Pool address on Raydium | |
| Scenario chosen (A/B/C) | |
| Opening price (SOL per token) | |
| Opening price (USD per token at current SOL price) | |
| SOL deposited | |
| Tokens deposited | |
| k value (SOL × tokens) | |
| LP token amount received | |
| Quoted price BEFORE test swap | |
| Quoted price AFTER test swap | |
| Price impact percentage | |

### Verify Your Pool on Solscan

Navigate to [solscan.io](https://solscan.io) and search for your pool address. You should see the pool's transaction history, current reserves, and the liquidity add event from your initialization. This is your pool's permanent, public, immutable record.

## Reading Your Position Over Time

Your LP position has a live value. If you return to Raydium's liquidity dashboard, you will see your pool listed under **My Positions**. It will show:
- Current total value of the pool
- Your percentage ownership (since you own 100% — you are the only LP)
- Accumulated fees (likely \$0.00 for now, until others trade through your pool)
- Any impermanent loss (will be minimal for a classroom token with low external price movement)

:::{figure} ../images/ch05-lp-position.png
:label: fig-ch05-lp-position
:alt: Diagram showing the Raydium LP position dashboard with pool value, ownership percentage, accumulated fees, and impermanent loss indicator
:width: 80%
:align: center

*Your LP dashboard on Raydium:* Track your pool's value, ownership stake, fee earnings, and impermanent loss in real time — all from on-chain state, no trusted third party required.
:::

## The Broader Picture: What You Just Built

Take a moment to understand what just happened. You created a functioning financial market from scratch, on a global network, in about 20 minutes, for less than \$20 in capital plus a few cents in transaction fees.

The pool you created will:
- Accept trades 24 hours a day, 365 days a year
- Price those trades algorithmically, without your involvement
- Distribute fees to you as the LP
- Remain accessible to any wallet in the world

In 2000, building a trading market for a new financial instrument required a broker-dealer license, a registered exchange, clearing relationships, market-maker agreements, compliance staff, and millions of dollars in capital. The shortest path was years, not hours.

:::{figure} ../images/ch05-defi-market-creation.png
:label: fig-ch05-defi-market
:alt: Timeline comparison showing the years and millions required to launch a traditional financial market versus the hours and dollars required to launch a DeFi AMM pool in 2024
:width: 80%
:align: center

*Compressed market creation:* What required regulatory approvals, exchange listings, and market-maker agreements for legacy finance now takes a wallet, a small capital allocation, and a few on-chain transactions.
:::

Is this revolutionary? Undeniably. Is it dangerous? That depends entirely on who you ask — and perhaps on which side of the trade you are on.

## 🎯 In-Class Assignment: Open Your Market (10 pts)

**Details and instructions will be provided in class.**

**Points:** 10

## Discussion: Feature or Danger?

:::{admonition} Discussion Prompt
:class: important

With \$20 you created a market and set an opening price for a financial asset. On Wall Street, this would require licenses, exchanges, registered market makers, and potentially years of regulatory approval. 

**Is the ease of AMM market creation a feature or a danger — and does your answer change depending on whether you are the creator or the buyer?**

Consider: the same infrastructure that allows a student to create a learning exercise also allows a fraudster to create a pump-and-dump scheme. The pool does not know the difference. The math does not ask about intent.
:::

### Discussion Guidelines

Write a substantive response (minimum 250 words) that takes a clear position on the feature-versus-danger question. Your response should:

- Distinguish between the perspective of the creator (who controls the initial liquidity and token supply) and the perspective of the buyer (who has no insight into the creator's intentions)
- Include at least one scholarly or credible citation — this could be an academic paper on DeFi market manipulation, a regulatory filing, a journalistic investigation of a rug pull, or a legal analysis of AMM governance
- Avoid purely descriptive answers — argue for a position, acknowledge the strongest counterargument, then defend your view

After posting your initial response, **reply to at least two classmates** with substantive engagement — not just "I agree." Push back on assumptions, introduce evidence they may have missed, or extend their argument into a domain they did not consider.

Do not describe small-group debate formats or in-class discussion structures — this is an individual written assignment.

## Glossary

```{glossary}
Liquidity
  The ease with which an asset can be bought or sold at a stable price. High liquidity means large trades can occur without significant price movement; low liquidity means even small trades can cause dramatic price swings.

Automated Market Maker (AMM)
  A type of decentralized exchange protocol that uses mathematical formulas — rather than order books — to price assets and execute trades. The pool of capital is the counterparty for every transaction.

Constant Product Formula
  The mathematical rule x·y=k that governs most AMMs. The product of the two token reserves in a pool must remain constant, which means that as one reserve decreases, the other increases proportionally, causing the price ratio between them to shift.

Pool Depth
  The total value of assets locked in a liquidity pool. Deeper pools produce less slippage for a given trade size; shallower pools produce more.

Slippage
  The difference between the expected price of a trade and the actual executed price. In AMMs, slippage increases with trade size relative to pool depth.

LP Token
  A token issued to a liquidity provider representing their proportional share of a pool. LP tokens can be redeemed to withdraw the underlying assets plus any accumulated fees.

Impermanent Loss
  The opportunity cost experienced by liquidity providers when the price ratio between the two pooled assets changes from the ratio at the time of deposit. The loss is "impermanent" only if prices return to their original ratio.

Price Impact
  The effect of a trade on the quoted market price within a pool. Large trades in small pools produce high price impact; small trades in large pools produce negligible impact.

Fee Tier
  The percentage of each trade's value charged as a fee and distributed to liquidity providers. Common tiers are 0.01%, 0.05%, 0.25%, and 1%.

Price Discovery
  The process by which a market determines the fair value of an asset through the interaction of supply and demand. In AMMs, price discovery is maintained through arbitrage trading that links pools across platforms.

Arbitrageur
  A trader who profits from price differences between markets, simultaneously buying from the cheaper source and selling to the more expensive one. Arbitrageurs keep AMM prices aligned with each other and with external markets.

Raydium
  A major decentralized exchange and AMM protocol on the Solana blockchain. Raydium is notable for combining on-chain AMM pools with access to Serum's central limit order book, and for its integration with the Jupiter aggregator.

Jupiter
  Solana's leading swap aggregator, which finds the best available price across all DEX pools on the network and routes trades accordingly. Any pool created on Raydium is automatically accessible through Jupiter.

Permissionless
  Describing a system that any participant can access without approval from a gatekeeper. AMM pool creation is permissionless — no exchange approval, no license, no regulatory filing is required.

Standard AMM
  Raydium's basic pool type, which implements the constant product formula. Suitable for most token pairs, including newly launched tokens with limited price history.
```

## Leader's Takeaway

Markets are infrastructure. Before AMMs, the infrastructure required to run a market was so expensive and regulated that it was accessible only to established financial institutions. The constant product formula changed that: any token with a funded pool has a market.

The implications extend beyond cryptocurrency. Any asset that can be tokenized — real estate, carbon credits, intellectual property, event tickets — can in principle have a permissionless AMM market. The question shifts from "can we build a market for this?" to "should we? And if so, who bears the risk when the pool is thin and the price is set by a single creator?"

Your \$20 pool is not just a classroom exercise. It is a demonstration of a technology that will force regulators, financial institutions, and entrepreneurs to confront the same question you will explore in your discussion post: when markets become as easy to create as web pages, what does market integrity actually mean?

## Walk Away With

After completing this chapter's activity, you have:

- ✅ A live, tradeable token with a real market price on Raydium
- ✅ An LP position earning fees from every trade through your pool
- ✅ A recorded price-impact observation from your Jupiter test swap
- ✅ A working understanding of the constant product formula and its implications for pool depth and slippage
- ✅ A framework for thinking about permissionless markets as infrastructure — and the risks that come with removing gatekeepers

In Chapter 6, you will decide who gets your token and how they get it — designing the distribution strategy that turns a live asset into a functioning token economy.
