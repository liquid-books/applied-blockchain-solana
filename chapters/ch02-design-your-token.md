---
title: "Design Your Token Like a Business, Not a Coin"
subtitle: "A Token Is a Business Model Made Transferable"
short_title: "Design Your Token"
description: "Most tokens die because they were designed as money. This chapter teaches you to design a token from business first principles — what it represents, who holds it and why, what supply signals to the market, and why your name and symbol are permanent business decisions."
label: ch-02-design-your-token
tags: [token design, tokenomics, fungible, non-fungible, loyalty programs, NAAT, supply, utility, access, ownership, reputation]
---

# Design Your Token Like a Business, Not a Coin

:::{figure} ../images/ch02-explainer-infographic.png
:label: fig-ch02-infographic
:alt: Illustrated explainer infographic showing the four token types (payment, access, ownership, reputation), the fungible vs. non-fungible spectrum, the NAAT framework applied to token design, and supply models
:width: 80%
:align: center

**Chapter 2 Explainer Infographic:** The complete map of token design thinking — from the four things a token can represent, to supply as a signal, to the "why would anyone want this" test.
:::

Most tokens die because they were designed as money.

This is not a metaphor. Hundreds of billions of dollars have been created, launched, and lost by teams that looked at the blockchain primitive — a cryptographically secured, transferable unit of digital value — and asked: *What if we made money with this?* The answer, in almost every case, is ruin. Because money is the hardest thing in the world to design. Governments with armies and tax authorities and centuries of institutional trust have spent millennia building money, and most of them have gotten it wrong at some point.

You are not a government. And you do not need to make money.

Here is what nobody tells you in the pitch decks: airline miles are worth more than most cryptocurrencies. The United Airlines MileagePlus program has been valued at approximately \$22 billion — more than United Airlines itself was worth at certain points during the COVID pandemic. The Starbucks Rewards program has over 34 million active members who collectively hold billions of unredeemed Stars. Dave & Buster's Power Card is a token. A Barnes & Noble gift card is a token. Stock certificates are tokens. Casino chips are tokens.

None of these were designed as money. All of them are extraordinarily successful token economies.

The difference between a dead coin and a thriving token economy is not the blockchain. It is not the tokenomics spreadsheet. It is not the whitepaper. It is whether the designer answered, honestly and in advance, a single question: *Why would anyone want this?*

This chapter is about how to answer that question before you launch anything.

---

## The Four Things a Token Can Represent

:::{figure} ../images/ch02-four-token-types.png
:label: fig-ch02-four-types
:alt: Four-quadrant diagram showing the four token types — payment, access, ownership, and reputation — with real-world examples in each quadrant
:width: 80%
:align: center

**The Four Token Types:** Every token represents one or more of these four things. The most durable token economies pick one primary representation and design everything else around it.
:::

When you strip away the marketing language — the "revolutionary decentralized ecosystems" and "frictionless value transfer protocols" — a token can represent exactly four things. Understanding which one your token represents is the first design decision, and it shapes every subsequent one.

### Payment

A payment token is designed to function as a medium of exchange. You hold it because you intend to spend it, and you accept it because you trust that others will also accept it. Bitcoin, at its most idealized, is a payment token. So is the dollar in your pocket.

Payment tokens are extraordinarily difficult to bootstrap. To function as a medium of exchange, a token must have *liquidity* (enough buyers and sellers that you can trade it without large price impact), *acceptance* (enough merchants or counterparties willing to take it), and *stability* (enough price consistency that holding it for a week does not destroy or multiply your purchasing power by 30%). Liquidity requires acceptance, which requires stability, which requires liquidity. This circular dependency is why most payment tokens fail.

:::{admonition} The Payment Token Trap
:class: warning

If your answer to "what does the token represent?" is "it's a currency for our ecosystem," stop. That answer is technically accurate for almost any token but strategically empty. Who accepts it? For what? At what price? These are the questions that payment tokens require you to answer — and that most founders cannot answer until they already have a network with tens of thousands of active participants. Design payment characteristics *into* a token that primarily represents something else; do not start there.
:::

The most successful "payment" tokens in practice are not payment-first: they are utility tokens or governance tokens that happen to be liquid enough to use as payment within a specific context. SOL, the native token of Solana, is technically a payment token — but its primary use case is paying transaction fees, which makes it, functionally, an *access* token.

### Access

An access token grants the holder the right to use something — a product, a service, a community, a dataset, an API. The holder's motivation for holding is simple: I want to use the thing this token lets me use. The holder's motivation for spending is also simple: when I no longer need access, or when a better access opportunity presents itself, I sell.

Access tokens are easier to design than payment tokens because the value proposition is concrete. A token that gives you access to a private Discord community with genuine alpha is worth what that alpha is worth to you. A token that gives you access to \$10,000 worth of compute per month is worth up to \$10,000 per month to someone who needs that compute. The value is not speculative — it is functional.

