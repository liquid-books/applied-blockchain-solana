---
title: "Governance and Treasury"
subtitle: "Who Decides — and How You Encode the Answer"
short_title: "Governance & Treasury"
description: "A DAO is a company whose bylaws execute themselves, and a multisig is the first governance decision that matters. This chapter covers governance tokens, the DAO lifecycle, multisig treasuries, governance attacks, and how to build your own on Realms and Squads."
label: ch-11-governance
tags: [DAO, governance, multisig, treasury, Realms, Squads, voting, proposal, quorum, decentralization, Solana]
---

# Governance and Treasury

:::{figure} ../images/ch11-explainer-infographic.png
:label: fig-ch11-infographic
:alt: Illustrated explainer infographic showing the full DAO governance ecosystem — governance tokens, proposal lifecycle, multisig treasury, voting quorum, and decentralization spectrum on Solana
:width: 80%
:align: center

**Chapter 11 Explainer Infographic:** The complete governance map — from governance tokens as voting power, through the proposal-quorum-execution lifecycle, to the multisig treasury that nobody controls alone. Every arrow is a decision encoded as code.
:::

Who decides? In a company, a board of directors votes and a CEO signs the check. In a country, a legislature debates and a president signs the bill. In most organizations, the answer to "who decides" is a chain of hierarchy, job titles, and legal authority. In your token economy, the answer is whoever you encode — and the tools to encode it take an afternoon.

This chapter is about governance: the system through which a group of token holders makes collective decisions about shared resources. We will build two things that form the foundation of any decentralized organization. First, a **multisig treasury** using Squads — a wallet that requires multiple people to approve any transaction, the same principle behind corporate bank accounts that require two signatures on checks over a certain amount. Second, a **governance space** on Realms — a voting system tied directly to your token, where holders submit proposals, quorum is enforced automatically, and winning votes execute on-chain.

By the end, you will not just understand how DAOs work conceptually. You will have a working one, with a real treasury and a completed vote.

---

## Governance Tokens: Voting Power as an Asset

To understand a governance token, start with something you already know: a share of corporate stock.

When you own one share of Apple, you own two things. You own a financial claim — a fractional interest in the company's profits and assets. And you own a political right — the right to vote on shareholder resolutions, board elections, and major corporate decisions. Most retail investors focus on the financial claim and ignore the political right, because for any individual holding 100 shares of a trillion-dollar company, the vote is meaningless. But for institutional investors holding millions of shares, the vote is enormously valuable. Governance *is* the asset.

A governance token works the same way, but the political right is the primary value, and it is enforced not by corporate law but by smart contracts. When you hold 10,000 units of a governance token, you hold 10,000 votes. You can submit proposals, vote on proposals others submit, and delegate your votes to representatives you trust — just like shareholders delegate to fund managers. The key difference is that when a proposal passes, no board of directors has to approve it, no bank has to process it, and no lawyer has to file paperwork. The smart contract executes the approved action automatically.

:::{figure} ../images/ch11-governance-token-power.png
:label: fig-ch11-governance-token
:alt: Diagram showing governance token as dual-use asset — financial value on the left, voting power on the right — with examples of both types of rights and how token count maps to proposal submission thresholds and vote weight
:width: 80%
:align: center

**Governance Token as Dual Asset:** Token holders simultaneously hold a financial claim and a political right. In most governance systems, one token equals one vote — making token concentration the primary determinant of governance power.
:::

This is both the beauty and the danger of token governance. The beauty: every rule the organization runs by is visible in the smart contract, and any rule change requires passing through the same transparent voting process. There are no backroom deals, no regulatory exemptions, no "that's just how it's always been done." The danger: whoever holds the most tokens holds the most votes, which means governance power can be purchased.

We will come back to the danger at length. But first, we need to understand the lifecycle of a governance decision.

---

## DAOs Through Familiar Analogies

A **DAO** — a Decentralized Autonomous Organization — sounds alien until you realize you have almost certainly been a member of one of its ancestors.

