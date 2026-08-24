---
title: "Your First Program, No Setup Required"
subtitle: "Deploy a Rule to a Global Network From Your Browser"
short_title: "Your First Program"
description: "Everything so far has been done through other people's tools. This chapter shows what those tools are made of — and you will deploy your own rule to a global network without installing anything. A smart contract is just a rule that runs itself, and understanding that is the difference between using blockchain and thinking with it."
label: ch-08-first-program
tags: [Solana programs, smart contracts, Solana Playground, devnet, instructions, accounts, signers, upgrade authority, code is law, on-chain development]
---

# Your First Program, No Setup Required

:::{figure} ../images/ch08-explainer-infographic.png
:label: fig-ch08-infographic
:alt: Illustrated explainer infographic showing the anatomy of a Solana program — stateless program box, separate account boxes holding state, instruction arrows, signer key icons, and devnet vs mainnet contrast
:width: 80%
:align: center

**Chapter 8 Explainer Infographic:** A Solana program is a stateless rule deployed to the network. Accounts hold the data. Instructions trigger the rules. Signers authorize the action. By the end of this chapter, you will have deployed all three to devnet and watched them run.
:::

Everything you have built so far in this course has been built *inside* someone else's rules. You used Phantom because Phantom's code connects your wallet to Solana's network. You used Raydium because Raydium's smart contracts calculate prices and move liquidity. You used Jupiter because Jupiter's routing program finds the best swap path across a dozen pools. Every tool you have touched is just a program — a rule deployed to a public network — and that program runs exactly as written, forever, for anyone who sends it the right instruction.

Now you are going to write and deploy one of your own.

This is not a software engineering chapter. You will not need to install anything. You will not need to understand every line of code. What you *will* understand is what a program actually is, how it differs from what you might have heard about Ethereum smart contracts, why the phrase "code is law" is both a promise and a serious warning, and how a business leader — not a developer — reads a deployed program and evaluates whether it is safe to trust.

The activity at the end deploys a check-in program to Solana's devnet entirely inside your browser using Solana Playground. By the time you finish, you will have a real transaction on a real network proving your program ran.

---

## What a Program Is (And Why Solana Flipped the Architecture)

Let us start with the most important mental model in this chapter, because getting it wrong will cause confusion every time you read about Solana development.

On Ethereum, a **smart contract** is a bundle that contains two things in one place: the rules (the logic, the code) and the data (the state, the balances, the counts, the records). The contract lives at a single address, and every interaction reads from and writes to that same bundle. The contract owns its data.

:::{figure} ../images/ch08-ethereum-vs-solana.png
:label: fig-ch08-architecture
:alt: Side-by-side architecture diagram comparing Ethereum smart contract (rules and state bundled together in one contract) versus Solana program (stateless program separate from data accounts that hold state)
:width: 80%
:align: center

**Architecture Contrast:** Ethereum bundles rules and state in one contract address. Solana separates them — programs are stateless, and accounts hold the data. This separation is why Solana can process transactions in parallel.
:::

Solana made a different choice. On Solana, **programs are stateless**. A program contains only the rules — the logic, the instructions it knows how to execute. It holds no data of its own. The data lives in separate **accounts** that the program can read from and write to when instructed to do so. The program does not own those accounts; it is merely authorized to modify them under specific conditions.

Think of it this way. Imagine a vending machine. The vending machine's logic — accept money, dispense item, return change — is the *program*. But the vending machine has no idea what inventory it currently holds or how much money is in the cash drawer until you look at those storage compartments separately. In Solana's model, the vending machine logic (program) and the inventory + cash tray (accounts) are physically separate. The logic runs, reads from the accounts, writes to the accounts, then steps back.

This design has enormous consequences for performance. Because programs do not hold state themselves, Solana's runtime can execute multiple transactions in parallel as long as they touch different accounts. When you hear that Solana processes 65,000 transactions per second, the stateless program model is a major reason why.

The analogy breaks down in one important way: a vending machine operator can open the machine and physically change things. On Solana, the only way to change account data is through an authorized instruction executed by the program. Nobody can reach in from outside the machine.