The risk with access tokens is over-issuance. If you create 1 billion tokens and only 1,000 users ever want access, 999,000,000 tokens are permanently worthless. Supply is a design variable. We will return to it.

**Real example:** Helium Mobile subscribers use MOBILE tokens to pay for wireless coverage. The token is not pretending to be general-purpose money. It is an access pass to a specific physical resource — cellular data — provided by a decentralized network of hardware operators. The business logic is clear: if you want coverage, you need the token. If you provide coverage, you earn the token.

### Ownership

An ownership token represents a fractional or full claim on an asset — a piece of real estate, a revenue stream, a company's future earnings, a piece of intellectual property. The holder's motivation for holding is the underlying asset's performance. The holder's motivation for selling is to realize gains or exit the position.

Ownership tokens are the most legally fraught category because they closely resemble securities. A token that represents a right to future profits is, in most jurisdictions, a security — which means it is subject to securities law, registration requirements, and investor protection regulations. We will cover this in depth in Chapter 12. For now, understand that ownership tokens require the most legal diligence and the clearest answer to "what exactly does this token entitle me to?"

The most interesting ownership tokens in 2025-2026 are real-world asset (RWA) tokens: fractional ownership of private credit, treasury bills, commercial real estate, and infrastructure assets. Tokenized private credit on Solana has grown to over \$400 million in assets under management, with Maple Finance and Credix running institutional-grade lending pools whose shares are on-chain tokens. These tokens represent specific, legally documented ownership claims — not speculative hope.

### Reputation

A reputation token represents earned standing in a community or system. It cannot be purchased — it must be earned through behavior that the system values: contributions, expertise, longevity, accuracy. The holder's motivation for holding is status and the privileges that come with it. The holder's motivation for *not* selling is that if they sell, they lose the status they earned.

Reputation tokens are the most underbuilt category and arguably the most interesting. Stack Overflow points are a reputation token — non-transferable, earned through quality contributions, granting access to moderation privileges and professional credibility. Gitcoin Passport scores are a reputation token, earned through on-chain behavior and off-chain verifications, granting eligibility for quadratic funding rounds.

The design challenge with reputation tokens is that once they become transferable and purchasable, they cease to function as reputation systems. A credential you can buy is not a credential — it is a costume. The best reputation token designs are either non-transferable (soulbound tokens, in Ethereum terminology) or deliberately difficult to use as currency because the cost of liquidating your reputation exceeds the market price.

:::{admonition} Most Tokens Use More Than One Category
:class: tip

The most durable token economies combine categories strategically. A governance token (ownership-adjacent: you own a vote in the future direction of the protocol) that also grants access to premium features is harder to dismiss than a pure governance token. A loyalty token that grants access to exclusive events *and* can be redeemed against future purchases combines access and payment in a virtuous way. The four categories are a design lens, not four mutually exclusive boxes.
:::

---

## Fungible vs. Non-Fungible: Casino Chips and Concert Tickets

:::{figure} ../images/ch02-fungible-nonfungible.png
:label: fig-ch02-fungibility
:alt: Side-by-side comparison of fungible tokens (casino chips) and non-fungible tokens (concert tickets) showing interchangeability vs. uniqueness, with examples of each
:width: 80%
:align: center

**Fungibility in Practice:** Casino chips of the same denomination are perfectly interchangeable — any \$100 chip is worth exactly \$100. Concert tickets are unique — seat 14B in Row C for Saturday's show is not the same as seat 14B in Row C for Sunday's show, even if the face value is identical.
:::

Before you decide what your token represents, you need to decide whether your token is *fungible* or *non-fungible*. This is not a technical decision — it is a business decision. The technology follows.

**Fungible** means interchangeable. One unit is identical to every other unit. My \$100 casino chip is worth exactly the same as your \$100 casino chip — I do not care which specific chip I am holding, only what it is worth. This is how currency works, how stocks work, and how most tokens work. On Solana, fungible tokens are SPL tokens — the format we will launch in Chapter 3.

**Non-fungible** means unique. My ticket to seat 14B, Row C, at the Saturday night performance of a specific show is not the same as your ticket to seat 15A, Row D, for the Sunday matinee. Even if both tickets cost the same, they represent different things. You cannot swap them without both parties agreeing, and even then, one party might prefer their original. On Solana, non-fungible tokens are NFTs — each has a unique identifier that makes it distinct from every other token, even those that are otherwise identical in appearance.

The business question is: *Does each unit of your token need to be distinguishable from every other unit?*

For a loyalty point system where 1 point = 1 point, fungibility is correct. You do not care which specific Star you are redeeming at Starbucks — only that you have enough of them. For a membership that grants access to a specific community tier, or a certificate of completion for a specific course, or a title to a specific piece of real estate, non-fungibility is correct because the specific token *is the asset* — not merely a unit of account.