Think about a **homeowners' association**. Every homeowner in the neighborhood pays dues into a shared treasury. The HOA has rules — you cannot paint your house neon green, you must maintain your lawn. When someone wants to change a rule, they submit a proposal at the annual meeting. Other homeowners vote. If a majority approves, the rule changes. If it fails quorum — not enough people showed up to vote — the proposal dies, regardless of how the votes split.

Or think about a **credit union**. Unlike a bank owned by shareholders, a credit union is owned by its members — the depositors. Members elect a board, vote on major policy decisions, and share in profits through better interest rates rather than stock dividends. The governance structure is member-driven by design.

Or think about **shareholder votes**. Every publicly traded company holds an annual meeting where shareholders vote on board elections, executive compensation, mergers, and other major decisions. The votes are weighted by share count. A hedge fund holding 15% of outstanding shares has 15% of the voting power — far more than any individual retail investor.

A DAO is the digital descendant of all three. Like an HOA, it governs a shared resource using community rules. Like a credit union, its members are its owners. Like a shareholder meeting, its votes are weighted by holdings. The difference is that the bylaws are smart contracts, the treasury is a blockchain address, and the governance process executes without human administrators.

:::{figure} ../images/ch11-dao-analogy.png
:label: fig-ch11-dao-analogy
:alt: Three-column comparison infographic showing HOA, credit union, and shareholder vote on the left mapping to DAO governance equivalents on the right — treasury, membership, voting weight, rule enforcement
:width: 80%
:align: center

**DAO Through Three Familiar Lenses:** The homeowners' association, the credit union, and the shareholder meeting each share structural DNA with a DAO. The DAO replaces legal enforcement with smart contract execution and paper ballots with on-chain transactions.
:::

The word "Autonomous" in DAO is a bit aspirational. Most DAOs today are not fully autonomous — humans still write the code, submit the proposals, and build the products. But the governance process itself is autonomous: once a proposal passes, the execution happens on-chain without any human having to push a button. That automatic execution is what makes DAO governance qualitatively different from any prior form of collective decision-making.

---

## The Governance Lifecycle: Proposal, Quorum, Execution

Every governance system — from the U.S. Congress to a neighborhood HOA — follows the same basic lifecycle. In a DAO, that lifecycle is encoded in smart contracts.

**Step 1: Proposal Submission**

A holder with enough tokens submits a proposal. Most governance systems require a minimum token balance to submit (the "proposal threshold") to prevent spam. On Realms, this is configurable — you set the minimum amount of your token a wallet must hold before it can open a vote.

A proposal is not just text. On Solana's Realms, a proposal includes an optional "instruction" — a specific on-chain action that will execute automatically if the proposal passes. This could be a token transfer from the treasury, a parameter change in your program, or a multisig signing event. The instruction is encoded in the proposal itself, so voters know exactly what they are approving before they cast a vote.

**Step 2: Deliberation**

After submission, there is a discussion period. Holders debate the merits in Discord, forums, or on-chain comment threads. This is the qualitatively human part of governance — the part no smart contract can automate. Good governance systems build in enough deliberation time (typically 48 hours to two weeks, depending on the stakes) for informed opinion to form.

**Step 3: Voting**

The voting window opens. Token holders cast votes — yes, no, or abstain. In token-weighted voting, the weight of your vote is proportional to your token balance at a "snapshot" block — a specific point in the chain's history. Snapshots prevent manipulation: if you could buy tokens after you saw how a vote was going, you could buy a winning position. The snapshot freezes the power distribution at a defined moment.

**Step 4: Quorum Check**

When the voting window closes, the system checks whether **quorum** was reached. Quorum is a minimum threshold of participation — without it, a proposal cannot pass, regardless of how the votes split. This protects against decisions being made by a tiny unrepresentative minority.

Here is where many DAOs fail in practice. If your token has 10 million circulating supply and your quorum threshold is 4 million tokens participating, but most holders are passive — they bought for price appreciation and never engage with governance — you will never reach quorum. The governance system is technically functional but practically paralyzed.