:::{admonition} Why This Matters for Business
:class: important

If you are evaluating a Solana protocol as an investor or business partner, you want to find the program address and read its list of instructions. That list tells you everything the protocol can and cannot do. A stablecoin protocol whose program has no instruction for minting additional tokens cannot inflate your holdings. A gaming protocol whose program has no instruction for transferring NFTs without owner consent cannot rug-pull your assets. The stateless architecture makes auditing cleaner: you audit the program's instructions, then audit the accounts it touches.
:::

---

## Instructions, Accounts, and Signers: The Three Things Every On-Chain Action Needs

Every single action on Solana — every token transfer, every NFT mint, every liquidity pool trade, and every check-in you will run today — requires exactly three things. Learn these and you can read any Solana transaction.

:::{figure} ../images/ch08-instruction-anatomy.png
:label: fig-ch08-instruction
:alt: Diagram showing a single Solana transaction composed of three labeled layers: instruction (what to do), accounts list (what data to read or write), and signers (who is authorizing)
:width: 80%
:align: center

**Transaction Anatomy:** Every Solana transaction carries an instruction (the action), a list of accounts (the data locations), and one or more signers (the authority). Missing any one of these three elements, the transaction fails.
:::

**Instructions** tell a program what to do. A program may know how to execute many different instructions — initialize, increment, transfer, close, vote, stake. An instruction is a specific call to one of those capabilities. When you hit "Confirm" in Phantom, your wallet is packaging an instruction and sending it to the Solana network to be executed.

**Accounts** are the data locations that the instruction needs to read from or write to. Every instruction must explicitly declare which accounts it will touch. This is not optional and not implicit — the declaration is built into the transaction itself. When the Solana runtime receives the transaction, it uses this account list to decide whether the transaction can be processed in parallel with others (if their account lists do not overlap, they can run simultaneously).

Accounts come in two varieties relevant here. A **program account** holds the compiled program code — it is read-only during execution. A **data account** holds the state that your program reads and modifies. When you deploy a program and then "initialize" it, you are creating a data account associated with that program and writing starting values into it.

**Signers** are wallets that have cryptographically authorized the transaction. The signer's private key produces a digital signature proving "I own this wallet and I approve this action." Most transactions require at least one signer — typically the person paying the transaction fee (the fee payer) and often the person whose assets are being affected. Some instructions require multiple signers: a multisig treasury might require three out of five designated wallets to sign before any funds move.

:::{admonition} Reading a Transaction on Solana Explorer
:class: tip