:::{admonition} Where the Analogy Breaks Down
:class: note

Casino chips are fungible within a denomination but non-fungible across denominations — a \$100 chip and a \$25 chip cannot be swapped. Some of the most interesting token designs create *semi-fungible* tokens: batches where tokens within the batch are interchangeable (fungible), but tokens across batches are distinguishable (non-fungible). The ERC-1155 standard on Ethereum formalized this. Solana's compressed NFTs and programmable NFTs support similar patterns. For your first token economy, pick one: pure fungible SPL token, or pure NFT. The hybrid cases are fascinating but belong in Chapter 9.
:::

---

## Loyalty Programs as the Original Token Economy

Before blockchain, before smart contracts, before Satoshi's whitepaper, loyalty programs were already running token economies at global scale. And they were getting most of the design decisions right.

:::{figure} ../images/ch02-loyalty-token-comparison.png
:label: fig-ch02-loyalty
:alt: Infographic comparing Starbucks Rewards as a traditional loyalty token economy versus the same system reimagined on-chain, showing issuance, redemption, value discovery, and composability differences
:width: 80%
:align: center

**Starbucks Rewards vs. On-Chain Loyalty:** The core economic design is identical — earn tokens by purchasing, spend tokens for rewards. The blockchain version adds composability (use Stars at partner businesses), transparency (auditable issuance), and user control (no expiration by corporate fiat).
:::

Consider the Starbucks Rewards program in detail, because it is a token economy designed by people who were trying to run a business — not launch a coin.

**Issuance:** Stars are issued when you make a purchase. Every \$1 spent earns a fixed number of Stars. The supply of Stars grows as the network (Starbucks purchases) grows — but the growth rate is controlled by the earn rate, which Starbucks can adjust. This is *managed inflation*: supply grows, but in direct proportion to economic activity.

**Redemption:** Stars are redeemable for specific rewards at specific quantities: 25 Stars for a customization, 100 Stars for a brewed coffee, 200 Stars for a handcrafted drink. The redemption schedule is the *price list* for the token. When Starbucks changes the redemption schedule (which they do periodically, almost always upward in cost), they are engaging in *effective deflation* — your existing Stars purchase less. This is a business decision with economic consequences that Starbucks can execute unilaterally.

**Expiration:** Stars expire after six months of inactivity. This is a *velocity mechanism* — it encourages holders to spend (by forcing them to earn regularly to keep their balance active) and it allows Starbucks to reduce its liability for unredeemed Stars. From a token design perspective, it is a form of demurrage: holding the token long-term has a cost.

**Portability:** Starbucks Stars are non-transferable, non-tradeable, and usable only at Starbucks. This maximizes Starbucks's control and prevents the emergence of a secondary market that could undermine the program. But it also means Stars have zero value outside the Starbucks ecosystem — a design choice that benefits Starbucks and constrains holders.

Now imagine the same economic design on-chain:

- Stars are SPL tokens on Solana, issued to your wallet address when you buy coffee (via a point-of-sale integration that calls a Solana program)
- Redemption burns Stars and triggers a fulfillment event — the record is on-chain, auditable by anyone
- Stars are *transferable* — you can give your Stars to a friend, sell them on a secondary market, or deposit them into a DeFi protocol that accepts them as collateral
- Composability — a third-party coffee shop can choose to accept Starbucks Stars at a set conversion rate, creating a *network effect* that Starbucks cannot unilaterally control

The on-chain version is more powerful for the holder and less controllable for the issuer. This is the fundamental trade-off that every token designer faces: decentralization transfers control from issuer to holder. Sometimes that is the goal. Sometimes it is a liability.

**The design insight:** Starbucks Rewards succeeds because the token represents something specific and concrete (coffee-buying activity), the earn and spend mechanisms are clear, and the value proposition for the holder is genuine (free drinks). The blockchain version succeeds or fails for identical reasons. The technology does not create the value — the business model does.

---

## The NAAT Framework Applied to Token Design

You built a NAAT Canvas in Chapter 0 — a map of your Network, Actors, Assets, and Transactions. Now we apply it specifically to token design. Every token lives inside a NAAT architecture, and the NAAT lens reveals exactly where token designs fail.

:::{figure} ../images/ch02-naat-token-design.png
:label: fig-ch02-naat
:alt: The NAAT framework canvas applied to token design, showing how Network, Actors, Assets, and Transactions map to token issuance, holder incentives, spend mechanics, and velocity
:width: 80%
:align: center

**NAAT Applied to Tokens:** A token is not an asset in isolation — it is the asset layer of a NAAT architecture. Every design failure can be traced to a breakdown in one of the four quadrants.
:::

### The Core NAAT Token Rule