This tension between token distribution and governance participation is one of the central design problems in the field. More on that in the Governance Attacks section.

**Step 5: Execution**

If quorum was reached and the yes votes exceed the threshold (often 51%, sometimes supermajority for major decisions), the proposal passes. On Realms, the attached instruction executes automatically. The treasury sends the approved amount. The parameter changes. The multisig signs. No human administrator has to intervene.

:::{figure} ../images/ch11-governance-lifecycle.png
:label: fig-ch11-governance-lifecycle
:alt: Flowchart showing the five stages of DAO governance lifecycle — proposal submission, deliberation period, voting window, quorum check, and execution — with decision branches for pass/fail outcomes
:width: 80%
:align: center

**The Governance Lifecycle:** From proposal submission through automatic execution, every step is enforced by smart contracts. The quorum check is where most DAO proposals die — not from opposition, but from apathy.
:::

---

## Multisignature Wallets: Nobody Holds the Keys Alone

Before we get to full DAO governance, we need to talk about the first governance decision every project makes — and almost always gets wrong.

When you launch a token, your treasury starts in a single wallet. You are the only signer. You could transfer every token, drain every SOL, and shut down the project in a single transaction. Nothing stops you but your own ethics. This is an enormous trust problem, and it is the reason that serious projects move their treasuries to **multisignature wallets** before anything else.

A multisig wallet requires M-of-N signatures to approve any transaction. The most common setup is 2-of-3: there are three authorized signers, and any two of them must approve before a transaction executes. This is the same principle behind the corporate controls you see in traditional finance: most corporate bank accounts require two authorized signers on checks above certain amounts. Wire transfers at banks require dual authorization. Not because either person is untrustworthy, but because the system cannot depend on any single person's integrity, judgment, or security.

Think of it like a safe deposit box at a bank. The bank holds one key. You hold the other. Neither of you can open it alone. Multisig is the same principle applied to a blockchain wallet: distribute the keys so that no single person — and no single point of failure — can move the funds unilaterally.

:::{figure} ../images/ch11-multisig-structure.png
:label: fig-ch11-multisig
:alt: Diagram showing 2-of-3 multisig wallet structure with three signers — founder, co-founder, advisor — each holding a key, and the vault requiring any two keys to approve a transaction
:width: 80%
:align: center

**Multisig Treasury Structure:** A 2-of-3 multisig requires any two of three authorized signers to approve each transaction. One signer losing access does not freeze the treasury. One signer going rogue cannot drain it.
:::

On Solana, **Squads** is the leading multisig platform. It provides a clean interface for creating a multisig vault, adding co-signers, and managing proposals. A "proposal" in Squads is any transaction the vault wants to make — a SOL transfer, a token transfer, a program upgrade. Once you create a proposal, the other signers receive a notification and can approve or reject. When the threshold is met, the transaction executes.

The corporate analogy maps cleanly:

| Corporate Control | Multisig Equivalent |
|---|---|
| Dual-signature bank account | 2-of-3 multisig |
| Board resolution required for major spending | Proposal + approval threshold |
| CFO + CEO signatures required | Two named signers must approve |
| Audit trail of all approvals | Immutable on-chain record |
| Separation of duties | No single key controls funds |

:::{admonition} Off-Chain Transaction Channels
:class: tip

Multisig approvals batch decisions efficiently, but not every transaction needs to hit the base chain. Bitcoin's Lightning Network pioneered the concept of payment channels — opening a channel on-chain, transacting off-chain at speed and low cost, then settling the net result on-chain. The same throughput philosophy informs how governance systems handle high-frequency treasury actions.
:::

**▶ Watch: Bitcoin's Lightning Network, Simply Explained! (5 min)**

<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;max-width:100%;margin:1.5rem 0;">
<iframe src="https://www.youtube.com/embed/rrr_zPmEiME" style="position:absolute;top:0;left:0;width:100%;height:100%;border:0;" allowfullscreen title="YouTube video"></iframe>
</div>

