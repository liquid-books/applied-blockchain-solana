# Master Change Log — Edit Spec 2026-08 (Additive Pass)

**Executed:** August 31, 2026 · **Spec:** `EDIT-SPEC-2026-08.md` · **SOL constant:** $100

Per-chapter change logs with every insertion and old→new correction are in this directory:

- `ch00-02-CHANGELOG.md` — Ch 0 (blockchain lab, Enron/Findex/TPS fixes, bridge box), Ch 1 (Phantom fixes, L2 sentences, embedded wallets), Ch 2 (glossary directive conversion, memecoin section + lab Part 0, DePIN, RWA box), index.md (ch05 link 404 fix, $100 note)
- `ch03-04-CHANGELOG.md` — Ch 3 (Token-2022 section + decision table + PYUSD lab, Solana Compass fix), Ch 4 (demand-side section, Model Three Futures Step 5), `resources/ch04-tokenomics-model.xlsx` (4 tabs, live formulas)
- `ch05-CHANGELOG.md` — Ch 5 (pool types, MEV/sandwich, launchpads/bonding curves, managing liquidity, **Beyond the Pool: The DeFi Stack** ×7 subsections, Burn & Earn + RugCheck + pump.fun lab steps, **DeFi in an Afternoon** lab, 0.15 SOL pool-fee corrections, Serum removal, 30 glossary entries)
- `ch06-08-CHANGELOG.md` — Ch 6 (devnet note, tax box, cancel-stream demo, Sybil test), Ch 7 (Collab.Land/Matrica replacement, Solana Pay + Get Paid lab), Ch 8 (annotated lib.rs, PDAs/CPI, auditor box, token-gated stretch)
- `ch09-10-CHANGELOG.md` — Ch 9 (LaunchMyNFT replacement, Two Metaplex Standards, soulbound fix, compressed NFTs, Collab.Land Part 4), Ch 10 (Dune, Buyer's Check, DeFiLlama)
- `ch11-12-CHANGELOG.md` — Ch 11 (quadratic voting fix, UNI fix, treasury management, legal wrapper), Ch 12 (exemption map, FinCEN/MSB, regulatory snapshot, red-team extensions), `resources/lab-sites.md`

## Post-merge fixes (main editor)
- ch06: unresolved `{term}` cross-reference to FMV glossary entry → italic reference (glossary term name didn't match anchor format)
- ch07: bare `@everyone` was parsed as a citation → wrapped in backticks

## NEW IMAGES NEEDED (consolidated, 27 total — see per-chapter comments)
ch00-live-networks.png · ch01-embedded-wallets.png · ch02-memecoin-actor-table.png · ch03-token2022-extensions-table.png · ch04-demand-vs-supply-inflection.png · ch05-cpmm-vs-clmm.png · ch05-sandwich-attack.png · ch05-bonding-curve-migration.png · ch05-rugcheck-annotated.png · ch05-defi-stack-overview.png · ch05-stablecoin-backing-models.png · ch05-staking-yield-decomposition.png · ch05-lending-market-health-factor.png · ch05-oracle-flow.png · ch05-liquidation-cascade.png · ch06-tax-events.png · ch07-solana-pay-qr-flow.png · ch07-gating-platforms.png (UPDATE) · ch07-holder-setup.png (UPDATE) · ch08-pda-and-cpi.png · ch08-annotated-lib-rs.png · ch08-vulnerability-classes.png · ch09-compressed-nft-tree.png · ch10-buyers-check.png · ch11-treasury-runway.png · ch11-legal-wrappers.png · ch12-exemption-map.png · ch12-msb-decision-tree.png · ch12-regulatory-snapshot.png

## Hands-on audit (post-edit): 13 of 13 chapters have real build/do activities
- Ch 0: hash/block/chain/distributed manipulation + two live networks (NEW)
- Ch 1: wallet creation + first real transaction
- Ch 2: token brief + live memecoin analysis on DexScreener (NEW Part 0)
- Ch 3: mainnet token mint + PYUSD Token-2022 reading (NEW Step 8) + optional devnet Token-2022 mint (NEW 3b)
- Ch 4: three-futures model + demand column (NEW Step 5) + xlsx model (NEW)
- Ch 5: live Raydium pool + LP lock/RugCheck (NEW) + bonding-curve observation (NEW) + DeFi in an Afternoon: swap/stake/borrow/oracle/map (NEW)
- Ch 6: vesting streams + cancel demo (NEW) + airdrop + Sybil self-test (NEW)
- Ch 7: token-gated Discord door (Collab.Land) + Solana Pay payment received (NEW Part 2)
- Ch 8: deploy program + token-gated check-in stretch (NEW)
- Ch 9: mint NFT passes (LaunchMyNFT) + tier gating + compressed-collection reading (NEW Part 7)
- Ch 10: live dashboard + Dune/DeFiLlama (NEW) + Buyer's Check on own token (NEW)
- Ch 11: Squads multisig + Realms DAO + add-signer walkthrough (NEW) + treasury policy (NEW Part 4)
- Ch 12: red-team + Buyer's Check/phishing drill/regulator drill (NEW items 6-8)

Progressive build confirmed: one token, minted in Ch 3 on mainnet, used in every subsequent chapter through governance and legal review.
