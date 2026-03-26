# Wallet Passport — Product Requirements Document

**A portable Web3 identity credential built on wlltrep.xyz and wlltresume.xyz**

| Field | Detail |
|---|---|
| Author | Bojan Pilipovic |
| Status | Draft — Pre-development |
| Version | 0.1 |
| Date | March 2026 |
| Product Suite | wlltrep.xyz · wlltresume.xyz · Wallet Passport |

---

## 1. Executive Summary

Wallet Passport is the third product in a Web3 identity suite that includes wlltrep.xyz (private reputation scoring) and wlltresume.xyz (public onchain resume). While the first two products generate and display identity data, Wallet Passport makes that identity portable, verifiable, and composable across the Web3 ecosystem.

A Wallet Passport is a soulbound (non-transferable) NFT credential minted by a wallet that has met minimum reputation and activity thresholds. It cryptographically attests to the wallet's history, score, and qualifications — enabling trustless identity verification across DAOs, DeFi protocols, NFT projects, and Web3 hiring.

> **Core Value Proposition:** Turn your onchain history into a portable credential that other protocols can verify without trusting a centralized source. Your reputation, your keys, your passport.

---

## 2. Problem Statement

### 2.1 The Identity Gap in Web3

Web3 has a fundamental trust problem. Every interaction starts from zero — wallets are pseudonymous, histories are public but unstructured, and there is no standard way for a protocol to verify that a user meets minimum quality thresholds. This creates friction in three major areas:

- DAOs waste governance power on sybil attacks and low-quality voters
- DeFi protocols cannot offer tiered access or reduced collateral without identity
- NFT projects cannot reward genuine long-term holders over bots and flippers
- Web3 hiring has no standard credential — portfolios are scattered across wallets, GitHub, and PDF CVs

### 2.2 Why Existing Solutions Fall Short

| Solution | What they do | Gap |
|---|---|---|
| Gitcoin Passport | Aggregate Web2+Web3 stamps | Not onchain-native, requires Web2 accounts |
| Proof of Humanity | Verify unique humans | Identity only, no reputation layer |
| Orange Protocol | Reputation scores via oracle | Complex integration, no user product |
| Karma | DAO contributor scoring | DAO-specific, not portable |
| ENS | Human-readable addresses | Name only, no activity data |

---

## 3. Product Vision

> **Vision Statement:** Become the default onchain identity credential for EVM wallets — the Web3 equivalent of a verified LinkedIn profile, passport, and credit score combined.

### 3.1 The Suite Architecture

Wallet Passport is the third layer of a deliberate product stack:

| Layer | Product | Role |
|---|---|---|
| Layer 1 | wlltrep.xyz | Private reputation scoring. You connect your wallet and see your score. Builds trust with the user. |
| Layer 2 | wlltresume.xyz | Public identity presentation. A shareable resume from onchain data. Builds visibility. |
| Layer 3 | Wallet Passport | Portable verifiable credential. An NFT attesting your score and history. Builds composability and monetization. |

---

## 4. Target Users

### 4.1 Primary Users — Passport Holders

- Active DeFi users wanting reduced collateral requirements or whitelisted access
- DAO contributors seeking to prove governance credibility
- Web3 professionals using the Passport as a CV in hiring processes
- NFT collectors proving collector status and long-term holding history
- Any wallet with a wlltrep score above threshold wanting to prove it trustlessly

### 4.2 Secondary Users — Passport Verifiers (B2B)

- DAOs — gate voting, proposals, or delegate status behind Passport ownership
- DeFi protocols — offer reduced collateral or higher limits to Passport holders
- NFT projects — whitelist Passport holders for mints or early access
- Web3 hiring platforms — accept Passport as a verifiable credential
- Launchpads — use Passport for sybil-resistant allocation

---

## 5. Core Features — V1

### 5.1 Passport Minting

- Connects wallet to `passport.wlltresume.xyz`
- Checks eligibility: minimum rep score of 40, wallet age > 6 months, at least 50 transactions
- If eligible, user signs a transaction to mint a soulbound ERC-721 NFT
- NFT metadata includes: rep score tier, wallet age, chain activity, protocol categories, issue date
- Minting fee: 0.005 ETH (~$15) — primary monetization mechanism

> **Soulbound Design Note:** The Passport NFT is non-transferable (ERC-5192 standard) to prevent credential trading. The value comes from it being tied to the wallet's actual history, not from speculation.

### 5.2 Passport Tiers

| Tier | Score Range | Description |
|---|---|---|
| Bronze | 40–59 | Basic credential. Entry-level protocol gating. |
| Silver | 60–79 | Established wallet. Standard protocol integrations. |
| Gold | 80–94 | Power user. Premium protocol benefits and reduced collateral. |
| Diamond | 95+ | Elite tier. Maximum benefits, early access to integrations. |