The multisig is not just a security measure. It is a governance statement. When you put your treasury in a 3-of-5 multisig and publish the signer addresses, you are telling your community: *nobody controls this alone, including me.* That signal is worth more than any whitepaper promise.

---

## Governance Attacks: What Can Go Wrong

Before you build your governance system, you need to understand how it fails. Governance attacks are not theoretical — they have happened to real projects, causing real losses.

**Vote Buying**

Also called "bribery attacks," these occur when a wealthy actor purchases tokens specifically to win a vote, then sells them immediately after. The attacker's cost is roughly proportional to the market impact of their buying and selling, which for thinly traded tokens can be quite low. If the vote controls a treasury worth \$500,000 and an attacker can swing it by spending \$50,000 on temporary token acquisition, the attack has a positive expected value.

The defense is snapshot-based voting combined with time locks. If your governance system takes a snapshot of token holdings 72 hours before voting opens, an attacker cannot acquire tokens and immediately vote. Combine this with a time lock on execution — a delay between when a vote passes and when it executes — and the community has time to spot and respond to malicious proposals before they cause damage.

**Low Turnout Capture**

This is more insidious than vote buying because it requires no bad faith from the attacker. If your token is widely distributed but most holders never vote, a small, organized minority can consistently win governance decisions even with modest holdings. 

Imagine a token with 100 million units circulating. Your quorum threshold is 10 million (10%). Your governance forum has an active community of 500 people who hold 8 million tokens between them. Quorum never reaches 10 million because the other 92 million tokens belong to holders who bought on an exchange and never engage. That engaged minority of 500 people effectively controls governance — not because they cheated, but because everyone else opted out.

The defense is a mix of lower quorum thresholds (more achievable), delegation (passive holders can delegate their voting power to active representatives), and governance incentives (token rewards for participation).

**Whale Capture**

When a single wallet — or a small group of coordinating wallets — controls enough tokens to pass any proposal unilaterally, governance becomes theater. The whale decides, and the vote is a formality.

This is the hardest problem in token governance, because it directly conflicts with the property rights of large holders. If someone bought 20% of your token's supply on the open market, do they not have a legitimate claim to 20% of the governance power? The philosophical answer is uncomfortable: maybe they do, and maybe that is okay. The practical answer is that projects can design governance systems with caps on voting weight per wallet, quadratic voting (where your voting power grows as the square root of your holdings, not linearly), or time locks that reduce the effectiveness of sudden large acquisitions.

:::{figure} ../images/ch11-governance-attacks.png
:label: fig-ch11-attacks
:alt: Three-panel diagram illustrating governance attack types — vote buying with token flash acquisition, low turnout capture with participation statistics, and whale capture with voting weight concentration — each with labeled defense mechanisms
:width: 80%
:align: center

**Three Governance Attack Vectors:** Vote buying exploits timing. Low turnout exploits apathy. Whale capture exploits concentration. Each requires different design defenses — but none is fully preventable without trade-offs.
:::

:::{admonition} The Honest Truth About Governance
:class: warning

No governance system is immune to all of these attacks simultaneously. Designing against vote buying (snapshot + time locks) does not address whale concentration. Designing against whales (quadratic voting) creates sybil attack surfaces — an attacker can split their holdings across many wallets. Governance design is not a solved problem. It is an ongoing negotiation between security, participation, and fairness.
:::

---

## The Decentralization Spectrum: Where You Actually Sit

There is a narrative in the blockchain industry that projects should be "fully decentralized" and that anything less is a failure or a fraud. This is a useful ideal for some contexts and a destructive fantasy for early-stage projects.

The reality is a spectrum, and most successful projects consciously position themselves somewhere in the middle.

At one end: **full founder control**. One wallet controls the treasury, the upgrade keys, the contract parameters. Efficient, fast, aligned — and utterly dependent on the trust and competence of one person or small team. This is appropriate for a project in the first days of existence, before there is a community to govern.