Every actor in your token economy must have **a reason to hold** and **a reason to spend**. If an actor has a reason to hold but no reason to spend, you get hoarding — tokens accumulate but do not circulate, and the economy freezes. If an actor has a reason to spend but no reason to hold, you get velocity collapse — tokens are sold the moment they are earned, and price goes to zero.

Let us walk through a failing token design using NAAT:

**Scenario:** A startup launches a governance token for a decentralized protocol. There are three actor types: investors (who bought the token in a private sale), team members (who received tokens as compensation), and users (who use the protocol).

- **Investors:** Reason to hold? The token might appreciate. Reason to spend? None — voting in governance is not worth the gas/effort, and there are no other spend mechanisms. **Result:** Investors hold until they can sell.
- **Team members:** Reason to hold? Vesting schedule prevents selling in the near term. Reason to spend? None. **Result:** Team members sell when vesting cliffs hit.
- **Users:** Reason to hold? None provided. Reason to spend? They were not given tokens in the first place. **Result:** Users never engage with the token economy.

The NAAT analysis reveals: this token economy has no virtuous loop. The only rational behavior for every actor type is to sell. The token price trajectory is predetermined.

Now contrast with a working design:

**Scenario:** A creative platform issues a token to content creators when their work is purchased. Collectors can use tokens to unlock creator-specific perks. Creators can stake tokens to earn a share of platform fee revenue.

- **Collectors:** Reason to hold? Appreciation value + access to perks they want. Reason to spend? Unlock specific perks that require token burn.
- **Creators:** Reason to hold? Staking rewards + status signaling (large creator stakes imply confidence in the platform). Reason to spend? N/A — creators earn, do not typically spend.
- **Platform:** Issues tokens as payment for creator contributions. Burns tokens on perk redemption. Net issuance is controlled by the volume of creator activity minus redemption burns.

The NAAT analysis reveals: collectors and creators both have reasons to hold, and collectors have a reason to spend (perk redemption). The spend mechanism creates a deflationary pressure that counterbalances issuance. This is a token economy with internal logic.

:::{admonition} The NAAT Token Checklist
:class: tip

Before finalizing any token design, run this check:

1. List every actor type in your network (buyer, seller, provider, consumer, governance participant, etc.)
2. For each actor: what is their primary reason to hold the token?
3. For each actor: what is their primary reason to spend (or never sell) the token?
4. If any actor has no reason to hold, or no mechanism to get the token in the first place: the design is incomplete.
5. Is there at least one virtuous loop? (Holding creates value → spending creates value for others → those others want to hold → cycle repeats)
:::

---

## Supply as a Design Decision

:::{figure} ../images/ch02-supply-models.png
:label: fig-ch02-supply
:alt: Four-panel diagram comparing fixed supply, inflationary supply, deflationary supply, and hybrid supply models with real-world examples and trade-offs for each
:width: 80%
:align: center

**The Four Supply Models:** Supply is not a parameter to fill in — it is a signal about the economic relationship between issuer and holder. Each model makes a different promise to the market.
:::

When you create a token on Solana, you set a total supply and a mint authority. The mint authority is the address that can create new tokens. If you revoke the mint authority (destroying the ability to create more tokens forever), you have created a *fixed supply* token. If you keep it, you retain the ability to issue more.

This decision is not technical. It is a promise to your holders about the future of the token's supply — and promises in token design are binding in ways that company policies are not.

### Fixed Supply

A fixed supply token commits to a maximum number of units that will ever exist. Bitcoin's 21 million coin limit is the canonical example. The promise is: I will never dilute your holdings by printing more.

**What fixed supply signals:** Confidence that the current distribution is fair and complete, and that the token's value will be determined by demand against a stable denominator. Fixed supply is appropriate when the token is primarily an ownership representation (you own a fixed percentage of a fixed total) or a store of value claim.

**The risk:** If adoption grows faster than expected, fixed supply creates price appreciation that rewards early holders but prices out late adopters. This can create distributional inequity that undermines network effects. Many fixed-supply tokens become plutocracies where early holders have permanently outsized influence.

**Fixed supply works when:** The token is designed for ownership or value storage, the initial distribution is genuinely fair, and the community accepts that late adoption means paying market price for existing tokens.

### Inflationary Supply

An inflationary token mints new tokens continuously, typically as rewards for desired behavior: staking, liquidity provision, content creation, protocol usage. The promise is: if you contribute to this network, you will be rewarded with tokens.

**What inflationary supply signals:** This economy is growing, and growth is being funded by token emissions. Come participate, and you will be paid in tokens that (we believe) will have future value.

**The risk:** If the rate of token emission exceeds the rate at which the ecosystem creates genuine value, the token price declines. This is the *hyperinflation scenario* — more tokens chasing the same (or less) underlying value. Axie Infinity's SLP token is the cautionary tale: emission was designed to reward gameplay, but when the player count stalled, unabsorbed token supply crushed the price by over 99%.