### 5.3 Verification API

- REST endpoint: `GET /api/verify/0x...` returns `{ hasPassport, tier, score, issuedAt }`
- Protocols integrate this to gate access without building their own scoring
- Rate-limited free tier (100 req/day) — paid tier for higher volume
- On-chain verification also available via smart contract call

### 5.4 Passport Renewal

- Passports expire after 12 months to ensure they reflect current activity
- Renewal fee: 0.002 ETH — lower than initial mint
- Score is re-evaluated at renewal — tier can go up or down

---

## 6. Smart Contract Design

| Field | Detail |
|---|---|
| Standard | ERC-721 with ERC-5192 (Soulbound) extension |
| Network | Base L2 — low gas, EVM-compatible, growing ecosystem |
| Transferability | Non-transferable — transfer functions revert |
| Metadata | On-chain SVG for visual badge + IPFS JSON for full attestation |
| Upgradeability | Proxy pattern for score criteria updates |
| Audit | Required before mainnet — budget for third-party audit |

Minting eligibility is verified via a signed attestation from the wlltrep backend in V1, with a plan to move to fully on-chain Chainlink oracle verification in V2.

---

## 7. Monetization

| Stream | Detail |
|---|---|
| Passport Mint Fee | 0.005 ETH per mint (~$15). Primary revenue. Scales with adoption. |
| Renewal Fee | 0.002 ETH per year. Recurring revenue from existing holders. |
| Verification API | Free tier (100 req/day). Paid tier at $99/month unlimited. |
| Protocol Integrations | Revenue share or flat fee for white-label Passport gating. |
| Premium Tiers | Future: enhanced Passport with additional attestations. |

> **Revenue Projection (Conservative):** At 1,000 mints year 1: ~$15,000 mint revenue + $2,000 renewals. At 10,000 mints via wlltrep/wlltresume funnel: ~$150,000. API tier adds recurring SaaS revenue from protocol integrations.

---

## 8. Go-To-Market Strategy

### 8.1 Launch Funnel

- wlltresume.xyz user generates resume → sees *"Verify with Wallet Passport"* CTA
- wlltrep.xyz user gets score ≥ 40 → sees *"Mint your Passport"* CTA
- Passport holder shares tier badge on Twitter → viral loop begins
- DAOs/protocols integrate verification API → supply-side network effects

### 8.2 Partnership Strategy

- Target 3–5 DAOs for pilot integrations — offer free API access for public case study
- Approach NFT projects pre-mint — offer Passport-gated whitelist as a feature
- Web3 job boards (Bankless Jobs, Cryptocurrency Jobs) — Passport as credential standard

---

## 9. Roadmap

| Phase | Timeline | Milestones |
|---|---|---|
| Phase 0 — Foundation | Now | wlltrep.xyz + wlltresume.xyz live, cross-linked, stable |
| Phase 1 — Design | Month 1–2 | Smart contract design, audit brief, UI mockups, Base testnet |
| Phase 2 — Beta | Month 3–4 | Closed beta 100 wallets, testnet minting, API v1, feedback |
| Phase 3 — Launch | Month 5 | Mainnet on Base, minting live, first protocol integration |
| Phase 4 — Scale | Month 6–12 | API paid tier, 3+ integrations, V2 on-chain verification |

---

## 10. Risks & Mitigations

| Risk | Likelihood | Mitigation |
|---|---|---|
| Smart contract exploit | Medium | Third-party audit, bug bounty, proxy upgrades |
| Low adoption | Medium | Funnel from existing products, partnership integrations |
| Privacy backlash | Low–Medium | Clear messaging: all data is public onchain. Opt-in only. |
| Competitor copies model | Medium | First-mover advantage, network effects, brand trust |
| Alchemy API costs scale | Low | Score computed once at mint, cached in NFT metadata |

---

## 11. Success Metrics

| Metric | Target |
|---|---|
| Passports minted (Month 6) | 500+ on mainnet |
| Protocol integrations (Month 6) | 3+ active integrations |
| Mint conversion rate | > 5% of eligible wlltrep/wlltresume users |
| API calls/month (Month 6) | > 10,000 verifications |
| Renewal rate (Month 12) | > 60% of expired passports renewed |
| Revenue (Year 1) | > $20,000 across all streams |

---

## 12. Open Questions

- Should the Passport be soulbound or allow transfer with score reset?
- Which chain for V1 — Base (low gas) or Ethereum mainnet (credibility)?
- Should tier thresholds be fixed or community-governed via DAO?
- How to handle wallets that lose score after minting — revocation or visual downgrade?
- Separate domain (walletpassport.xyz) or keep under wlltresume.xyz?

---

*wlltrep.xyz · wlltresume.xyz · Wallet Passport*