Open any transaction on [explorer.solana.com](https://explorer.solana.com) and you will see all three elements laid bare. The top section shows the instruction name and the program it called. Below that, the "Account Inputs" section lists every account the instruction touched with a label for whether it was read, written, or signed. This is public, permanent, and unalterable. There is no way for a program to secretly touch an account that is not declared in the transaction. That is the audit trail.
:::

---

## "Code Is Law": The Promise and the Warning

The phrase **code is law** is the oldest and most contentious slogan in blockchain culture. It means exactly what it sounds like: the rules encoded in a smart program are the governing authority. Not a CEO's decision, not a regulator's ruling, not a court order, not a change of heart. The code runs as written.

:::{figure} ../images/ch08-code-is-law.png
:label: fig-ch08-code-is-law
:alt: Split illustration showing code-is-law as both shield (protection from arbitrary authority, censorship, corruption) and double-edged sword (bugs cannot be patched, exploits cannot be stopped, compliance becomes impossible)
:width: 80%
:align: center

**Code Is Law — Promise and Risk:** The same property that protects users from arbitrary authority also protects exploiters from correction. Immutability is not inherently good or bad; it is a design choice with consequences that must be evaluated before deployment.
:::

For users, this is a powerful guarantee. When you deposit funds into a Solana protocol whose program has been audited and whose upgrade authority has been revoked, you know with certainty that no one — not the founders, not regulators, not hackers — can change the rules after the fact. The promise made to you at deposit time is the promise that will govern your funds forever.

For builders and regulators, this is a genuine problem. Consider: in 2016, a vulnerability in Ethereum's "The DAO" contract allowed an attacker to drain \$60 million. The code was doing exactly what it was written to do. The attack was, in a strict technical sense, legal under the code-is-law framework. The Ethereum community ultimately chose to fork the blockchain and reverse the theft — an enormously controversial decision that resulted in the split between Ethereum and Ethereum Classic.

The uncomfortable question code-is-law raises for business is this: *who bears the risk of a bug?* In a traditional business, when a software error causes harm, the company patches it, compensates affected customers, and updates its systems. In a deployed-and-immutable smart program, there is no patch. There is no compensation path. There is the code, running as written, processing the exploit as a valid instruction because the rules permit it.

This is not a reason to avoid programs. It is a reason to choose your upgrade strategy deliberately.

---

## Upgradeable vs. Immutable: A Business Decision, Not a Technical One

When you deploy a program on Solana, you can choose one of three stances on upgrades:

:::{figure} ../images/ch08-upgrade-authority.png
:label: fig-ch08-upgrade
:alt: Three-column diagram showing upgrade authority options — upgradeable (developer controls), multisig (DAO/committee controls), and revoked (immutable forever) — with labeled pros, cons, and trust implications for each
:width: 80%
:align: center

**Upgrade Authority Spectrum:** Every deployed program occupies one of three positions on the upgrade spectrum. The right choice depends on the stage of your protocol, the nature of your users' assets, and your regulatory exposure.
:::

**Upgradeable programs** have a designated upgrade authority — typically the deploying wallet. The authority can push new code to the same program address at any time. Users interacting with that program are trusting not just the current code but also the authority's future intentions. This is appropriate for early-stage protocols where bugs are likely and the team needs to iterate. It is a trust relationship, like trusting a CEO.

**Multisig upgrade authority** transfers upgrade control to a multisignature wallet or a DAO governance program. Code changes require approval from multiple independent parties. This is the middle path: the protocol can still be updated to fix bugs or comply with regulations, but no single person can push malicious code. Most mature DeFi protocols use this model.

**Revoked upgrade authority** means the program is permanent. No one can change it. Ever. This maximizes user trust in the code-is-law sense — the rules are literally fixed — but it also means bugs live forever and compliance with new legal requirements becomes impossible. Protocols that have revoked upgrade authority and hold significant user funds are making a statement: *we are so confident in this code that we are giving up the ability to fix it.*

As a business leader building a token economy, your choice of upgrade authority is a stakeholder communication. Before you revoke upgrade authority, ask: have we had the program audited by at least two independent firms? Have we run it on devnet and mainnet with real funds for a meaningful period? Do our users understand and want immutability? Is immutability actually required for our use case?

The answer is often: not yet. Most token economies should start upgradeable and revoke authority only after extended battle-testing and community agreement.

---

## Devnet vs. Mainnet: Rehearsal and Performance

Solana runs multiple parallel networks that share the same software but have separate ledgers, separate tokens, and separate validators.

:::{figure} ../images/ch08-devnet-mainnet.png
:label: fig-ch08-networks
:alt: Diagram showing two parallel Solana networks — devnet (free tokens via faucet, no real value, for testing) and mainnet-beta (real SOL with real value, live users) — with arrows showing the deploy workflow from devnet to mainnet
:width: 80%
:align: center

**Devnet and Mainnet:** Two separate Solana networks. Devnet is the rehearsal stage where tokens are free and mistakes cost nothing. Mainnet-beta is the performance — real SOL, real users, real consequences.
:::

**Devnet** is the rehearsal stage. SOL on devnet has no real-world value and can be obtained for free via a faucet. Programs deployed to devnet run exactly the same way as they would on mainnet, but mistakes cost nothing. Devnet is where you test your program's logic, verify your instructions work as expected, and practice the full deploy-and-test workflow.

**Mainnet-beta** is the live performance. SOL is real money, users are real people, and mistakes have real consequences. Deploy to mainnet only after exhaustive devnet testing and (ideally) an independent audit.

**Testnet** exists as a third option used primarily by Solana validators and core developers to test protocol upgrades. For application developers, devnet is the right environment.

The workflow is always: *develop locally or on Playground → test exhaustively on devnet → audit → deploy to mainnet*. Skipping steps in this sequence is how protocols lose user funds.

For today's activity, you are working on devnet. Everything you deploy there is real in terms of code execution — it uses the same runtime, the same instruction format, the same account model — but the SOL costs you nothing and the program affects no one's actual finances.

---

## Reading, Not Writing, Code: How a Business Leader Evaluates a Program

You do not need to write Rust to evaluate a deployed Solana program. A business leader's job is to understand what a program *can* and *cannot* do and whether those boundaries match the protocol's stated purpose.

:::{figure} ../images/ch08-reading-programs.png
:label: fig-ch08-reading
:alt: Annotated screenshot-style illustration of a Solana program's instruction list showing how to identify what a program can do, what accounts it touches, and what authority constraints protect users
:width: 80%
:align: center

**Evaluating a Program Without Writing Code:** The program's instruction list, its account access patterns, and its upgrade authority status are the three things a business-minded evaluator reads. These are publicly available for every deployed program.
:::

Here is the checklist:

**1. Find the program address.** Every protocol publishes its program ID — a base58-encoded public key that uniquely identifies the deployed program on the network. Look for it in the protocol's documentation, their GitHub repository, or their audit reports.

**2. Check the upgrade authority.** Go to [explorer.solana.com](https://explorer.solana.com), search the program ID, and look at the program account's details. The upgrade authority field tells you who can change this program. If it shows "None," the program is immutable. If it shows a wallet address, that wallet is the god of that protocol.

**3. Read the instruction list.** Open-source protocols publish their program source code (typically Rust using the Anchor framework). The list of `pub fn` function names in the program's `lib.rs` file is the instruction list. Each function is something the program can do. If the function does not exist, the program cannot do it — not by a clever hack, not by calling a hidden API. The instruction list is the complete capability set.

**4. Cross-reference with the whitepaper.** A protocol's stated purpose and its actual program capabilities should match. If the whitepaper says "we cannot mint additional tokens" but the program has a `mint_tokens` instruction, there is a discrepancy worth investigating.

**5. Review the audit reports.** Reputable programs have been audited by firms like Halborn, OtterSec, Trail of Bits, or Neodyme. Audit reports identify vulnerabilities found and whether they were resolved. No audit means no one has professionally searched for ways to exploit this code.

This process takes an hour and requires no coding. For any protocol where you or your organization plans to hold significant funds, it is due diligence.

---

## Activity: Deploy a Check-In Program to Devnet

This activity uses **Solana Playground** — a browser-based development environment at [beta.solpg.io](https://beta.solpg.io). No installation required. No local toolchain. Just a browser.

:::{figure} ../images/ch08-playground-overview.png
:label: fig-ch08-playground
:alt: Annotated interface diagram of Solana Playground browser IDE showing the file explorer panel, code editor, build button, deploy button, and test panel with labeled callouts for each element
:width: 80%
:align: center

**Solana Playground Interface:** The browser-based IDE includes a file panel, code editor, build system, and interactive test panel. Every step of today's activity happens inside this interface — no installation needed.
:::

### Step 1: Open Solana Playground and Create a Wallet

Navigate to [beta.solpg.io](https://beta.solpg.io) in your browser. Click **"Not connected"** in the bottom left corner. Solana Playground will generate a devnet wallet for you automatically. Save the keypair when prompted — you can export it if you want to reuse it. Your devnet SOL balance will appear at the bottom left.

If your balance shows 0 SOL, click the airdrop button (the faucet icon) to request free devnet SOL. You will need a small amount to pay for deployment.

### Step 2: Load the Counter Template

Click **"File → New Project"** and choose the **"Counter"** template from the starter options. This is a minimal Anchor program with three instructions: `initialize`, `increment`, and a stored count. It is the simplest possible stateful program.

You will see three files:
- `lib.rs` — the program logic (Rust + Anchor)
- `Anchor.toml` — project configuration
- `tests/counter.test.ts` — the test file

### Step 3: Rename It as Your Check-In Program

This step is optional but meaningful. The counter template counts generic increments. We are renaming it mentally to represent **check-ins** in your token economy — a loyalty program where users earn points each time they check in to your platform.

In `lib.rs`, find the struct named `Counter` and the field named `count`. You can rename these to `CheckInAccount` and `check_in_count` throughout the file if you wish to practice reading Rust, or leave the template unchanged and simply understand that "increment" means "check in" for our purposes.

The code, unchanged, still performs exactly the logic we need:
- `initialize` creates a new account and sets the count to zero.
- `increment` adds one to the count each time it is called.

### Step 4: Build the Program

Click the **"Build"** button (the hammer icon) in the left sidebar. Solana Playground compiles your Rust code into a binary that Solana's BPF (Berkeley Packet Filter) runtime can execute. Watch the terminal at the bottom for output. A successful build ends with:

```
Build successful. Completed in X.XXs.
```

If you see errors, they will point to specific lines in the code. The counter template builds without modification — if you renamed fields, double-check that every reference was updated consistently.

### Step 5: Deploy to Devnet

Ensure the network selector in the top right shows **"devnet"** — not mainnet. Click the **"Deploy"** button. Playground will:
1. Upload the compiled program binary to a program account on devnet
2. Set your Playground wallet as the upgrade authority
3. Return your **Program ID** — a base58 public key that uniquely identifies your deployed program

Copy and save your Program ID. It looks something like: `7JyKbGkKp5sS...` (32 bytes encoded in base58).

:::{admonition} What Just Happened
:class: note

You just published code to a global network of validators spread across dozens of countries. Those validators have now stored your program. Any wallet in the world can send your program ID an instruction and execute your check-in logic. This is what "deploying to a blockchain" means in concrete terms — not uploading to a server, but propagating to a decentralized network of nodes that will execute your rule forever.
:::

### Step 6: Run the Initialize Instruction

Click the **"Test"** tab (beaker icon) in the left sidebar. Solana Playground generates an interactive test panel from your program's instruction definitions.

Find the **`initialize`** instruction and click **"Run"**. Playground will:
- Create a new data account associated with your program
- Set `check_in_count` (or `count`) to zero
- Return a transaction signature

Click the transaction signature to open it in Solana Explorer. You will see:
- The program ID you just deployed
- The accounts touched: your wallet (signer), the new data account (writable)
- The instruction name: `initialize`
- The fee paid: a tiny fraction of a devnet SOL

### Step 7: Run the Increment Instruction

Back in the Test panel, find **`increment`** and click **"Run"**. This fires the check-in instruction — adding 1 to the counter.

Run it three or four times. Each execution is a separate transaction, each with its own signature and its own entry on the Solana Explorer. This is your transaction log: irrefutable on-chain proof that the rule ran.

### Step 8: Locate Your Program on Solana Explorer

Navigate to [explorer.solana.com](https://explorer.solana.com) and switch the network selector to **"Devnet"**. Search your Program ID. You will see the program account, its upgrade authority (your wallet), the number of transactions processed, and a list of recent transactions including your initialize and increment calls.

This is what your program looks like from the outside. This is what an investor, user, or auditor sees when they look up your protocol.

### Stretch Activity: Add a Decrement Instruction

If you are comfortable with the code, try adding a `decrement` instruction using `increment` as a template. The only change needed is replacing `+= 1` with `-= 1`. Rebuild and redeploy. Run decrement and verify the count drops on Explorer.

Students who do not wish to modify code: the deploy-and-test loop above, with the template unchanged, is the complete activity. You have deployed a real program.

---

## Walk Away With

By the end of this activity you have:

- A **Program ID** — a real address on Solana's devnet network identifying your deployed program
- A **transaction log** — multiple Solana Explorer links proving your program was initialized and executed
- A mental model of programs, accounts, and instructions that applies to every protocol you will ever use or evaluate
- The ability to look up any deployed program and evaluate its upgrade authority and capability set without writing a line of code

:::{figure} ../images/ch08-walk-away-summary.png
:label: fig-ch08-summary
:alt: Summary illustration showing three key outputs from the activity — a Program ID card, a transaction log timeline on Solana Explorer, and a checkmark list of concepts understood (stateless programs, accounts, instructions, upgrade authority)
:width: 80%
:align: center

**What You Built:** A deployed program on devnet (Program ID), a verifiable transaction log on Solana Explorer, and a framework for evaluating any Solana protocol from the outside.
:::

---

## Application Cases

:::{figure} ../images/ch08-application-cases.png
:label: fig-ch08-applications
:alt: Diagram showing four real-world application domains for Solana programs — loyalty rewards, DAO governance, supply chain provenance, and subscription access control — each with use case arrows
:width: 80%
:align: center

**Real-World Applications of On-Chain Programs:** The same program architecture you deployed today — initialize an account, increment on each event — underlies loyalty systems, governance votes, supply chain records, and subscription access control.
:::

### Loyalty and Rewards Programs

Starbucks' Odyssey program launched in 2022 as a blockchain-based loyalty extension, using smart contract logic to issue NFT stamps and track engagement points. The underlying principle — a check-in program incrementing a counter tied to a user's wallet — is exactly what you built today. At scale, this becomes: user buys coffee, app sends `increment` instruction to the loyalty program, counter updates, threshold triggers token reward. No central database, no points expiry managed by the company, no opaque "we reset your balance" decisions.

The business case is straightforward: token balances in self-custodied wallets cannot be silently zeroed by a policy change. Users retain ownership of their accumulated loyalty. For brands seeking differentiation on trust, this is a meaningful claim.

### Decentralized Voting and Governance

Many DAO (Decentralized Autonomous Organization) governance systems use a program that is structurally similar to what you built: an initialize instruction creates a proposal account, an increment (vote) instruction records each member's participation, and a separate instruction finalizes the result when the voting window closes. The entire vote is publicly auditable. Every vote is a transaction with a timestamp and a signer.

Compare this to traditional shareholder voting administered by a transfer agent: opaque, slow, and accessible only to sophisticated institutional investors. On-chain governance makes voting real-time, globally accessible, and cryptographically verifiable.

### Supply Chain Provenance

A luxury goods manufacturer could deploy a program where the `initialize` instruction creates an asset account for each product leaving the factory and subsequent `increment`-style instructions record each custody transfer — manufacturer to distributor to retailer to end customer. The program's logic ensures no one can claim a custody transfer without the current owner's signature. The history is permanent and unforgeable.

LVMH's Aura blockchain consortium operates on this principle. Your check-in program is the conceptual skeleton of every provenance system on Solana.

### Subscription and Access Control

Imagine a publishing platform where your token economy includes a `check_subscription` instruction. Each time a user accesses premium content, the platform's backend calls the instruction, verifying the user's subscription account shows an active status. The subscription expiry is written on-chain. Renewal triggers an on-chain transaction. Cancellation is an instruction call. Every subscription event is a transaction — a public log of when access was granted and revoked.

---

## Glossary

```{glossary}
Program (Solana)
  A stateless binary deployed to the Solana network containing the logic (instructions) that the program can execute. Programs do not hold their own state; they read and write data accounts.

Account (Solana)
  A storage location on the Solana ledger. Accounts hold data, SOL balances, or program code. Every account has a public key address and an owner (the program authorized to modify it).

Instruction
  A specific action that a program knows how to execute. An instruction specifies the program to call, the accounts it needs, and any additional parameters. Transactions contain one or more instructions.

Signer
  A wallet that has cryptographically authorized a transaction using its private key. The signer's public key is included in the transaction, and validators verify the signature before executing the instruction.

Upgrade Authority
  The wallet or multisig address that controls whether a deployed program can be updated with new code. Revoking upgrade authority makes the program permanently immutable.

Devnet
  A Solana test network that runs the same software as mainnet but uses SOL with no real-world value. Used for development and testing before deploying to mainnet.

Mainnet-beta
  The live Solana network where SOL has real economic value and transactions have real consequences. Also called mainnet.

Anchor
  A framework for building Solana programs in Rust that handles much of the low-level boilerplate (account validation, serialization, error handling), making programs easier to write and audit.

Program ID
  A base58-encoded public key that uniquely identifies a deployed program on the Solana network. Used to call the program's instructions and to find it on Solana Explorer.

BPF (Berkeley Packet Filter)
  The virtual machine format that Solana uses to execute programs. Program code is compiled to BPF bytecode, which the Solana runtime executes on every validator.

Data Account
  An account created by a program to store state. When you call `initialize` in today's activity, you create a data account that holds the check-in counter value.

Code Is Law
  The principle that a deployed smart program executes exactly as written, with no exceptions for intent, error, or external authority. A feature to users seeking trustless execution; a risk to builders who need to fix bugs.

Solana Playground
  A browser-based Solana development environment at beta.solpg.io that allows writing, building, deploying, and testing programs without installing any local tools.

Multisig
  A wallet or governance structure that requires signatures from multiple independent parties before executing a transaction. Used for shared custody and for governance of upgrade authority.

Immutable Program
  A deployed program whose upgrade authority has been revoked. The program's code can never be changed. This maximizes user trust but eliminates the ability to fix bugs or comply with new regulations.
```

---

## The Leader's Takeaway

A smart contract — or on Solana, a *program* — is a rule that runs itself. That is the entire idea, and it is the most consequential shift in institutional design since the invention of the corporation.

Corporations exist because we needed a legal entity that could persist beyond individual humans, hold assets, and execute agreements reliably. We built courts, regulators, auditors, and contract law to enforce those agreements. That infrastructure is expensive, slow, geographically limited, and corruptible.

A deployed program on Solana is also a persistent entity. It holds no assets directly, but it governs accounts that do. It executes agreements automatically — not in days or weeks through legal machinery, but in 400 milliseconds, globally, for a fraction of a cent in fees. Its rules are publicly readable. Its history is permanently auditable. Its upgrade authority is a visible, evaluable fact rather than a hidden organizational power.

This does not mean programs replace corporations. It means there is now a new tool available for encoding certain kinds of rules — loyalty points, vote counts, custody records, subscription states — in a way that is cheaper to operate, harder to corrupt, and more transparent to verify than any alternative.

You deployed one today. From your browser. On a global network. Without asking anyone's permission.

That is worth sitting with.

---

## 🎯 In-Class Assignment: Program Evaluation Exercise (10 pts)

**Details and instructions will be provided in class.**

**Points:** 10

---

## 💬 Discussion: When Should Rules Be Unchangeable?

A program with its upgrade authority revoked can never be changed — not to fix a bug, not to comply with a new law, not to stop a theft. Would you ever run a business on rules that cannot be changed? What would have to be true for that to be the right choice?

**Discussion Guidelines:**

Craft a substantive initial response (minimum 300 words) that stakes a clear position. Your response must include at least one scholarly or credible citation — a peer-reviewed paper, a law review article, a credible industry report, or documented case study of a protocol that revoked upgrade authority (or refused to). Citing "a blog post said" is not sufficient.

After posting your initial response, return and reply to at least **two peers** with substantive engagement. "I agree" is not a reply. Challenge a hidden assumption in their argument, offer a counterexample, or extend their reasoning to a context they did not consider.

Consider these angles as you write:
- Under what conditions does immutability actually serve users better than upgradeability?
- What legal jurisdictions have begun regulating smart contracts as binding agreements? How does upgrade authority interact with contract law?
- The DAO hack in 2016 and the subsequent Ethereum fork: was the fork a violation of code-is-law? What precedent did it set?
- Are there domains — real estate title records, medical consents, pension rules — where permanent, auditable, unalterable records are not just acceptable but desirable?