**Inflationary supply works when:** The behaviors being rewarded are genuinely value-creating (not just "play our game"), the emission rate is controlled and declining over time (like Bitcoin's halvings — still technically inflationary but at a decreasing rate), and there are meaningful token sinks (spend mechanisms that remove tokens from circulation).

### Deflationary Supply

A deflationary token burns tokens permanently as they are spent. Every transaction or redemption removes tokens from circulation. If the burn rate exceeds the mint rate, the total supply decreases over time.

**What deflationary supply signals:** The more this network is used, the scarcer the token becomes. If you believe in this network's growth, holding the token is the rational choice.

**The risk:** Deflation encourages hoarding. Why spend a token today if it will be worth more tomorrow? The Paradox of Thrift, applied to token economies: if everyone holds in anticipation of appreciation, no one spends, and the velocity collapses. A token economy with zero velocity is not an economy — it is a collectible.

**Deflationary supply works when:** The primary value of the token is as a store of value or investment (Bitcoin, arguably), or when there is a forced spend mechanism that prevents pure hoarding (like expiring access rights that require periodic token renewal).

### Hybrid Supply

Most successful long-running token economies use hybrid models: a fixed total supply with time-released emission schedules (creating initial inflationary pressure that decreases as the schedule exhausts itself), combined with burn mechanisms that create deflationary pressure from usage. Solana's SOL token has inflationary staking rewards that decrease at approximately 15% per year until they reach a steady state of 1.5% annual inflation — designed to reward early validators while preventing permanent dilution.

**The design principle:** Your supply model is a *commitment mechanism*. The market will hold you to it. If you promise a fixed supply and then mint more tokens (as many projects have done via "emergency" measures), you will destroy trust permanently. Design the supply model you can commit to, not the one that looks best on a whitepaper slide.

---

## Name, Symbol, Decimals, and Metadata: Why Permanence Makes These Business Decisions

:::{figure} ../images/ch02-token-identity.png
:label: fig-ch02-identity
:alt: Infographic showing the components of on-chain token identity — name, symbol, decimals, image URI, and extended metadata — with examples of good and poor choices for each
:width: 80%
:align: center

**Token Identity on Solana:** Every field in your token's metadata is permanent and publicly visible. These are not placeholders — they are your first public business decisions.
:::

When you deploy a token on Solana (Chapter 3 will walk you through the exact steps), you set five attributes that are extremely difficult to change later:

**Name** — The full name of the token (e.g., "USD Coin," "Wrapped SOL," "Bonk"). This appears in wallet interfaces, block explorers, and DEX listings. It is your token's legal name in the informal economy of token markets. Choose it like you would choose a company name: for clarity, for brand alignment, for the impression it creates. Generic names ("Utility Token," "Community Coin") signal a lack of conviction. Gimmick names signal a lack of seriousness. A clear, purposeful name — one that tells you exactly what the token is for — signals good design.

**Symbol** — The ticker (e.g., USDC, WSOL, BONK). Three to five characters, all caps by convention. Your symbol is how traders and protocols reference your token. Once you have any trading volume, changing the symbol is effectively impossible without losing your market history. Choose something memorable, clearly distinct from existing major tokens, and aligned with your name.

**Decimals** — How divisible the token is. SOL has 9 decimal places, meaning the smallest unit of SOL is 0.000000001 SOL (called a lamport). USDC has 6 decimal places. Most SPL tokens use 6 or 9. If your token represents something indivisible — a membership pass, a voting right, a single certificate — you might use 0 decimals. If it represents a currency or commodity that should be finely divisible, use 6 or 9.

This is a business decision masquerading as a technical parameter. If you create a token with 0 decimals and a supply of 10,000, you are saying: there will be exactly 10,000 of these, ever, and each one is a complete, indivisible unit. If you create a token with 9 decimals and a supply of 1,000,000,000 (plus nine decimal places), you are creating 1 quintillion minimum units — effectively unlimited for most practical purposes. The decimals setting shapes how users think about the token. Round, memorable numbers matter.

**Metadata URI** — A link to a JSON file containing your token's image, description, and extended attributes. On Solana, this is typically stored on IPFS, Arweave, or a centralized server. The image at this URI is what wallets and marketplaces display as your token's icon. The description is what users read when they hover over your token. This metadata is your token's marketing material at the point of first contact.

**Mint Authority** — After launch, the most consequential metadata decision is whether to revoke the mint authority. Revoking it signals commitment to fixed supply. Keeping it signals that more tokens might be issued. Many token launches have been criticized for retaining mint authority "just in case" — the market interprets this as a willingness to dilute, which suppresses price. If you are committed to fixed supply, revoke the authority publicly and document it. This is a trust signal.

:::{admonition} The Permanence Principle
:class: important

On a public blockchain, every transaction is permanent. This means your initial token name, symbol, and supply are effectively permanent — not because the code prevents changes (technically, some metadata can be updated), but because the *history* of what you launched with is on-chain forever. If you launch with an unfortunate name and change it six months later, every block explorer will show the original name in the transaction history. Design for permanence from day one.
:::

---

## The "Why Would Anyone Want This?" Test

:::{figure} ../images/ch02-why-would-anyone-want-this.png
:label: fig-ch02-want-test
:alt: Decision flowchart for the "why would anyone want this?" test — branching through holder motivation, spend mechanism, network effects, and supply model to reach a pass/fail verdict
:width: 80%
:align: center

**The "Why Would Anyone Want This?" Test:** The most important quality filter in token design. If you cannot answer this for each actor type in your network, the token is not ready to launch.
:::

Before you write a single line of code, before you fill out a single form on a token launch platform, you must be able to answer this question for every actor in your token economy:

*Why would [specific actor type] want to hold this token? And what would make them want to spend it?*

Not in general. Not in the abstract. For each specific type of participant in your system, with specific, concrete answers.

Here are the most common failure patterns, and how the test catches them:

**Failure Pattern 1: "People will want it because it will go up in value."**

This is circular. The token goes up in value if people want it. If the only reason people want it is because it will go up in value, you have described a Ponzi scheme. The test requires you to answer: what does the token *do* for the holder, independent of its market price?

**Failure Pattern 2: "Holders get governance rights."**

Who is governing? Over what? With what stakes? If the protocol is small, the governance rights are worth very little. If the protocol is large but the governance token has no other utility, the token's value is entirely determined by expected future value of governance — which is circular again. Governance rights are a *supplement* to value, not the source of it.

**Failure Pattern 3: "Users will need the token to use the platform."**

This is stronger — it establishes demand from usage. But the follow-up question is critical: *How do users acquire the token?* If users must go to a DEX and buy the token before they can use your platform, you have created friction that will cost you 90% of your potential user base. The best-designed access token systems either give users the first batch of tokens free (onboarding subsidy), let them earn tokens through the behaviors you want to encourage, or integrate payment in fiat and convert to tokens invisibly.

**Failure Pattern 4: "Our community will support the token."**

Communities support what provides them value. The question is not whether your community will support the token at launch — early communities often do, out of enthusiasm. The question is whether the token design gives the community a *reason to hold* once the initial enthusiasm fades. Sustainable token economies do not rely on community support to suppress selling — they rely on economic incentives that make holding rationally superior to selling.

When your token design passes the "why would anyone want this?" test, you will be able to say, for each actor type in your network, something like:

*Creators want to hold CreatorToken because staking 1,000 tokens gives them a 5% fee discount on all transactions, which saves them more money per month than the tokens are worth. They want to spend CreatorToken to unlock premium analytics dashboards that cost 200 tokens per month — an expenditure that makes sense because the dashboard insights help them earn more from their content.*

That is a passing answer. It is specific, it is economic, and it does not depend on circular price appreciation.

---

## Activity: Write Your Token Brief

:::{figure} ../images/ch02-token-brief-template.png
:label: fig-ch02-brief
:alt: Token brief template showing the five sections — token representation, actor table with hold/spend reasons, supply model, name/symbol/decimals, and 100–200 word description
:width: 80%
:align: center

**The Token Brief Template:** One page. Five sections. Everything you need to know before you launch.
:::

Using your NAAT Canvas from Chapter 0 (or building one now if you are starting here), complete the following Token Brief. This document is your design commitment — the artifact that Chapter 3 will transform into an actual on-chain token.

### Section 1: What Does Your Token Represent?

Circle the primary representation (and optionally one secondary):

- **Payment** — a medium of exchange within your ecosystem
- **Access** — the right to use something (service, community, data, feature)
- **Ownership** — a fractional or full claim on an asset or revenue stream
- **Reputation** — earned standing, granted through demonstrated behavior

In 2–3 sentences, explain what specific thing your token grants access to, proves ownership of, represents payment for, or demonstrates reputation in.

### Section 2: Actor Table

For each actor type in your network, complete the following:

| Actor Type | How They Acquire Tokens | Reason to Hold | Reason to Spend |
|-----------|------------------------|----------------|-----------------|
| [Actor 1] | [earn / buy / receive] | [specific benefit from holding] | [specific value from spending] |
| [Actor 2] | [earn / buy / receive] | [specific benefit from holding] | [specific value from spending] |
| [Actor 3] | [earn / buy / receive] | [specific benefit from holding] | [specific value from spending] |

Every cell must be filled. Empty cells mean incomplete design.

### Section 3: Supply Model

Answer each question:

1. What is your total supply? (Pick a specific number and explain why that number.)
2. Is the supply fixed, inflationary, deflationary, or hybrid?
3. Will you revoke the mint authority? If not, who controls it and under what conditions would new tokens be minted?
4. Are there token sinks (mechanisms that permanently remove tokens from circulation)? What are they?

### Section 4: Name, Symbol, and Decimals

- **Token Name:** _______________
- **Symbol:** _______________
- **Decimals:** _______________ (justify your choice)
- **Why this name and symbol:** _______________

### Section 5: 100–200 Word Description

Write a plain-English description of your token: what it is, who it is for, what it does, and why it exists. This will become your token's on-chain metadata description. Write it for a potential holder who has never heard of your project — someone who encounters your token on a DEX and wants to understand it before deciding to buy.

This description should answer the "why would anyone want this?" question implicitly, without ever using the phrase "community," "ecosystem," or "revolutionary."

### Section 6: Logo Generation

Using an AI image tool (DALL-E 3, Midjourney, Adobe Firefly, or the NanoBanana Pro model used in this book), generate a 512×512 pixel PNG logo for your token. Your logo should:

- Be legible at small sizes (it will display as a tiny icon in wallets and on DEXes)
- Clearly reference the token's primary function or the community it represents
- Work on both light and dark backgrounds (consider a circular design with a distinct border)
- Avoid generic crypto imagery (no coins with lightning bolts, no rocket ships)

Prompt template: *"Minimalist logo for [token name], a token representing [primary function]. Clean vector style. [Color palette]. Circular format with white border. Professional, modern, readable at 32x32 pixels."*

### Peer Review: The "Why Would Anyone Want This?" Test

Before you proceed to Chapter 3, exchange your Token Brief with a classmate. The reviewer's job is to ask, for each actor type: *Why would I, as [actor type], actually want to hold this token? What specific, concrete, economic benefit does holding give me?*

The author must answer these questions using only what is written in the Token Brief — no verbal explanation allowed. If the Token Brief cannot answer the question, it is not ready.

A brief passes peer review when every actor type has a clear, economic reason to hold that does not depend on future price appreciation.

---

## What You Walk Away With

By the end of this chapter's activity, you have:

:::{figure} ../images/ch02-deliverables.png
:label: fig-ch02-deliverables
:alt: Checklist graphic showing the five deliverables from Chapter 2 — completed token brief, token name and symbol, supply model decision, 100-200 word description, and 512x512 logo
:width: 80%
:align: center

**Your Chapter 2 Deliverables:** Everything you need to walk into Chapter 3 and launch. If any item on this list is missing, complete it before proceeding — Chapter 3 will use all five.
:::

- ✅ A completed Token Brief with actor table
- ✅ A chosen token name and symbol
- ✅ A supply model with explicit justification
- ✅ A 100–200 word description ready for on-chain metadata
- ✅ A 512×512 logo image file

These five deliverables are the inputs to Chapter 3. Chapter 3 will take them exactly as written and turn them into a live token on Solana mainnet — for under \$60, in a single session. The quality of your Chapter 3 token depends entirely on the quality of your Chapter 2 design work.

---

## Glossary

**Burn** — The permanent destruction of tokens, removing them from circulating supply. Burning is typically accomplished by sending tokens to an address for which no private key exists (making them unspendable).

**Deflationary Token** — A token design where the total supply decreases over time, typically through burn mechanisms.

**Decimals** — The number of decimal places a token supports, determining the smallest possible unit. Nine decimals means the smallest unit is 0.000000001 of the token.

**Fungible** — Interchangeable; one unit is identical to every other unit. Dollar bills are fungible; vintage baseball cards are not.

**Inflationary Token** — A token design where new tokens are continuously minted, typically as rewards for desired behaviors, increasing the total supply over time.

**Mint Authority** — The cryptographic key that holds the power to create new tokens. Revoking the mint authority permanently ends the ability to issue new supply.

**NAAT Framework** — Network, Actors, Assets, Transactions — the analytical framework used throughout this book to evaluate token economies.

**Non-Fungible** — Unique; each unit is distinguishable from every other unit and represents a specific, non-interchangeable thing. NFT stands for Non-Fungible Token.

**Reputation Token** — A token that represents earned standing in a community, typically non-transferable or designed to resist use as pure currency.

**Soulbound Token** — A non-transferable token, designed by Ethereum co-founder Vitalik Buterin, that represents credentials or reputation that cannot be sold or transferred — only earned.

**SPL Token** — Solana Program Library Token — the standard for fungible tokens on Solana, equivalent to ERC-20 on Ethereum.

**Token Brief** — The one-page design document that specifies a token's representation, actor incentives, supply model, name, symbol, and description. The output of this chapter's activity.

**Token Sink** — A mechanism that removes tokens from circulation permanently (burning) or temporarily (locking, staking). Essential for preventing unlimited supply growth in inflationary systems.

**Velocity** — The rate at which tokens circulate in an economy. High velocity means tokens are frequently exchanged; low velocity (hoarding) means tokens sit in wallets. Both extremes can be pathological.

---

## Discussion

**Airline miles are worth billions and almost nobody thinks of them as cryptocurrency. What is the actual difference between a loyalty point and a token — and does that difference favor the company or the customer?**

Consider: Delta SkyMiles has an estimated value of \$28 billion as collateral — Delta used its loyalty program as collateral for a \$9 billion government-backed loan during the COVID pandemic. The miles are not stored on a blockchain. They cannot be transferred freely. Delta can change the redemption value unilaterally, as they do regularly. And yet they function, economically, almost identically to a utility token: earn through purchases, redeem for specific rewards, with supply controlled by the issuer.

The technical difference between a loyalty point and a blockchain token is primarily one of *custody and mutability*. Your airline miles live in Delta's database. Delta can freeze them, expire them, devalue them, or disappear entirely (if Delta goes bankrupt, your miles become worthless — creditors are paid first, loyalty program members are not). A blockchain token lives in your wallet. No airline, no company, no government can freeze it without controlling your private key.

The economic difference is *composability*. Your airline miles can only be redeemed through Delta's approved channels. A blockchain token can be integrated into any protocol that chooses to accept it — a DEX, a DeFi protocol, a third-party merchant. The value of the token can be discovered by a market rather than set by the issuer.

The question of who this favors is genuinely interesting. Delta's control over SkyMiles allows them to manage program economics in their favor — which is why they have used the program as a multi-billion dollar financial instrument. Customer-controlled blockchain tokens prevent this kind of unilateral management — but also remove the issuer's ability to sustainably fund the program through favorable program economics.

**Discussion Guidelines:**

Your response should engage seriously with the power dynamics at play — who benefits from the custodial structure of traditional loyalty programs, and who bears the costs. Include at least one scholarly or credible citation (academic paper, mainstream financial reporting, regulatory document) that supports or complicates your argument. Your response should be 250–400 words.

After posting, respond to at least **two classmates** with substantive engagement — not agreement or disagreement summaries, but a new angle, a counterexample, or a question that pushes the conversation further. Responses of fewer than 100 words do not count as substantive.

---

## 🎯 In-Class Assignment: Token Brief Workshop (10 pts)

**Details and instructions will be provided in class.**

**Points:** 10

---

## 🔬 Hands-On Lab: Token Brief Peer Review

### Part 1: Analyze a Real Token Economy (Individual, 30 minutes)

Choose one of the following existing token economies and apply the NAAT Actor analysis to it:
- **Helium HNT** — a token earned by operating wireless hotspots
- **Axie Infinity SLP** — a token earned through gameplay
- **Stepn GMT** — a token earned through walking
- **Hivemapper HONEY** — a token earned through dashcam mapping

For your chosen token, complete the Actor Table from Section 2 of this chapter using publicly available information. Be specific: find actual holder incentives and spend mechanisms from official documentation, not marketing copy.

Then apply the "why would anyone want this?" test: for each actor type you identified, does the design pass? Where does it fail?

**Deliverable:** A completed actor table + a 200-word assessment of where the token design succeeds and where it breaks down.

### Part 2: Build Your Token Brief (Group, 45 minutes)

Work in groups of 2–3. Each person brings their individual Token Brief draft from the chapter activity.

1. Each group member presents their token brief in 3 minutes. No slides — just the brief.
2. The group applies the "why would anyone want this?" test to each brief, acting as skeptical potential holders.
3. Each group member revises their brief based on the feedback received.
4. Groups present the single most interesting token concept from the group to the class — 2 minutes, brief-only, no embellishment.

**Deliverable:** A revised Token Brief that has passed group peer review, plus a 100-word reflection on what changed and why.

---

## Leader's Takeaway

The most durable insight from this chapter is not about blockchain. It is about business model clarity.

A token is a business model made transferable — which means every weakness in your business model is amplified when it becomes a public, liquid financial instrument. The companies that have built successful token economies are not companies that figured out clever blockchain mechanics. They are companies that figured out clear value propositions, understood their user incentives, and designed supply mechanisms that rewarded genuine network participation.

Airline miles succeed because they solve a real business problem: customer retention in a commodity industry. They create genuine value for frequent flyers. The economics are sustainable because earn rates are tied to revenue and redemption rates are set to maintain program profitability.

Your token will succeed for exactly the same reasons — or fail for the same reasons loyalty programs fail when they become too complex, too restrictive, or too obviously designed to accumulate liability without delivering value.

The technology is Table Stakes. The business design is the work.

---

*End of Chapter 2 · Next: [Chapter 3 — Launch Your Token for Under \$60](#ch-03-launch-your-token)*