Moving along the spectrum: **multisig control**. The treasury requires multiple signatures from a known, trusted group — founders, lead investors, key community members. Decisions are made by this small council. Still fast, but with distribution of risk. The community cannot be harmed by any single person going rogue.

Further along: **delegated governance**. Token holders elect a council or set of representatives who make day-to-day decisions. Full holders can override on major questions. This is how many DAOs actually work in practice — a small active group handles routine governance, with the broader community reserved for constitutional questions.

At the other end: **on-chain token governance**. Every decision — from treasury allocation to contract upgrades — goes through a public vote. Token holders have full, direct control. Slow, potentially paralyzed by quorum problems, but maximally decentralized.

:::{figure} ../images/ch11-decentralization-spectrum.png
:label: fig-ch11-spectrum
:alt: Horizontal spectrum diagram from full founder control on the left to full on-chain token governance on the right, with labeled stops at multisig control and delegated governance, showing tradeoffs of speed versus decentralization at each stage
:width: 80%
:align: center

**The Decentralization Spectrum:** No project starts at full decentralization, and many never get there — nor should they. The appropriate governance model depends on the project's maturity, community size, and risk tolerance.
:::

The most sustainable trajectory is deliberate progression: start with a multisig, add delegation as the community grows, move to broader token governance as the protocol matures. Compound Finance, Uniswap, and Aave all followed versions of this path — maintaining tight control early, then progressively expanding governance rights as the communities demonstrated the capacity to use them responsibly.

The worst governance decisions are the ones made out of narrative obligation — projects that rush to "full decentralization" before the community is ready, producing systems that are technically decentralized but practically ungovernable.

---

## Activity: Form the DAO

This is where the chapter becomes hands-on. By the end of this activity, you will have a working DAO: a multisig treasury with classmates as co-signers, a Realms governance space tied to your token, and one completed proposal that executed on-chain.

### Part 1: Create Your Multisig Treasury on Squads

**You will need:** Your Phantom wallet (with your token from earlier chapters), the wallet addresses of two classmates who will serve as co-signers.

1. Navigate to [app.squads.so](https://app.squads.so) and connect your Phantom wallet.

2. Click **Create Squad**. Give it a name — something like "[YourToken] Treasury" — and choose **2-of-3 multisig** as your configuration.

3. Add your own wallet as signer #1. Add your two classmates' wallet addresses as signers #2 and #3. Confirm that all three addresses are correct before proceeding.

4. Click **Create** and approve the transaction in Phantom. Squads will deploy the multisig vault on Solana. Copy the vault address — you will need it in the next step.

5. Once the vault is live, initiate a token transfer from your own wallet. Send 5–10% of your token's total supply into the vault. This represents the portion of your token economy managed by the DAO treasury.

:::{admonition} Why 5–10%?
:class: tip

Your treasury allocation (from Chapter 4's tokenomics design) is probably 10–20% of total supply. For the lab, send a portion of it to the multisig to demonstrate the mechanism without depleting your entire treasury allocation. Real projects seed their multisig treasury with their full designated allocation after the multisig is operational.
:::

6. After the transfer, verify the vault balance in the Squads UI. Your two co-signers should also be able to log in and see the vault — ask them to confirm.

### Part 2: Set Up Your Governance Space on Realms

**Realms** ([app.realms.today](https://app.realms.today)) is the standard governance platform on Solana. It is where proposals live, where votes happen, and where on-chain execution gets triggered.

1. Navigate to Realms and click **Create DAO**. Select **Multisig Wallet** if you want governance to reflect your Squads setup, or **Token Governance** to create a fully token-weighted system. For this activity, use **Token Governance**.

2. In the token governance setup, enter the mint address of the token you created in Chapter 3. Realms will verify it on-chain.

3. Configure governance parameters:
   - **Min tokens to create proposal:** Set this to 1 (since you are testing with a small distribution)
   - **Min tokens to vote:** 1
   - **Approval quorum:** 60% (a supermajority — conservative for testing)
   - **Vote duration:** 24 hours (shortened for the lab; real DAOs use longer periods)

4. Click **Create Realm** and approve the transaction. Realms will create your DAO on-chain. Copy the Realm address.

5. Distribute a small amount of your token to your two classmates so they have voting power. They will need to "deposit" the tokens into the governance account in Realms to activate their voting rights — there is a "Deposit Governance Tokens" step in the Realms UI.

### Part 3: Submit and Execute a Real Proposal

Now for the actual governance. You are going to propose, vote on, and execute a real on-chain action: a small airdrop from the treasury.

1. In Realms, navigate to your DAO and click **New Proposal**.

2. Title it something like: "Fund Inaugural Airdrop — Distribute 100 Tokens to Each Governance Member."

3. Write a brief description explaining the rationale: airdrops activate holder engagement and reward early governance participation.

4. Add an instruction: select **Token Transfer**, enter your multisig vault as the source, and set up the transfer details. For the lab, you can simplify by proposing a transfer from your own wallet rather than the multisig — the mechanics of the proposal and vote are identical.

5. Submit the proposal and approve the transaction.

6. Ask your classmates to log in to Realms, find your proposal, and cast their votes. You vote yes. They vote yes. Watch the vote counts accumulate in real time.

7. After 24 hours (or if your governance allows early execution once quorum is clear), click **Execute** when the proposal passes. The on-chain instruction fires. The tokens move. The airdrop happens.

8. Screenshot the completed vote — the proposal status showing "Executed" with the transaction signature. This is your proof of work.

:::{figure} ../images/ch11-realms-proposal.png
:label: fig-ch11-realms
:alt: Screenshot-style mockup of a Realms governance proposal interface showing proposal title, description, vote counts with yes/no bars, time remaining, quorum indicator, and execute button for a passed proposal
:width: 80%
:align: center

**Realms Proposal Interface:** A passed proposal shows vote counts, quorum achieved, and the Execute button ready to fire. Once clicked, the attached instruction runs on-chain automatically — no administrator required.
:::

### What You Have Built

Pause and look at what just happened. You proposed a treasury action. Holders voted. The vote passed quorum. The blockchain executed the result. No bank, no lawyer, no administrator, no intermediary of any kind touched this process. 

That is a DAO. Not as an abstract concept. As a system you built and ran today.

:::{figure} ../images/ch11-dao-architecture.png
:label: fig-ch11-dao-arch
:alt: Full DAO architecture diagram showing the connection between governance token, Realms voting system, Squads multisig treasury, and on-chain execution layer — with labeled arrows showing proposal flow, vote aggregation, quorum check, and treasury transaction
:width: 80%
:align: center

**Your DAO Architecture:** Governance token provides voting power. Realms aggregates votes and enforces quorum. Squads holds treasury funds with multisig protection. On-chain execution connects all three — no human administrator required between proposal and outcome.
:::

---

## Real-World Cases

**MakerDAO: Governing a \$10 Billion System**

MakerDAO governs the DAI stablecoin — a \$10 billion-plus system entirely controlled by MKR token holders. Every parameter that matters — the stability fee charged on loans, the liquidation ratios for collateral, which assets can be used as collateral — is set by governance vote. This is not ceremonial. When MakerDAO governance voted to add real-world assets (physical loan portfolios from traditional banks) as collateral in 2022, it was a decision that brought billions of dollars of traditional finance assets on-chain, made by token holders, executed automatically. The governance system is the company's constitution.

**Compound: The Model Everyone Copied**

Compound Finance built one of the first sophisticated token governance systems in DeFi and then open-sourced it. The "Compound Governor" smart contract — which defines how proposals are submitted, votes are counted, and instructions are executed — became the template for dozens of subsequent governance implementations, including Uniswap. Understanding Compound's governance is understanding how most of DeFi votes.

**▶ Watch: What is a Bitcoin hard fork? Simply Explained! (4 min)**

<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;max-width:100%;margin:1.5rem 0;">
<iframe src="https://www.youtube.com/embed/XCo6yyutYAM" style="position:absolute;top:0;left:0;width:100%;height:100%;border:0;" allowfullscreen title="YouTube video"></iframe>
</div>

**The Juno Network Incident: Whale Capture in Real Life**

In 2022, the Cosmos-based Juno Network passed a governance proposal to "claw back" a large allocation of tokens from a single whale wallet that the community believed had gamed an airdrop. The proposal passed with broad community support. But the execution had an error — the wrong wallet address was in the proposal, and the clawback hit an innocent exchange custodial wallet instead of the intended target. A second vote corrected it. 

The incident illustrated both the power and the fragility of on-chain governance: the community could act decisively against a bad actor, but the automatic execution of a flawed proposal was irreversible. Time locks — delays between vote passage and execution — exist precisely to catch this kind of error before it causes permanent damage.

**Uniswap: Governance as Brand**

Uniswap's UNI token launched with \$6.43 per UNI and an initial market cap of hundreds of millions of dollars — before Uniswap governance had made a single meaningful decision. The value was not current utility; it was future optionality. Holders were buying the right to vote on the direction of the leading DEX, on fee switches, on grants, on protocol upgrades. Governance power was so obviously valuable that the market priced it immediately. This is the clearest evidence that governance tokens are genuinely assets, not just voting chips.

:::{figure} ../images/ch11-case-studies.png
:label: fig-ch11-cases
:alt: Four-panel case study cards showing MakerDAO governing DAI parameters, Compound open-sourcing Governor contracts, Juno claw-back incident with time lock lesson, and Uniswap UNI as governance-value asset
:width: 80%
:align: center

**Four DAO Case Studies:** MakerDAO governs billions. Compound set the template. Juno learned the hard way about time locks. Uniswap proved governance is an asset class. Each teaches a distinct lesson about what governance systems can do and how they fail.
:::

---

## 🎯 In-Class Assignment: DAO Formation Report (10 pts)

**Details and instructions will be provided in class.**

**Points:** 10

---

## 💬 Discussion

**In your DAO, one token equals one vote. That means the largest holder has the loudest voice — exactly like a shareholder meeting. Is that democracy, plutocracy, or just honesty about how power works? Could you design something better?**

The one-token-one-vote system is honest about something most governance systems pretend is not true: power is not equal. In a shareholder meeting, the hedge fund with 12% of the float does not have the same influence as the retail investor with 100 shares, and nobody pretends otherwise. Token governance makes this explicit and algorithmic instead of implicit and political.

But "honest" is not the same as "right." Democracy as an ideal is not one-dollar-one-vote — it is one-person-one-vote, because we believe every citizen has equal standing regardless of wealth. The question is whether a token economy is more like a company (where owners govern in proportion to ownership) or more like a polity (where stakeholders govern as equals).

Some alternatives have been tried. **Quadratic voting** makes each additional vote more expensive — your first token gives you one vote, but your second costs two tokens, your third costs three, and so on. This compresses the power of large holders without eliminating it. **Conviction voting** weights votes by time: holding a vote position for longer builds more voting power, rewarding long-term commitment over short-term speculation. **Reputation systems** give voting power based on contribution history rather than token balance — harder to buy, easier to earn.

Each system has costs. Quadratic voting is sybil-vulnerable: a whale can split tokens across a thousand wallets and recover most of their power while pretending to be a thousand citizens. Reputation systems are opaque and gameable in different ways.

The honest answer is that there is no perfect governance system — only systems that optimize for different values with different trade-offs. One-token-one-vote is the simplest, most transparent, and most easily understood by outsiders. Its trade-off is concentration of power. Alternatives reduce concentration but add complexity and new attack surfaces.

What you design should reflect the community you are actually building, not the one you imagine. A protocol used primarily by a small group of sophisticated technical users might work well with reputation governance. A mass-market consumer token probably needs something simple and widely understood. The governance system is not separate from the community — it is one of the clearest expressions of what the community believes about itself.

### Discussion Guidelines

Write a minimum 300-word original post that responds to the discussion prompt. Your post must:
- Take a position on whether one-token-one-vote is appropriate for your specific token project from this course
- Include at least one scholarly or credible citation (academic paper, reputable news source, or documented governance case study)
- Propose at least one concrete modification to improve your governance design and explain the trade-offs

After posting, respond to **at least two peers** with substantive feedback — not just agreement, but engagement with their reasoning. Challenge their assumptions, build on their ideas, or offer a counterexample from a real project.

---

## Glossary

```{glossary}
DAO
  Decentralized Autonomous Organization. A collective governed by smart contracts rather than traditional legal and corporate structures. Rules are encoded in code, treasury is held on-chain, and decisions are made by token holders through public voting processes.

Governance Token
  A token whose primary utility is voting rights over a protocol or organization. Holders can submit proposals, vote on proposals, and often delegate their votes to representatives.

Multisig
  Short for multi-signature. A wallet or account that requires approval from M of N authorized signers before any transaction can execute. The most common configurations are 2-of-3 and 3-of-5.

Squads
  The leading multisig platform on Solana. Allows groups to create shared vaults, submit transaction proposals, and require threshold approval before funds move.

Realms
  The leading DAO governance platform on Solana. Supports token-weighted voting, proposal submission with on-chain instructions, quorum enforcement, and automatic execution of passed proposals.

Quorum
  A minimum threshold of participation required for a governance vote to be valid. If fewer than the quorum threshold of tokens participate, a proposal fails regardless of how the votes split.

Proposal Threshold
  The minimum token balance a wallet must hold to submit a governance proposal. Prevents spam and ensures proposers have skin in the game.

Vote Snapshot
  A specific block height at which token balances are recorded for voting purposes. Prevents manipulation by buying tokens after seeing how a vote is trending.

Time Lock
  A delay between when a governance proposal passes and when its associated instruction executes. Gives the community time to spot and respond to malicious or flawed proposals before they cause permanent damage.

Vote Delegation
  The ability of a token holder to assign their voting power to another wallet — a representative who votes on their behalf. Allows passive holders to participate indirectly.

Quadratic Voting
  A voting system where the cost of additional votes grows quadratically. Your first vote costs 1 token, your second costs 4, your third costs 9. Compresses power concentration compared to one-token-one-vote.

Conviction Voting
  A governance mechanism where voting power accumulates over time. The longer you hold a vote position, the more weight it carries. Rewards long-term commitment over short-term coordination.

Whale Capture
  A governance failure mode where a small number of large token holders effectively control governance outcomes, reducing the system to a formality for everyone else.

Governance Attack
  Any attempt to manipulate a governance system to extract value or push through self-serving proposals at the expense of the broader community. Includes vote buying, low-turnout exploitation, and flash loan attacks.

Sybil Attack
  An attack in which one entity creates many fake identities or wallets to game a system that assigns power per identity rather than per token. Particularly relevant when governance systems try to limit per-wallet voting power.
```

---

## Chapter Summary

Governance is not a feature you add to a token economy — it is the architecture underneath everything else. The decisions you encode about who can propose, how votes are weighted, what quorum looks like, and where treasury funds live will shape your project's culture and resilience for years.

The two tools in this chapter — **Squads** for multisig treasury and **Realms** for on-chain voting — are not exotic. They are the standard infrastructure that serious Solana projects use in production. By completing this chapter's activity, you have done exactly what founding teams do when they formalize their governance: moved funds into a shared vault, set up a public voting process, and run a real proposal to completion.

The conceptual foundation matters as much as the tools. A DAO is a company whose bylaws execute themselves. A multisig is the first governance decision that matters — because nobody should hold the keys alone. And the decentralization spectrum is not a linear path toward some ideal end state. It is a design space where you choose the position that fits your community, your maturity, and your risk tolerance — and revisit that choice as all three evolve.

**Walk Away With:**
- ✅ A 2-of-3 multisig treasury on Squads with co-signers
- ✅ A token-governed DAO on Realms linked to your token
- ✅ One completed proposal — submitted, voted on, executed on-chain
- ✅ A framework for understanding governance attacks and how to design against them
