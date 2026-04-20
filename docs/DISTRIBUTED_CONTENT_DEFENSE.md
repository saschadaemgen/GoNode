# GoNode Distributed Content Defense (DCD)

## A Privacy-Preserving, Legally Defensible Architecture for Unsolicited Media in Decentralized Messaging Networks

---

**Whitepaper v1.0 - Draft for Review**
**Part of the SimpleGo Ecosystem**
**Publisher:** IT and More Systems, Recklinghausen, Germany
**Author:** Sascha Dämgen with GoNode Contributors
**Date:** April 2026
**Status:** Technical Draft / Open for Public Comment
**Repository:** github.com/saschadaemgen/GoNode
**Contact:** contact@simplego.dev

---

## Table of Contents

- [Abstract](#abstract)
- [Executive Summary](#executive-summary)
  - [The core problem in one paragraph](#the-core-problem-in-one-paragraph)
  - [Why this is not an abstract concern](#why-this-is-not-an-abstract-concern)
  - [Why existing messengers have not solved this](#why-existing-messengers-have-not-solved-this)
  - [What this whitepaper proposes](#what-this-whitepaper-proposes)
  - [Why this is legally defensible](#why-this-is-legally-defensible)
  - [Document structure](#document-structure)

**Part I: Problem, Landscape, Legal Framework**

- [1. Introduction and Problem Statement](#1-introduction-and-problem-statement)
  - [1.1 The ambient vulnerability](#11-the-ambient-vulnerability)
  - [1.2 The escalation to weaponization](#12-the-escalation-to-weaponization)
  - [1.3 Scope of this whitepaper](#13-scope-of-this-whitepaper)
  - [1.4 Non-goals and ethical posture](#14-non-goals-and-ethical-posture)
- [2. Threat Landscape](#2-threat-landscape)
  - [2.1 The opportunistic abuse pattern](#21-the-opportunistic-abuse-pattern)
  - [2.2 The targeted planting pattern](#22-the-targeted-planting-pattern)
  - [2.3 The state-pretext pattern](#23-the-state-pretext-pattern)
  - [2.4 The WhatsApp Project Zero disclosure (January 2026)](#24-the-whatsapp-project-zero-disclosure-january-2026)
  - [2.5 Summary of the threat landscape](#25-summary-of-the-threat-landscape)
- [3. Comparative Analysis of Existing Messengers](#3-comparative-analysis-of-existing-messengers)
  - [3.1 SimpleX Chat](#31-simplex-chat)
  - [3.2 Signal](#32-signal)
  - [3.3 WhatsApp](#33-whatsapp)
  - [3.4 Matrix / Element](#34-matrix--element)
  - [3.5 Telegram](#35-telegram)
  - [3.6 Session (Oxen Foundation)](#36-session-oxen-foundation)
  - [3.7 Briar](#37-briar)
  - [3.8 Threema](#38-threema)
  - [3.9 Delta Chat](#39-delta-chat)
  - [3.10 Wire](#310-wire)
  - [3.11 XMPP clients (Conversations, Gajim, Dino)](#311-xmpp-clients-conversations-gajim-dino)
  - [3.12 Keybase](#312-keybase)
  - [3.13 Discord](#313-discord)
  - [3.14 Comparative summary](#314-comparative-summary)
- [4. Legal Framework](#4-legal-framework)
  - [4.1 Germany: Criminal law](#41-germany-criminal-law)
  - [4.2 Germany: Telecommunications and media law](#42-germany-telecommunications-and-media-law)
  - [4.3 European Union](#43-european-union)
  - [4.4 United States](#44-united-states)
  - [4.5 United Kingdom](#45-united-kingdom)
  - [4.6 Authoritarian jurisdictions](#46-authoritarian-jurisdictions)
  - [4.7 Summary of the legal framework](#47-summary-of-the-legal-framework)

**Part II: Design, Threat Model, Architecture**

- [5. Design Goals and Non-Goals](#5-design-goals-and-non-goals)
  - [5.1 Primary design goals](#51-primary-design-goals)
  - [5.2 Secondary design goals](#52-secondary-design-goals)
  - [5.3 Explicit non-goals](#53-explicit-non-goals)
  - [5.4 The solution in one page](#54-the-solution-in-one-page)
- [6. Formal Threat Model](#6-formal-threat-model)
  - [6.1 Assets](#61-assets)
  - [6.2 Adversaries](#62-adversaries)
  - [6.3 Spoofing threats and mitigations](#63-spoofing-threats-and-mitigations)
  - [6.4 Tampering threats and mitigations](#64-tampering-threats-and-mitigations)
  - [6.5 Repudiation threats and mitigations](#65-repudiation-threats-and-mitigations)
  - [6.6 Information disclosure threats and mitigations](#66-information-disclosure-threats-and-mitigations)
  - [6.7 Denial of service threats and mitigations](#67-denial-of-service-threats-and-mitigations)
  - [6.8 Elevation of privilege threats and mitigations](#68-elevation-of-privilege-threats-and-mitigations)
  - [6.9 Threat model summary](#69-threat-model-summary)

**Part III: Cryptography, Architecture, Protocols**

- [7. Cryptographic Foundations](#7-cryptographic-foundations)
  - [7.1 Notation](#71-notation)
  - [7.2 Symmetric primitives](#72-symmetric-primitives)
  - [7.3 Asymmetric primitives](#73-asymmetric-primitives)
  - [7.4 Reed-Solomon erasure coding](#74-reed-solomon-erasure-coding)
  - [7.5 Shamir's Secret Sharing for master keys](#75-shamirs-secret-sharing-for-master-keys)
  - [7.6 ECVRF for operator selection](#76-ecvrf-for-operator-selection)
  - [7.7 PDQ perceptual hash for known-bad content matching](#77-pdq-perceptual-hash-for-known-bad-content-matching)
  - [7.8 Double Ratchet and X3DH](#78-double-ratchet-and-x3dh)
  - [7.9 Summary of primitives](#79-summary-of-primitives)
- [8. System Architecture](#8-system-architecture)
  - [8.1 High-level component diagram](#81-high-level-component-diagram)
  - [8.2 Component responsibilities](#82-component-responsibilities)
  - [8.3 Trust model](#83-trust-model)
  - [8.4 Deployment topology](#84-deployment-topology)
- [9. Protocol Specifications](#9-protocol-specifications)
  - [9.1 Operator handshake protocol](#91-operator-handshake-protocol)
  - [9.2 Share upload protocol](#92-share-upload-protocol)
  - [9.3 Share retrieval protocol](#93-share-retrieval-protocol)
  - [9.4 Group join protocol](#94-group-join-protocol)
  - [9.5 Explicit fetch protocol](#95-explicit-fetch-protocol)
  - [9.6 Audit challenge protocol](#96-audit-challenge-protocol)
  - [9.7 Repair protocol](#97-repair-protocol)
  - [9.8 Summary of protocols](#98-summary-of-protocols)
- [10. Storage Layer: Distributed Erasure-Coded Design](#10-storage-layer-distributed-erasure-coded-design)
  - [10.1 Parameter choices](#101-parameter-choices)
  - [10.2 Share layout and metadata](#102-share-layout-and-metadata)
  - [10.3 Operator selection via ECVRF](#103-operator-selection-via-ecvrf)
  - [10.4 Jurisdiction declarations and metadata](#104-jurisdiction-declarations-and-metadata)
  - [10.5 Storage durability calculation](#105-storage-durability-calculation)
  - [10.6 Deletion semantics](#106-deletion-semantics)
  - [10.7 Repair economics](#107-repair-economics)
  - [10.8 Comparison with Storj and Sia](#108-comparison-with-storj-and-sia)
- [11. Client Layer: No Auto-Download and RAM-Only Rendering](#11-client-layer-no-auto-download-and-ram-only-rendering)
  - [11.1 The default contract](#111-the-default-contract)
  - [11.2 Silhouette generation](#112-silhouette-generation)
  - [11.3 Explicit fetch flow](#113-explicit-fetch-flow)
  - [11.4 Locked-memory buffer implementation](#114-locked-memory-buffer-implementation)
  - [11.5 Rendering surface](#115-rendering-surface)
  - [11.6 Cache policy for confirmed contacts](#116-cache-policy-for-confirmed-contacts)
  - [11.7 Uninstall and data clearing](#117-uninstall-and-data-clearing)
  - [11.8 Differences from existing messengers](#118-differences-from-existing-messengers)
- [12. Moderation Layer: TEE-Based Classification](#12-moderation-layer-tee-based-classification)
  - [12.1 TEE options surveyed](#121-tee-options-surveyed)
  - [12.2 TEE fragmentation problem](#122-tee-fragmentation-problem)
  - [12.3 DCD moderation architecture](#123-dcd-moderation-architecture)
  - [12.4 Classifier implementation](#124-classifier-implementation)
  - [12.5 Attestation protocol](#125-attestation-protocol)
  - [12.6 Flag propagation](#126-flag-propagation)
  - [12.7 Accountability and appeal](#127-accountability-and-appeal)
  - [12.8 Legal defensibility of the moderation approach](#128-legal-defensibility-of-the-moderation-approach)
- [13. Hash Matching Against Known-Bad Content](#13-hash-matching-against-known-bad-content)
  - [13.1 Hash function selection](#131-hash-function-selection)
  - [13.2 Known-bad list sourcing](#132-known-bad-list-sourcing)
  - [13.3 List distribution](#133-list-distribution)
  - [13.4 Client-side comparison](#134-client-side-comparison)
  - [13.5 Constant-time comparison for privacy](#135-constant-time-comparison-for-privacy)
  - [13.6 Match outcome](#136-match-outcome)
  - [13.7 False positive handling](#137-false-positive-handling)
  - [13.8 Hash list transparency](#138-hash-list-transparency)
  - [13.9 Limits of the approach](#139-limits-of-the-approach)

**Part IV: Economics, Compliance, Comparison**

- [14. Economic Model: Stake-Based Operator Participation Without Tokens](#14-economic-model-stake-based-operator-participation-without-tokens)
  - [14.1 Why no native token](#141-why-no-native-token)
  - [14.2 Stake mechanics](#142-stake-mechanics)
  - [14.3 Payment for service](#143-payment-for-service)
  - [14.4 Slashing conditions](#144-slashing-conditions)
  - [14.5 Distribution of slashed stake](#145-distribution-of-slashed-stake)
  - [14.6 Governance model](#146-governance-model)
  - [14.7 Comparison with token-based projects](#147-comparison-with-token-based-projects)
  - [14.8 Long-term sustainability](#148-long-term-sustainability)
- [15. Legal Compliance Strategy](#15-legal-compliance-strategy)
  - [15.1 Germany](#151-germany)
  - [15.2 European Union](#152-european-union)
  - [15.3 United States](#153-united-states)
  - [15.4 United Kingdom](#154-united-kingdom)
  - [15.5 Compliance matrix](#155-compliance-matrix)
  - [15.6 Open legal questions](#156-open-legal-questions)
- [16. Comparison Matrix: DCD vs Existing Messengers](#16-comparison-matrix-dcd-vs-existing-messengers)
  - [16.1 Evaluation criteria](#161-evaluation-criteria)
  - [16.2 Comparison table](#162-comparison-table)
  - [16.3 Analysis](#163-analysis)
  - [16.4 Relative performance costs](#164-relative-performance-costs)
  - [16.5 Conclusion of comparison](#165-conclusion-of-comparison)

**Part V: Roadmap, Future Work, Conclusion**

- [17. Implementation Roadmap](#17-implementation-roadmap)
  - [17.1 Phase 0: Specification and prototyping (months 0-3)](#171-phase-0-specification-and-prototyping-months-0-3)
  - [17.2 Phase 1: Alpha deployment (months 3-9)](#172-phase-1-alpha-deployment-months-3-9)
  - [17.3 Phase 2: Beta with public operator onboarding (months 9-15)](#173-phase-2-beta-with-public-operator-onboarding-months-9-15)
  - [17.4 Phase 3: Mainnet launch (months 15-24)](#174-phase-3-mainnet-launch-months-15-24)
  - [17.5 Phase 4: Maturity and immutability (months 24-36)](#175-phase-4-maturity-and-immutability-months-24-36)
  - [17.6 Risk factors and mitigations](#176-risk-factors-and-mitigations)
  - [17.7 Parallel work streams](#177-parallel-work-streams)
- [18. Open Problems and Future Work](#18-open-problems-and-future-work)
  - [18.1 Residual risk: Threshold collusion](#181-residual-risk-threshold-collusion)
  - [18.2 Residual risk: TEE fragmentation limits moderation](#182-residual-risk-tee-fragmentation-limits-moderation)
  - [18.3 Residual risk: Novel content not in hash list](#183-residual-risk-novel-content-not-in-hash-list)
  - [18.4 Residual risk: Adversarial perturbation of known content](#184-residual-risk-adversarial-perturbation-of-known-content)
  - [18.5 Residual risk: Legal evolution](#185-residual-risk-legal-evolution)
  - [18.6 Residual risk: Client-device compromise](#186-residual-risk-client-device-compromise)
  - [18.7 Future work: Post-quantum upgrades](#187-future-work-post-quantum-upgrades)
  - [18.8 Future work: Integration with Matrix federation](#188-future-work-integration-with-matrix-federation)
  - [18.9 Future work: Fully-homomorphic filtering](#189-future-work-fully-homomorphic-filtering)
  - [18.10 Call for partners](#1810-call-for-partners)
- [19. Conclusion](#19-conclusion)

**References and Appendices**

- [References](#references)
  - [Academic papers and peer-reviewed sources](#academic-papers-and-peer-reviewed-sources)
  - [Standards and RFCs](#standards-and-rfcs)
  - [Legal sources](#legal-sources)
  - [Technical documentation](#technical-documentation)
  - [News and investigative sources](#news-and-investigative-sources)
- [Appendix A: Wire format summary](#appendix-a-wire-format-summary)
- [Appendix B: Selected legal text excerpts](#appendix-b-selected-legal-text-excerpts)
  - [B.1 §184b StGB (Germany)](#b1-184b-stgb-germany)
  - [B.2 DSA Article 4 (Mere conduit)](#b2-dsa-article-4-mere-conduit)
  - [B.3 GDPR Article 32](#b3-gdpr-article-32)
  - [B.4 18 U.S.C. §2252A(a)(5)(B)](#b4-18-usc-2252aa5b)
- [Appendix C: Threat model extended tables](#appendix-c-threat-model-extended-tables)
  - [C.1 Asset-Adversary matrix](#c1-asset-adversary-matrix)
  - [C.2 Defence-in-depth summary](#c2-defence-in-depth-summary)
- [Appendix D: Glossary](#appendix-d-glossary)

---


## Abstract

Secure messengers today ship with a design flaw that has become a weaponizable attack vector: by default, profile pictures, avatars, and media attachments are automatically downloaded and written to persistent client storage the moment a user becomes visible inside a group. In jurisdictions where mere possession of certain content is a strict-liability offence (§184b StGB in Germany, 18 U.S.C. §2252A in the United States, comparable provisions in over 120 jurisdictions), this default behavior transforms every group membership into a potential criminal liability and every hostile actor into a potential framer. The problem is well documented inside the issue trackers and RFC folders of every major messenger project, is privately acknowledged by their maintainers, and remains unresolved in production for reasons that are part technical, part commercial, and part jurisdictional.

This whitepaper specifies **GoNode Distributed Content Defense (DCD)**, a six-layer defence-in-depth architecture that integrates into the GoNode decentralized service-node network deployed by the SimpleGo Ecosystem. DCD combines: (1) an opt-in retrieval model where no media is auto-downloaded for unconfirmed contacts, (2) ephemeral RAM-only rendering using `mlock(2)` and `explicit_bzero(3)` with zero disk persistence, (3) a (3,5) Reed-Solomon erasure coding scheme with per-share AEAD encryption distributed across five independent operator jurisdictions such that no single node ever holds reconstructible plaintext, (4) client-side perceptual hashing against the NCMEC hash list and Meta's open-source PDQ hash database executed prior to render, (5) optional TEE-based moderation using ARM TrustZone, Apple Secure Enclave, or Intel SGX where the moderator's host OS never observes plaintext, and (6) a stake-based, non-token operator economic model that deliberately avoids MiCA classification as a crypto-asset.

We show that this architecture (a) prevents illegal content from ever reaching persistent client storage, (b) makes distributed-storage operators individually incapable of reconstructing user content (thus satisfying common-carrier and mere-conduit doctrines under the EU Digital Services Act Articles 4 and 6, and 47 U.S.C. §230), (c) supports lawful moderation workflows that comply with DSA Article 16 notice-and-action, and (d) withstands the threat models faced by journalists, dissidents, and opposition figures in jurisdictions where planted evidence is a documented prosecution tactic.

The whitepaper provides verifiable citations for every claim about existing messenger behavior (GitHub issues, RFC documents, CVE numbers), every legal provision (paragraph numbers, official gazette references), and every cryptographic construction (peer-reviewed papers or NIST standards). We also address the open problems we cannot yet solve and state honestly where the architecture has residual risk.

---

## Executive Summary

### The core problem in one paragraph

When Alice joins Bob's group on any major secure messenger in 2026 (SimpleX, Signal, Matrix, Telegram, WhatsApp, Wire, Threema, Delta Chat, Session, Briar), Bob's client automatically fetches Alice's profile picture and media thumbnails for unread messages and writes them to persistent storage. If Alice is a hostile actor and her profile picture is Child Sexual Abuse Material (CSAM), or if she posts CSAM and Bob's client auto-caches the preview, then Bob's device now contains illegal content. Under German §184b StGB (1) as amended on 28 June 2024 (BGBl. 2024 I Nr. 213), mere possession is punishable by a minimum of three months and up to five years of imprisonment even where the content depicts non-real events, and up to ten years where the content depicts real events. Under 18 U.S.C. §2252A (a)(5)(B), possession in the United States carries up to ten years for a first offence and up to twenty years for subsequent offences. Intent is relevant to sentencing but not to the elements of the offence in most jurisdictions, and forensic artifacts such as cache timestamps routinely form the core of the prosecution case, as discussed in recent practitioner guidance [Envista Forensics 2026]. The practical consequences for an affected user, regardless of eventual acquittal, include device seizure, pre-trial detention, professional destruction, and social ostracisation.

### Why this is not an abstract concern

The threat model is not speculative. On 27 January 2026, Malwarebytes reported on a Google Project Zero disclosure of a WhatsApp vulnerability in which "a malicious media file, sent into a newly created group chat, can be automatically downloaded and used as an attack vector" [Malwarebytes 2026a]. In 2019, Russian investigative journalist Ivan Golunov of the independent outlet Meduza was arrested on drug-dealing charges after narcotics were planted in his backpack and apartment by five officers of the Moscow anti-drug unit; the charges were dropped after mass protests, the officers were later convicted of evidence fabrication and sentenced to between five and twelve years, and the Russian Investigative Committee formally confirmed the drugs had been "illegally acquired, stored and transported" for the purpose of framing him [Moscow Times 2020, RFE/RL 2020, Moscow Times 2021]. Evidence planting against inconvenient figures is not a conspiracy theory in many jurisdictions, it is a documented and prosecuted pattern; the Golunov case was unusual only in that it was prosecuted. Digital CSAM planting is the information-age equivalent of planting physical contraband, with the decisive advantages that (a) it requires no physical access, (b) the evidence self-replicates through cache mechanisms, and (c) strict-liability statutes foreclose intent-based defences.

### Why existing messengers have not solved this

The SimpleX Chat team published an official Request for Comments on content moderation dated 30 December 2024 [SimpleX 2024, commit 821f034d1]. The RFC documents the current SimpleX approach (user complaints routed to an automated bot that joins public groups and deletes files via a server control port) and acknowledges candidly that "nothing prevents users who created such group to create a new one" and that the current method "will not be sustainable once we add support for large groups" [SimpleX 2024]. The RFC then enumerates future options including blocking records, client-side restrictions, and denylist servers, but none of the enumerated options address the core issue identified in this whitepaper: once a file has been automatically fetched and cached by a recipient client, the damage is done. The SimpleX RFC itself concedes that "users can configure automatic deletion of messages with blocked files" as a future option, which implicitly confirms that current behavior retains auto-fetched content on disk.

Signal's approach to media auto-download is configurable per network type via Settings > Data and Storage > Media auto-download [Signal Support 2024], but the defaults enable auto-download for photos on Wi-Fi and, in Signal's own words from GitHub issue 8714 [Signal-Android #8714], media auto-download applies by default, with any files under 100 KB being fetched regardless of user preference. WhatsApp defaults to auto-download of photos on all networks and has suffered a long chain of CVEs involving automatic media processing, including CVE-2019-11932 (double-free GIF parsing, remote code execution), CVE-2025-30401 (MIME/extension spoofing in WhatsApp for Windows), and the September 2025 zero-click exploit chain combined with Apple's ImageIO vulnerability [Malwarebytes 2025]. Matrix, Wire, Threema, and Telegram exhibit similar defaults to varying degrees, as we catalogue systematically in Section 3.

### What this whitepaper proposes

GoNode Distributed Content Defense is a six-layer architecture specified for integration into the GoNode service-node network, an open-source decentralized storage and routing layer maintained by IT and More Systems under AGPL-3.0. The six layers are:

1. **No auto-download for unconfirmed contacts.** Profile pictures default to a deterministic silhouette placeholder derived from a colour-hash of the user's public key. Media from non-whitelisted contacts is never fetched without explicit user action.

2. **Ephemeral RAM-only rendering.** When media is explicitly requested, the shares are reassembled in a locked memory buffer (`mlock(2)` on POSIX, `VirtualLock` on Windows), rendered via zero-copy framebuffer, and the buffer is overwritten with `explicit_bzero(3)` upon closure. No disk cache is written for unconfirmed contacts.

3. **Distributed (3,5) erasure coding with per-share encryption.** Every uploaded media blob is processed as follows: the plaintext is encrypted with a random 256-bit XChaCha20-Poly1305 key; the ciphertext is split into five shares via a (3,5) Reed-Solomon code over GF(2^8); each share is independently re-encrypted with a share-specific subkey derived via HKDF-SHA-256 from the master key; the five shares are distributed to five independent operators selected deterministically via ECVRF; the master key is itself split using Shamir's (3,5) threshold secret sharing and the key shares are encrypted to the recipient's static public key and bundled with the file shares. Any subset of two or fewer shares yields zero information about the plaintext; any three or more shares enable full reconstruction.

4. **Client-side perceptual hashing against known-bad content.** Before any reconstructed plaintext is rendered, the client computes the PDQ perceptual hash [Meta ThreatExchange] and compares against a locally-distributed hash list sourced from NCMEC's CyberTipline partnerships and the Internet Watch Foundation. A match aborts the render and triggers a report-to-upstream workflow that never reveals the plaintext to anyone.

5. **Optional TEE-based moderation.** Group administrators who opt into moderator duties run a classifier inside a Trusted Execution Environment (ARM TrustZone on mobile, Intel SGX or AMD SEV on server, Apple Secure Enclave on iOS). The host OS observes only a Boolean classifier output plus a signed attestation.

6. **Stake-based operator economics without tokens.** Operators post a EUR-denominated stake to a smart contract deployed on Arbitrum One. Payment occurs in EURC (MiCA-compliant e-money token per Circle Internet Financial's EMI license) or USDC. There is no GoNode-native token with floating value. This design choice is deliberate and discussed in Section 14.

### Why this is legally defensible

The architecture satisfies three converging legal tests:

- **Mere conduit under DSA Article 4 and §8 TMG (Germany).** Individual GoNode operators, holding only a single encrypted share of a file and lacking two of the three shares required for reconstruction, satisfy the definition of "transient storage of information" that "does not modify the information" and "is not for longer than reasonably necessary." No single operator can meaningfully "know" what they are storing.

- **Technical organisational measures per Article 32 GDPR.** Encryption at rest, distribution across jurisdictions, share-level access controls, and hash-based content filtering collectively establish a demonstrable standard of care.

- **Avoidance of client-side mass scanning.** By restricting hash-matching to content explicitly fetched by the user and by never scanning incoming or outgoing communications at the device level without user action, DCD avoids the constitutional and European Convention on Human Rights Article 8 issues that have repeatedly defeated the EU's "Chat Control" proposal, most recently on 31 October 2025 when Denmark backed away from mandatory scanning after firm opposition from Germany, and then definitively on 3 April 2026 when the voluntary scanning derogation (EU Regulation 2021/1232) expired without renewal [State of Surveillance 2026].

### Document structure

This document proceeds in nineteen substantive sections plus appendices. Sections 1-4 establish the problem, the threat landscape, the state of existing messengers, and the legal framework. Sections 5-7 define design goals, formal threat model, and cryptographic foundations. Sections 8-14 specify the system architecture, protocols, storage, client, moderation, hashing, and economics. Sections 15-16 address legal compliance by jurisdiction and compare DCD against existing systems. Sections 17-19 cover implementation roadmap, open problems, and conclusions. Appendices contain protocol wire formats, full legal citations, and threat model tables.

---

# 1. Introduction and Problem Statement

## 1.1 The ambient vulnerability

The modern secure messenger is a product of approximately fifteen years of iteration by several distinct engineering communities: the Signal Foundation and its predecessors TextSecure and RedPhone; the Matrix.org Foundation; Open Whisper Systems; the Telegram team; WhatsApp under Meta (formerly Facebook); the Threema team; the Wire team; the Session team at the Oxen Foundation; the Briar Project; the SimpleX team; and a long tail of XMPP-based projects including Conversations, Gajim, Dino, and Prosody. These projects disagree strongly about architecture, cryptographic choices, metadata handling, account identity, and business model. They converge, with almost no exceptions, on a single user-experience design decision: **new media arriving at the client should be pre-fetched and cached on local storage so that the user sees it immediately when they open the conversation**.

This convergence exists for three reasons. First, network conditions on mobile are unreliable; pre-fetching reduces perceived latency and produces a more responsive product. Second, the unit economics of mobile data in most jurisdictions in 2010 favoured pre-fetching over on-demand retrieval because the marginal data cost of fetching a small thumbnail was low relative to the user-experience value. Third, the alternative, on-demand retrieval with placeholder rendering, requires more complex UI state management and is therefore engineering-expensive.

The cost of this default, borne almost entirely by the user and not by the messenger vendor, is that a third party in possession of the means to deliver media into the target's conversation view can cause that media to be written to persistent storage on the target's device without any action by the target and often without any visible indication. In almost every jurisdiction where the messenger operates, that written file has legal consequences if it is of the wrong type.

## 1.2 The escalation to weaponization

Until approximately 2019, the principal concern with unsolicited media was that it could carry exploits capable of remote code execution. CVE-2019-11932 in WhatsApp for Android (double-free in GIF parser, automatic triggering if the sender is a contact) [Awakened 2019] and the Pegasus-related zero-click chains against iOS ImageIO have been the archetypes. This threat model is well understood by security teams, and the mitigations (hardened parsers, sandboxing, sandboxed renderers, frequent patching) are reasonably mature, though incompletely deployed.

The threat model we address in this whitepaper is orthogonal and, in an important sense, worse. It does not require any vulnerability in the parser or the rendering stack. It requires only that the messenger behave according to its documented specification: receive media, write to cache, generate thumbnail, display. If the attacker substitutes a payload where "payload" means "a file whose existence on the target's device is a criminal offence" rather than "a file whose parsing triggers arbitrary code execution," the messenger's correctness is the attacker's tool.

The earliest public documentation of this style of attack that we have been able to verify is in discussions of Signal group invitation spam in approximately 2018-2019, and in Russian-language threat modelling by opposition-linked security trainers who began advising journalists around 2020 to disable media auto-download as a specific defence against "image-planting operations." By 2023, the concern had surfaced publicly in SimpleX Chat's own issue tracker in the context of large public groups and CSAM abuse. By December 2024, SimpleX had published its RFC on content moderation [SimpleX 2024]. By January 2026, Google Project Zero had disclosed the zero-click group-chat media download vulnerability in WhatsApp [Malwarebytes 2026a]. The attack surface is now publicly known, publicly discussed, and publicly unresolved.

## 1.3 Scope of this whitepaper

We address the problem of **unsolicited illegal media in decentralized and federated messenger networks**, with specific focus on three sub-problems:

1. **Profile-picture poisoning**, where a new group member's avatar is illegal content, triggering auto-fetch by all existing members.
2. **Group-media poisoning**, where an actor inside a group posts illegal media that is auto-fetched by all members before moderators can act.
3. **Targeted planting**, where an attacker knowing a target's public identifier (user ID, public key fingerprint, phone number depending on messenger) joins a shared group or initiates contact and posts illegal media with the specific intent to create evidence against the target.

We do not, in this whitepaper, address:

- Mass-scale CSAM distribution through clearnet or darknet hosting (outside scope; addressed by existing NCMEC, IWF, and law enforcement workflows).
- Grooming behavior detection (requires semantic analysis of communications and is widely considered inconsistent with end-to-end encryption).
- Client-side parser vulnerabilities (addressed by standard sandboxing and patching practices).
- Content moderation for legal-but-objectionable content (handled by per-group moderator tools).

## 1.4 Non-goals and ethical posture

We state explicitly and without equivocation that this whitepaper's purpose is **to prevent the weaponization of unsolicited media against users**, not to facilitate distribution of illegal content. The architecture described is harder for offenders to abuse than current messengers because (a) hash-matching against known-bad content is executed before rendering, (b) moderators gain structured reporting workflows they currently lack, and (c) operator-side deniability is paired with aggressive client-side filtering rather than replacing it.

The authors are based in the Federal Republic of Germany, operate under German law, and are committed to compliance with §184b-§184l StGB, the EU Digital Services Act, and the General Data Protection Regulation. We believe and argue in Section 15 that DCD is more compliant with the balance struck by these regimes than the current auto-download-everything default, because DCD embeds the "technical organisational measures" contemplated by GDPR Article 32 into the transport layer rather than relying on post-hoc takedown.

---

# 2. Threat Landscape

This section documents the threat landscape with primary-source citations. We distinguish between three threat actors: (a) the opportunistic abuser who uses illegal content for personal reasons and whose victims are incidental, (b) the targeted adversary who plants content against a specific person for a specific reason, and (c) the state-level actor who uses planted or auto-cached content as a pretext for prosecution, device seizure, or professional destruction.

## 2.1 The opportunistic abuse pattern

SimpleX Chat's own RFC of 30 December 2024 states, and we quote the relevant passage as a technical reference [SimpleX 2024]:

> "Most CSAM distribution in all communication networks happens in publicly accessible channels, and it's the same for SimpleX network."

This is consistent with the pattern observed across Telegram public channels, Discord public servers, WhatsApp community groups, and Matrix public rooms. The opportunistic abuser does not target any particular victim; they seek distribution reach. The victim population is "everyone who joined the group," which in SimpleX's own analysis includes groups of up to 100,000 members in their design target. For a user who joins a nominally-innocuous group that has been quietly infiltrated by abusers, their client begins auto-fetching whatever media is posted, and the cache state of the victim's device is determined by the activity of strangers.

## 2.2 The targeted planting pattern

The targeted planting pattern has been the subject of security trainings for journalists since at least 2020, though it has been difficult to document individual cases because (a) planted-CSAM cases rarely result in public vindication of the victim, (b) the plausible deniability of "yes but maybe they actually did want it" is very hard to rebut in court, and (c) victims face overwhelming pressure to plea-bargain rather than litigate.

We document the adjacent and well-verified pattern of physical evidence planting against journalists as a model:

The case of Ivan Golunov is the most fully-documented modern example. Golunov, an investigative journalist for the independent outlet Meduza covering corruption in Moscow law enforcement, was arrested on 6 June 2019 on drug-dealing charges. Mephedrone and cocaine were claimed to have been found in his backpack and apartment. Golunov was released after mass protests; the charges were dropped. Between January 2020 and May 2021, five officers of the Moscow anti-drug unit (Denis Konovalov, Akbar Sergaliyev, Roman Feofanov, Maksim Umetbayev, and their supervisor Igor Lyakhovets) were arrested, charged, and ultimately convicted of abuse of authority, fabrication of evidence, and drug possession. Sentences ranged from five to twelve years. The Russian Investigative Committee stated that the drugs "had been illegally acquired, stored and transported" for the specific purpose of framing Golunov [Moscow Times 2020, RFE/RL 2020, Moscow Times 2021]. In December 2022, Moscow City Court ruled Russia's Interior Ministry liable for 1.5 million rubles in damages [Moscow Times 2023].

The Golunov case is a watershed because it ended with actual convictions of the officers who planted evidence. The more ordinary outcome, in most jurisdictions, is that planted evidence prompts prosecution of the target and either a conviction or a plea bargain, with no subsequent investigation of how the evidence came to be there.

Digital CSAM planting is easier than physical drug planting on almost every axis:

- **No physical access required.** The attacker needs only a network identifier (phone number for WhatsApp, public key fingerprint for SimpleX, user ID for Signal/Matrix, etc.).
- **Low operational cost.** The attacker does not need to acquire illegal content at personal risk; known-bad CSAM circulates in the same underground channels as the opportunistic pattern, so the marginal cost of using some for planting is near zero.
- **Self-replicating evidence.** The target's own messenger creates the persistent artifact automatically.
- **Strict-liability defence posture.** In most jurisdictions, the fact that the content was auto-fetched rather than deliberately acquired is relevant to sentencing but not to the elements of the offence, meaning the defendant still bears the burden of proving they did not know, and prosecutors still have a headline they can run.

## 2.3 The state-pretext pattern

In jurisdictions where the rule of law is fragile or selectively applied, the existence of auto-fetched illegal material on a device is a law-enforcement pretext rather than a prosecutable crime in the ordinary sense. The Pegasus Project, coordinated by Forbidden Stories and documented in peer-reviewed research [Harvard Human Rights Journal 2023], identified at least 180 journalists in twenty countries targeted with NSO Group surveillance products. Surveillance deployments often precede pretextual prosecution. A device seizure following a pretextual prosecution will find whatever is on the device, which in the case of a major messenger includes a multi-gigabyte cache of material the user did not choose.

Documented cases of pretextual prosecution of journalists and dissidents in Belarus, Turkey, Russia, Iran, China, and Egypt are compiled annually by Reporters Without Borders (Reporters sans frontières) [RSF Press Freedom Index 2025], the Committee to Protect Journalists, and Amnesty International. We do not reproduce the full catalogue here. We note that the combination of (a) state-level targeting, (b) a messenger that auto-caches anything arriving in a group, and (c) an attacker who knows the target's group memberships or phone number, is a turnkey framing kit in 2026.

## 2.4 The WhatsApp Project Zero disclosure (January 2026)

On 27 January 2026, Malwarebytes published a summary of a Google Project Zero disclosure concerning WhatsApp on Android [Malwarebytes 2026a]. Project Zero identified that "WhatsApp can download a malicious media file without you doing anything at all. The bug affects WhatsApp on Android and involves zero-click media downloads in group chats. You can be attacked simply by being added to a group and having a malicious file sent to you." Project Zero assessed that the attack "is most likely to be used in targeted campaigns, since the attacker needs to know or guess at least one contact" but noted that it "is relatively easy to repeat once an attacker has a likely target list." The disclosure was accompanied by CVE-tracking for the underlying media-parsing flaw; the attack vector, however, was the auto-download behavior itself, not any specific parser bug.

This is the clearest recent public confirmation from an uncontroversial source (Project Zero is a Google team with no commercial stake in the outcome) that the threat model described in this whitepaper is not theoretical.

## 2.5 Summary of the threat landscape

| Threat actor | Motivation | Capability | Documented examples |
|:-------------|:-----------|:-----------|:--------------------|
| Opportunistic abuser | Personal / ideological | Low: account creation and group-join | SimpleX RFC 2024 |
| Targeted adversary | Personal grievance, financial, political | Medium: requires target identifier | Journalist trainings since 2020 |
| Corporate adversary | Commercial sabotage | Medium: requires target identifier and patience | Anecdotal, rarely publicized |
| State-level actor (lawful) | Lawful prosecution | High: can compel provider cooperation | Varies by jurisdiction |
| State-level actor (pretextual) | Silencing journalists / dissidents | Very high: full surveillance, physical access | Pegasus Project 2021; Golunov (drug analogy) 2019 |

All of these actors are aided, not hindered, by a messenger that auto-caches media without user action.

---

# 3. Comparative Analysis of Existing Messengers

This section surveys the auto-download and media-caching behavior of thirteen significant messaging systems. For each, we identify: (a) the documented default behavior with respect to media auto-download, (b) the configurability available to the user, (c) known incidents or vulnerability disclosures, and (d) issue-tracker or RFC references that show the problem is acknowledged.

## 3.1 SimpleX Chat

**Repository:** github.com/simplex-chat/simplex-chat
**Language:** Haskell (core), Kotlin (Android), Swift (iOS)
**Model:** No persistent user identity; SMP (SimpleX Messaging Protocol) servers; XFTP for file transfer.

**Default behavior:** SimpleX Chat auto-downloads group members' profile pictures upon group-join, which has been the subject of multiple community discussions. Media auto-download for files is governed by a user setting with default thresholds, but profile pictures are treated as metadata and fetched automatically as part of group roster synchronization.

**Official acknowledgement:** The SimpleX team published an RFC titled "Evolving content moderation" at `docs/rfcs/2024-12-30-content-moderation.md` [SimpleX 2024]. The RFC is the single most candid document published by any mainstream messenger on this issue. We quote directly:

> "As the users and groups grow, and particularly given that we are planning to make large (10-100k members) groups work, the abuse will inevitably grow as well."

And regarding the limits of their current approach:

> "The limitation of this approach is that nothing prevents users who created such group to create a new one, and communicate the link to the new group to the existing members so they can migrate there. While this whack-a-mole game has been working so far, it will not be sustainable once we add support for large groups."

The RFC then enumerates possible future measures including `BLOCK` protocol commands, client-side restrictions on senders whose files were blocked, server-side blocking records propagated to receiving clients, and the ability to configure "automatic deletion of messages with blocked files." Notably, the RFC does not commit to eliminating auto-download for unconfirmed contacts; it proposes reactive mechanisms that act after a file has been identified as abusive.

**Other issues:** SimpleX Chat Issue #6207 (20 August 2025) documents a Linux-specific problem with changing profile pictures, but is not directly relevant to the core problem. Issue #4328 (15 June 2024) documents 32-bit device issues with profile pictures and webview. The relevant technical capability, that profile pictures are fetched automatically and cached locally, is confirmed across the issue tracker.

**Known hardening issues:** The user community has identified conflicts between SimpleX's libsodium usage and the `hardened_malloc` library on GrapheneOS that historically consumed up to 2.6 GB of RAM under load. This is a memory-safety-adjacent issue rather than an auto-download issue per se, but it is relevant because it suggests that the Haskell GHC runtime's interaction with hardened allocators is incompletely resolved.

## 3.2 Signal

**Repositories:** github.com/signalapp/Signal-Android, Signal-iOS, Signal-Desktop
**Language:** Java/Kotlin, Swift, TypeScript
**Model:** Phone-number identity, Signal Protocol for E2EE, centralised server.

**Default behavior:** Signal auto-downloads profile pictures for all contacts by default. For attachments, Signal's default is to auto-download images and voice notes on Wi-Fi and mobile data, videos on Wi-Fi only, and documents on Wi-Fi only [Signal Support 2024]. Crucially, Signal GitHub Issue #8714 (27 March 2019) and subsequent community discussion establish that files under 100 KB are auto-downloaded regardless of user-configured settings, for reasons related to the Signal team's (entirely legitimate) desire to ensure link previews and small system messages render correctly. Profile pictures, being typically under 100 KB, fall in this auto-fetch category.

**Configurability:** Settings > Data and Storage > Media auto-download allows per-network-type configuration for Photos, Audio, Video, and Documents. Profile pictures are not user-configurable in the same way.

**Known incidents:** Signal's security record is among the best in the industry; the primary auto-download concern is design rather than implementation. Sealed Sender (Signal's feature to minimize sender metadata on the server) does not alter the recipient-side cache behavior.

## 3.3 WhatsApp

**Vendor:** Meta Platforms, Inc.
**Model:** Phone-number identity, Signal Protocol for E2EE (with Meta's extensions), Meta-operated servers.

**Default behavior:** WhatsApp auto-downloads photos on all networks by default; videos and documents are auto-downloaded on Wi-Fi. Auto-download is user-configurable in Settings > Storage and Data > Media auto-download.

**Known incidents:** WhatsApp has the longest public record of auto-download-related CVEs among major messengers, primarily because its user base is the largest target. Notable entries include:

- **CVE-2019-11932:** Double-free in GIF parsing library (libpl_droidsonroids_gif). Triggered by receiving a malicious GIF, which was auto-downloaded if the sender was in the contact list. Patched in WhatsApp for Android 2.19.244 [Awakened 2019].
- **CVE-2025-30401:** MIME-type vs filename-extension spoofing in WhatsApp for Windows. Attachment could display as an image but execute as code when opened. Patched in 2.2450.6 [Help Net Security 2025].
- **September 2025 zero-click:** Undisclosed CVE combined with Apple's ImageIO flaw for targeted attacks against WhatsApp users [Malwarebytes 2025].
- **January 2026 Project Zero disclosure:** Zero-click group-chat media download attack vector [Malwarebytes 2026a]. We quote:

> "Google's Project Zero has just disclosed a WhatsApp vulnerability where a malicious media file, sent into a newly created group chat, can be automatically downloaded and used as an attack vector. The bug affects WhatsApp on Android and involves zero-click media downloads in group chats. You can be attacked simply by being added to a group and having a malicious file sent to you."

This disclosure is the most direct confirmation of the threat model in this whitepaper.

**Configurability:** Auto-download can be disabled per network type, but profile pictures and small thumbnails remain auto-fetched.

## 3.4 Matrix / Element

**Protocol:** Matrix, specified at spec.matrix.org
**Reference clients:** Element (Web, iOS, Android), various third-party clients
**Model:** Federated servers, per-server homeserver model, MegOlm for E2EE in rooms.

**Default behavior:** Element clients auto-download thumbnails for media attachments and auto-fetch profile pictures for all room members upon joining. Full-resolution media is typically fetched on view, not on receive, but thumbnails are fetched by default and cached. For a room with 1000 members and 10 media posts per day, this represents significant background fetching.

**Matrix Spec Changes (MSCs):** The Matrix protocol has no current MSC dedicated to changing default auto-download behavior for hostile-content scenarios. MSC2589 and related proposals address media repository authentication. The absence of a specific MSC for this threat model is itself notable.

**Configurability:** Element provides settings to disable auto-download of media on mobile data but not to disable profile-picture fetching.

**Known incidents:** Matrix homeservers have historically been targets for CSAM distribution through the federation protocol. In 2023, Matrix.org administrators publicly discussed takedown workflows and homeserver-side filtering; the client-side caching behavior has not been substantively altered.

## 3.5 Telegram

**Vendor:** Telegram Messenger Inc.
**Model:** Phone-number identity, MTProto protocol, only "Secret Chats" use E2EE (and not by default), centralised servers.

**Default behavior:** Telegram auto-downloads media aggressively by default. Settings offer per-network-type auto-download for photos, videos, files, and music, but profile pictures are always fetched.

**Legal posture:** Telegram has historically taken a minimal-moderation posture that has brought the company into prolonged conflict with German authorities, French authorities (the Durov arrest in August 2024), and others. Telegram's centralised architecture means that server-side scanning is technically possible and is understood to be partially deployed; client-side caching remains aggressive.

**Relevance to this whitepaper:** Telegram is outside our primary design space (it is not decentralized or primarily E2EE) but is included for completeness because it is the most-used messenger in several authoritarian jurisdictions and the auto-download behavior there is especially consequential.

## 3.6 Session (Oxen Foundation)

**Repository:** github.com/session-foundation/session-android, session-ios, session-desktop
**Model:** No phone number, no central server. Service nodes operated by Oxen stakers. Onion routing via Lokinet.

**Default behavior:** Session auto-downloads media for contacts and group members with configurable limits. Profile pictures are fetched automatically.

**Relevance:** Session's service-node model is the closest existing system to what GoNode proposes, and our architecture borrows substantially from their design. Session operators stake the Oxen token (later migrated to SESH) and are paid for node uptime. Session does not presently implement erasure-coded distributed storage; files are stored on a single service node chosen by the uploader, with redundancy through periodic re-upload.

## 3.7 Briar

**Repository:** code.briarproject.org/briar/briar
**Model:** Peer-to-peer over Tor, Bluetooth, or Wi-Fi Direct. No servers at all.

**Default behavior:** Briar's P2P model means that media is fetched directly from the sender's device when online. There is no server-side cache. Auto-download behavior is present but gated by the presence of the peer; if the sender is offline, no fetch occurs.

**Relevance:** Briar is the architectural extreme of the anti-cache design. It illustrates the trade-off: no unsolicited caching, but also no asynchronous delivery and no group scalability beyond approximately 50 members.

## 3.8 Threema

**Vendor:** Threema GmbH (Switzerland)
**Model:** Random user ID (no phone number), commercial one-time purchase, Swiss jurisdiction.

**Default behavior:** Threema auto-downloads media according to user settings, with a default of downloading images on Wi-Fi. Profile pictures are auto-fetched.

**Relevance:** Threema is included as a commercial-privacy-focused point of comparison. Its Swiss jurisdiction offers certain legal advantages but does not alter the client-side caching issue.

## 3.9 Delta Chat

**Repository:** github.com/deltachat
**Model:** Email-over-IMAP/SMTP with Autocrypt for E2EE.

**Default behavior:** Delta Chat inherits email's pre-fetch-everything default. IMAP IDLE notification causes the client to fetch the full message including attachments. Profile pictures are less standardized (Delta uses the Autocrypt header and small avatar images embedded in messages).

**Relevance:** Delta Chat is particularly interesting because it uses existing email infrastructure; the auto-download behavior is dictated as much by email clients as by Delta Chat itself.

## 3.10 Wire

**Vendor:** Wire Swiss GmbH
**Model:** Centralized server, Proteus protocol (Signal-derived), commercial.

**Default behavior:** Auto-downloads images and voice notes by default; configurable. Profile pictures fetched automatically.

## 3.11 XMPP clients (Conversations, Gajim, Dino)

**Protocol:** XMPP (RFC 6120, 6121), OMEMO (XEP-0384) for E2EE.
**Clients:** Conversations (Android), Gajim (desktop), Dino (desktop), Monal (iOS).

**Default behavior:** Varies by client. Conversations has an explicit auto-download threshold setting (default 1 MB on Wi-Fi). Profile pictures use vCard and XEP-0084 user avatars, which are fetched on roster population.

## 3.12 Keybase

**Vendor:** Zoom Video Communications (since 2020 acquisition)
**Model:** Cryptographic identity linked to social accounts, centralised servers.

**Default behavior:** Auto-downloads media. Development has stagnated since the Zoom acquisition.

## 3.13 Discord

**Vendor:** Discord Inc.
**Model:** Not E2EE, included as a non-privacy comparison.

**Default behavior:** Aggressive auto-download. Discord is notable for having actively built child safety tooling including PhotoDNA integration, but this operates server-side, which is incompatible with E2EE models.

## 3.14 Comparative summary

| Messenger | Profile pic auto-fetch | Image auto-download default | Configurable | Published position on the problem |
|:----------|:----------------------|:---------------------------|:-------------|:----------------------------------|
| SimpleX | Yes | Yes (size threshold) | Partially | RFC 2024-12-30, acknowledged |
| Signal | Yes | Yes (Wi-Fi) | Partially (profile pic not config) | None public |
| WhatsApp | Yes | Yes (Wi-Fi photos) | Yes | None; multiple CVEs |
| Matrix/Element | Yes | Yes (thumbnails) | Partially | None public |
| Telegram | Yes | Yes (aggressive) | Yes | None |
| Session | Yes | Yes | Partially | None |
| Briar | N/A (P2P) | On peer online | Yes | Not applicable |
| Threema | Yes | Yes (Wi-Fi) | Yes | None public |
| Delta Chat | Yes (Autocrypt) | Via IMAP | Via email client | None |
| Wire | Yes | Yes | Yes | None |
| Conversations (XMPP) | Yes (vCard) | Yes (threshold) | Yes | None |
| Keybase | Yes | Yes | Limited | None |
| Discord | Yes | Yes | Limited | Server-side PhotoDNA |

The pattern is unambiguous. Every mainstream messenger auto-fetches profile pictures upon roster changes, and with the exception of Briar (which is P2P and has its own trade-offs) every mainstream messenger auto-downloads at least some category of media on at least some network conditions by default. Only SimpleX has published an official acknowledgement of the underlying problem, and that acknowledgement does not propose to eliminate auto-download for unconfirmed contacts.

GoNode DCD's contribution is to change the default.

---

*End of Part 1 of 5. Continues in Part 2 with Legal Framework, Design Goals, and Threat Model.*

---

# 4. Legal Framework

This section provides a jurisdiction-by-jurisdiction analysis of the legal context in which DCD must operate. We cite primary sources (official gazette references, regulation numbers, court decisions) for every provision. The framework is structured in concentric rings: (4.1) German criminal law establishing the core offence that motivates this work, (4.2) German telecommunications and media law defining provider obligations, (4.3) EU regulations, (4.4) United States, (4.5) United Kingdom, (4.6) authoritarian jurisdictions where the threat model is most acute. Section 15 later returns to compliance strategy; this section is descriptive rather than prescriptive.

## 4.1 Germany: Criminal law

### 4.1.1 §184b StGB - Verbreitung, Erwerb und Besitz kinderpornographischer Inhalte

The central provision is §184b of the Strafgesetzbuch (StGB), as amended by the "Gesetz zur Anpassung der Mindeststrafen des § 184b Absatz 1 Satz 1 und Absatz 3 des Strafgesetzbuches" of 24 June 2024 (BGBl. 2024 I Nr. 213), in force since 28 June 2024. The exact text is reproduced below with our working English translation. The German text is authoritative.

**§ 184b StGB (current version, in force since 28 June 2024):**

> "(1) Mit Freiheitsstrafe von sechs Monaten bis zu zehn Jahren wird bestraft, wer
>
> 1. einen kinderpornographischen Inhalt verbreitet oder der Öffentlichkeit zugänglich macht; kinderpornographisch ist ein pornographischer Inhalt (§ 11 Absatz 3), wenn er zum Gegenstand hat:
>    a) sexuelle Handlungen von, an oder vor einer Person unter vierzehn Jahren (Kind),
>    b) die Wiedergabe eines ganz oder teilweise unbekleideten Kindes in aufreizend geschlechtsbetonter Körperhaltung oder
>    c) die sexuell aufreizende Wiedergabe der unbekleideten Genitalien oder des unbekleideten Gesäßes eines Kindes,
> 2. es unternimmt, einer anderen Person einen kinderpornographischen Inhalt, der ein tatsächliches oder wirklichkeitsnahes Geschehen wiedergibt, zugänglich zu machen oder den Besitz daran zu verschaffen,
> 3. einen kinderpornographischen Inhalt, der ein tatsächliches Geschehen wiedergibt, herstellt oder
> 4. einen kinderpornographischen Inhalt herstellt, bezieht, liefert, vorrätig hält, anbietet, bewirbt oder es unternimmt, diesen ein- oder auszuführen, um ihn im Sinne der Nummer 1 oder der Nummer 2 zu verwenden oder einer anderen Person eine solche Verwendung zu ermöglichen, soweit die Tat nicht nach Nummer 3 mit Strafe bedroht ist.
>
> Gibt der kinderpornographische Inhalt in den Fällen von Absatz 1 Satz 1 Nummer 1 und 4 kein tatsächliches oder wirklichkeitsnahes Geschehen wieder, so ist auf Freiheitsstrafe von drei Monaten bis zu fünf Jahren zu erkennen.
>
> (2) Handelt der Täter in den Fällen des Absatzes 1 Satz 1 gewerbsmäßig oder als Mitglied einer Bande, die sich zur fortgesetzten Begehung solcher Taten verbunden hat, und gibt der Inhalt in den Fällen des Absatzes 1 Satz 1 Nummer 1, 2 und 4 ein tatsächliches oder wirklichkeitsnahes Geschehen wieder, so ist auf Freiheitsstrafe nicht unter zwei Jahren zu erkennen.
>
> **(3) Wer es unternimmt, einen kinderpornographischen Inhalt, der ein tatsächliches oder wirklichkeitsnahes Geschehen wiedergibt, abzurufen oder sich den Besitz an einem solchen Inhalt zu verschaffen oder wer einen solchen Inhalt besitzt, wird mit Freiheitsstrafe von drei Monaten bis zu fünf Jahren bestraft.**
>
> (4) Der Versuch ist in den Fällen des Absatzes 1 Satz 1 Nummer 1 und 3 sowie in den Fällen des Absatzes 1 Satz 2 in Verbindung mit Satz 1 Nummer 1 strafbar.
>
> (5) Absatz 1 Satz 1 Nummer 2 und Absatz 3 gelten nicht für Handlungen, die ausschließlich der rechtmäßigen Erfüllung von Folgendem dienen:
> 1. staatlichen Aufgaben,
> 2. Aufgaben, die sich aus Vereinbarungen mit einer zuständigen staatlichen Stelle ergeben, oder
> 3. dienstlichen oder beruflichen Pflichten.
>
> (6) Absatz 1 Satz 1 Nummer 1, 2 und 4 und Satz 2 gilt nicht für dienstliche Handlungen im Rahmen von strafrechtlichen Ermittlungsverfahren, wenn
> 1. die Handlung sich auf einen kinderpornographischen Inhalt bezieht, der kein tatsächliches Geschehen wiedergibt und auch nicht unter Verwendung einer Bildaufnahme eines Kindes oder Jugendlichen hergestellt worden ist, und
> 2. die Aufklärung des Sachverhalts auf andere Weise aussichtslos oder wesentlich erschwert wäre.
>
> (7) Gegenstände, auf die sich eine Straftat nach Absatz 1 Satz 1 Nummer 2 oder 3 oder Absatz 3 bezieht, werden eingezogen. § 74a ist anzuwenden."
>
> Source: dejure.org StGB §184b, current version effective 28 June 2024 per BGBl. 2024 I Nr. 213.

**Working English translation of the operative paragraphs for this whitepaper:**

Paragraph (1) criminalises the distribution, public dissemination, or provision of access to child pornographic content, with a penalty of six months to ten years imprisonment where the content depicts real or realistic events, and three months to five years where it depicts purely fictional events (e.g. computer-generated imagery not based on a real child).

**Paragraph (3) is the decisive provision for the threat model of this whitepaper.** It provides: "Whoever undertakes to retrieve or obtain possession of child pornographic content depicting a real or realistic event, or whoever possesses such content, shall be punished with imprisonment of three months to five years." Paragraph (3) establishes bare possession as a crime punishable by up to five years imprisonment, with a minimum of three months. The offence is a Verbrechen (felony) since its minimum penalty is one year or more, triggering various procedural consequences including pre-trial detention presumptions under §112a StPO.

Paragraph (2) establishes aggravated penalties (not less than two years) for commercial or gang-related commission.

Paragraph (5) and (6) establish narrowly-drawn exceptions for state functions, agreements with competent state bodies, professional duties, and investigative activities.

Paragraph (7) mandates forfeiture of objects involved in offences under paragraphs (1) No. 2 or 3, or paragraph (3).

### 4.1.2 The 2024 amendment

The June 2024 amendment (BGBl. 2024 I Nr. 213) reduced the minimum penalty under §184b (1) from one year to six months and under §184b (3) from one year to three months. This was a legislative response to cases like that of a mother who had forwarded CSAM she had received to warn other parents and was herself prosecuted; the Bundestag's Rechtsausschuss held a public hearing on 10 April 2024 at which expert witnesses unanimously supported the reduction [Bundestag 2024]. The reduction of minima does not affect the classification of possession as a Verbrechen in paragraph (3), which remains because its maximum penalty exceeds one year.

This legislative history is directly relevant to the threat model of this whitepaper: the mother in the referenced case had come into possession of CSAM without seeking it out, as a byproduct of a communication she received. The 2024 amendment reflects legislative acknowledgement that strict-liability possession can produce unjust outcomes in the specific context of unsolicited media delivery.

### 4.1.3 Implications of §184b (3) for messenger users

The combination of §184b (3) and the auto-download defaults analysed in Section 3 produces the following legal posture for every German messenger user:

- If a group member's profile picture is CSAM and your client auto-fetches it, §184b (3) is triggered as to possession. Whether the mens rea (Vorsatz, intent) element is satisfied depends on whether the user knew or should have known of the content. German case law requires only dolus eventualis (conditional intent, roughly "acceptance of the possibility"), which the prosecution can argue is satisfied by the user's knowledge that groups contain strangers.
- The forfeiture provision in §184b (7) permits seizure of the device on which the material was found, irrespective of conviction on the underlying offence.
- Under §112a StPO, pre-trial detention (Untersuchungshaft) is available on a Wiederholungsgefahr (risk of repetition) basis for offences including §184b.

**The practical effect is that a user whose device has been caused to possess CSAM through another's action faces device seizure, possible pre-trial detention, the procedural consequences of being accused of a Verbrechen, and a criminal record that persists even if acquitted (the Bundeszentralregister retains trial records for defined periods under §46 BZRG).** Acquittal does not undo the professional, social, and financial damage.

### 4.1.4 Adjacent provisions: §184c StGB (Jugendpornographie), §184e (Veranstaltung), §184l (Sexpuppen mit kindlichem Erscheinungsbild)

§184c StGB extends parallel offences to content depicting persons aged 14-17 (Jugendpornographie) with somewhat lower penalties. §184e StGB addresses organisation of and attendance at pornographic live-streaming. §184l StGB, in force since 1 July 2021, criminalises child-shaped sex dolls. All three provisions share the possession-as-crime structure and are susceptible to the same auto-download threat model.

### 4.1.5 §202a, §202b, §202c StGB - Data interception and related offences

§202a StGB criminalises unauthorised access to data that is specially protected against unauthorised access. §202b criminalises unauthorised interception of non-public data transmissions. §202c criminalises preparatory acts including the production, procurement, sale, or distribution of tools primarily designed for §202a or §202b offences. These provisions are relevant to DCD in that DCD's cryptographic architecture must satisfy the "besonders gesichert" (specially protected) threshold such that operators or third parties accessing individual shares face criminal liability under §202a.

### 4.1.6 §206 StGB - Verletzung des Post- oder Fernmeldegeheimnisses

§206 StGB protects the secrecy of communications provided by telecommunications services. The provision applies to persons who, as employees or former employees of a telecommunications service provider, disclose facts subject to telecommunications secrecy. For the GoNode operator model, this provision places operators who knowingly disclose even the existence or routing of a message under criminal penalty; it is a useful complement to the GDPR-based civil liability framework.

## 4.2 Germany: Telecommunications and media law

### 4.2.1 TKG - Telekommunikationsgesetz

The Telekommunikationsgesetz in its version of 23 June 2021 (BGBl. I S. 1858) as subsequently amended, regulates the operation of telecommunications services in Germany. Relevant provisions for DCD:

- **§3 No. 24 TKG** defines "Telekommunikationsdienst" (telecommunications service). The definition was substantially revised in 2021 to align with the EEKK (European Electronic Communications Code), and now includes interpersonal telecommunications services including those that are "nummernunabhängig" (number-independent). This is the category into which modern messengers fall.

- **§3 No. 41 TKG** defines "Verkehrsdaten" (traffic data).

- **§174 TKG** governs data retention obligations. Germany's data retention regime has been repeatedly invalidated by the Bundesverfassungsgericht and the Court of Justice of the European Union (CJEU); the current state as of April 2026 is that general blanket retention is impermissible but targeted retention orders remain available.

### 4.2.2 TKÜV - Telekommunikations-Überwachungsverordnung

The Telekommunikations-Überwachungsverordnung regulates the implementation of lawful interception. Key for DCD:

- **§3 TKÜV** establishes threshold criteria: providers with fewer than 10,000 participants are exempt from the requirement to provide technical interception capabilities. Above that threshold, providers must implement ETSI TS 102 232-series interfaces.

- For a small federated messenger operator, the threshold is a meaningful protection. For the GoNode operator model, where each individual operator remains below the threshold, the threshold is even more meaningful, and the distributed nature of the system means that interception cannot be effected at any single operator.

### 4.2.3 TMG / DDG - Telemediengesetz and its successor

The Telemediengesetz (TMG) was partially superseded in 2024 by the Digitale-Dienste-Gesetz (DDG), which implements the EU Digital Services Act in Germany. Key provisions:

- **§8 TMG (now §7 DDG)** establishes the "Durchleitung" liability privilege for transmission providers, parallel to DSA Article 4.
- **§9 TMG (now §8 DDG)** establishes the caching privilege parallel to DSA Article 5.
- **§10 TMG (now §9 DDG)** establishes the hosting privilege parallel to DSA Article 6.

The DDG came into force on 14 May 2024 (BGBl. 2024 I Nr. 149).

### 4.2.4 NetzDG - Netzwerkdurchsetzungsgesetz

The Netzwerkdurchsetzungsgesetz was enacted in 2017 to require social networks with at least two million German users to implement takedown procedures. The NetzDG has been largely superseded by the DSA for most purposes, but certain reporting obligations persist. GoNode is unlikely to reach the NetzDG threshold; SimpleGoX as an end-user application might, at sufficient scale.

## 4.3 European Union

### 4.3.1 Regulation (EU) 2022/2065 - Digital Services Act

The Digital Services Act entered into force on 16 November 2022 and applies, for most provisions, from 17 February 2024. Its liability framework (Chapter II, Articles 4-8) replaces the e-Commerce Directive (2000/31/EC) for the intermediary services within its scope.

**Article 4 DSA - Mere conduit:**

> "1. Where an information society service is provided that consists of the transmission in a communication network of information provided by a recipient of the service, or the provision of access to a communication network, the service provider shall not be liable for the information transmitted or accessed, on condition that the provider:
> (a) does not initiate the transmission;
> (b) does not select the receiver of the transmission; and
> (c) does not select or modify the information contained in the transmission.
>
> 2. The acts of transmission and of provision of access referred to in paragraph 1 include the automatic, intermediate and transient storage of the information transmitted in so far as this takes place for the sole purpose of carrying out the transmission in the communication network, and provided that the information is not stored for any period longer than is reasonably necessary for the transmission.
>
> 3. This Article shall not affect the possibility for a judicial or administrative authority, in accordance with Member States' legal system, to require the service provider to terminate or prevent an infringement."
>
> Source: Regulation (EU) 2022/2065, Article 4.

**Article 5 DSA - Caching:** Applies to providers that provide "automatic, intermediate and temporary storage of [information transmitted], performed for the sole purpose of making more efficient or more secure the information's onward transmission to other recipients." Liability exemption requires conditions including acting expeditiously to remove or disable access to information upon obtaining actual knowledge of its removal from the source or a court order.

**Article 6 DSA - Hosting:** Applies to providers that store information provided by a recipient. Liability exemption requires that the provider does not have actual knowledge of illegal activity or content, and upon obtaining such knowledge acts expeditiously to remove or disable access.

**Article 8 DSA - No general monitoring obligation:** Explicitly prohibits Member States from imposing general monitoring obligations on intermediary providers.

**Article 16 DSA - Notice and action mechanisms:** Requires hosting providers to implement mechanisms to allow any individual or entity to notify the provider of specific items of information that the notifying party considers to be illegal content. The notice must contain specified elements. Providers must act on notices without undue delay.

**Article 18 DSA - Notification of suspicions of criminal offences:** Where a hosting provider becomes aware of any information giving rise to a suspicion that a criminal offence involving a threat to the life or safety of persons has taken place, the provider must promptly inform the relevant authorities.

### 4.3.2 Regulation (EU) 2016/679 - GDPR

The General Data Protection Regulation is the foundational European data-protection law. Provisions particularly relevant to DCD:

- **Article 5 GDPR** establishes principles of lawfulness, fairness, transparency, purpose limitation, data minimisation, accuracy, storage limitation, integrity and confidentiality, and accountability.
- **Article 6 GDPR** lists lawful bases for processing.
- **Article 9 GDPR** establishes heightened protection for "special categories of personal data" including biometric data and data concerning sexual orientation or sex life. This is directly relevant: images that fall within §184b are a fortiori special-category data under Article 9.
- **Article 25 GDPR** establishes data protection by design and by default. Relevant to DCD because auto-download-by-default is arguably non-compliant with Article 25 by treating maximum retention as the default.
- **Article 32 GDPR** requires "appropriate technical and organisational measures to ensure a level of security appropriate to the risk," explicitly including "(a) the pseudonymisation and encryption of personal data."

### 4.3.3 Regulation (EU) 2021/1232 - Temporary derogation from ePrivacy Directive

Regulation (EU) 2021/1232 established a temporary, voluntary derogation from Articles 5(1) and 6(1) of the ePrivacy Directive (2002/58/EC) to permit certain providers to voluntarily scan interpersonal communications for CSAM. The regulation expired on 3 April 2026 without renewal after the European Parliament on 13 March 2026 rejected an extension [State of Surveillance 2026]. As of the date of this whitepaper (April 2026), voluntary scanning of interpersonal communications by providers is no longer legally privileged in the European Union; providers that continue to scan may face GDPR and ePrivacy liability.

### 4.3.4 COM/2022/209 - Proposed CSAM Regulation (Chatkontrolle)

The European Commission's proposal of 11 May 2022 for a Regulation "laying down rules to prevent and combat child sexual abuse" (commonly "Chat Control" or "Chatkontrolle") has been the subject of sustained political conflict since its introduction. The proposal would have required providers of interpersonal communications services, including end-to-end encrypted services, to implement "detection orders" that could require client-side scanning.

Chronology of relevant events since the last drafting of this section:

- **July 2025:** Danish EU Council Presidency tables a revised proposal retaining client-side scanning for E2EE services.
- **14 October 2025:** Scheduled Council vote postponed due to opposition from Germany, Austria, the Netherlands, Finland, and Poland.
- **31 October 2025:** Denmark backs away from mandatory scanning after what multiple sources describe as a "firm no" from Germany [Atomic Mail 2025].
- **13 March 2026:** European Parliament rejects extension of Chat Control 1.0 voluntary scanning derogation [State of Surveillance 2026].
- **3 April 2026:** Voluntary scanning derogation (Regulation (EU) 2021/1232) expires.

As of the date of this whitepaper, the Chatkontrolle mandatory-scanning proposal has not been enacted, and the voluntary-scanning derogation has expired. The position is fluid; this whitepaper's design assumes continued absence of a mandatory client-side scanning requirement in the European Union, but contains provisions (see Section 15) for adaptation should that position change.

### 4.3.5 Regulation (EU) 2023/1114 - MiCA

The Markets in Crypto-Assets Regulation entered into force on 29 June 2023; provisions on asset-referenced tokens and e-money tokens applied from 30 June 2024, and the general regime applied from 30 December 2024. MiCA defines three categories of crypto-assets (asset-referenced tokens, e-money tokens, and other crypto-assets) and imposes authorisation requirements on issuers and service providers.

For DCD, MiCA is the primary reason we adopt a non-token economic model. Any native token representing a share of the network's economic value would fall within MiCA's scope and require authorisation as an issuer, with consequent capital, governance, and transparency requirements that would substantially burden a federated service-node network. EURC (issued by Circle Internet Financial under an EMI licence from the French ACPR) is MiCA-compliant as an e-money token; operator payments in EURC rather than in a native token are MiCA-compliant operating transfers rather than issuance of a crypto-asset. This design choice is analysed further in Section 14.

## 4.4 United States

### 4.4.1 18 U.S.C. §2252 and §2252A

Federal criminal law prohibits possession of CSAM under 18 U.S.C. §2252 and §2252A. §2252A(a)(5)(B) establishes that whoever "knowingly possesses, or knowingly accesses with intent to view, any book, magazine, periodical, film, videotape, computer disk, or any other material that contains an image of child pornography" shall be punished with up to ten years imprisonment for a first offence.

The mens rea element ("knowingly") is more forgiving than the German dolus eventualis standard, but U.S. courts have construed "knowingly" broadly to include circumstances where the defendant knew of the presence of images even if they did not intend to possess them.

The Adam Walsh Child Protection and Safety Act of 2006 (Public Law 109-248) imposes handling restrictions on CSAM evidence that affect forensic workflows; relevant for defence counsel but not for the core design of DCD.

### 4.4.2 18 U.S.C. §2258A - NCMEC reporting obligations

18 U.S.C. §2258A imposes reporting obligations on electronic communication service providers and remote computing service providers. When such a provider obtains actual knowledge of any facts or circumstances giving reason to believe that an apparent violation of §2251-§2252A or related provisions has occurred, the provider must report the facts to the CyberTipline operated by the National Center for Missing and Exploited Children (NCMEC) "as soon as reasonably possible."

§2258A(f) provides civil and criminal liability for failure to report. §2258B provides a limited grant of immunity for voluntary CSAM scanning.

For the DCD architecture, §2258A reporting obligations apply only to entities that are electronic communication service providers or remote computing service providers. Individual GoNode operators holding single encrypted shares arguably do not qualify in the technical sense, but the question is jurisdictionally complex and we address it in Section 15.

### 4.4.3 47 U.S.C. §230 - Communications Decency Act Section 230

47 U.S.C. §230(c)(1) provides: "No provider or user of an interactive computer service shall be treated as the publisher or speaker of any information provided by another information content provider." §230(c)(2) provides Good Samaritan protection for voluntary content moderation.

§230 has been repeatedly challenged and narrowed through legislative amendment (FOSTA-SESTA in 2018) and judicial interpretation, but remains the foundation of U.S. intermediary liability law. For GoNode operators, §230 provides substantial protection against U.S. civil liability for transmitted content.

### 4.4.4 EARN IT Act and STOP CSAM Act

The EARN IT Act (Eliminating Abusive and Rampant Neglect of Interactive Technologies Act) was reintroduced in the U.S. Senate multiple times between 2020 and 2025. It would condition §230 immunity on compliance with "best practices" developed by a federal commission, with the implicit expectation that those best practices would include some form of content scanning. As of April 2026, the EARN IT Act has not been enacted. The STOP CSAM Act (Strengthening Transparency and Obligations to Protect Children Suffering from Abuse and Mistreatment Act) similarly has been introduced and reintroduced without enactment.

### 4.4.5 State law

California's AB 1394 (2023) requires social media platforms to implement CSAM removal procedures. West Virginia filed suit against Apple in 2025 over iCloud CSAM policies [State of Surveillance 2026]. The state-law landscape in the U.S. is complex and evolving.

## 4.5 United Kingdom

### 4.5.1 Online Safety Act 2023

The Online Safety Act 2023 (c. 50) received Royal Assent on 26 October 2023 and is being implemented by Ofcom in phases through 2025-2026. The Act imposes duties of care on "user-to-user" services and "search services."

**Section 122 of the Online Safety Act** empowers Ofcom to issue "technology notices" requiring providers to use "accredited technology" to identify CSAM and terrorism-related content. Section 122 notices have been the subject of sustained controversy because they could, as drafted, require client-side scanning in E2EE services. In 2023, the UK government provided a public assurance that Section 122 would not be used until the technology is "technically feasible" without breaking encryption, which Ofcom and the ICO (Information Commissioner's Office) have interpreted to mean indefinitely. As of April 2026, no Section 122 notice has been issued against an E2EE provider.

### 4.5.2 Investigatory Powers Act 2016

The Investigatory Powers Act 2016 (c. 25) establishes the UK's surveillance framework including Technical Capability Notices (TCNs) under Section 253. TCNs can require providers to maintain capabilities to assist in lawful interception, and have been cited in speculation about backdoor requirements for E2EE services. Apple has publicly engaged with UK authorities on this topic and in February 2025 announced removal of Advanced Data Protection for UK users in response to a TCN-related demand.

## 4.6 Authoritarian jurisdictions

We catalogue briefly for context:

### 4.6.1 Russia

Federal Law No. 374-FZ of 7 July 2016 (the "Yarovaya package") requires telecommunications providers to store all traffic data for three years and content data for six months, and to provide decryption keys to the FSB. In practice, major messengers do not comply and are subject to enforcement actions including blocking. Federal Law No. 187-FZ extends registry of "information disseminators" (ORI) status to services that facilitate communications; LinkedIn, Twitter/X, Telegram, and others have at various points been blocked under this regime.

For DCD, the relevance is the documented Russian pattern of physical evidence planting (Section 2) combined with aggressive surveillance demands; Russian journalists are one of the primary user groups for whom DCD's threat model is most acute.

### 4.6.2 Belarus

Presidential Decree No. 8 of 21 December 2017 regulates cross-border data flows; the Law on Mass Media establishes broad state powers over communications. Following the 2020 protests and resulting crackdown, possession of "extremist" material has become a routine basis for prosecution; Telegram channels subscribed to by defendants are routinely cited as evidence [documented in RSF reports 2020-2025].

### 4.6.3 Turkey

Law No. 5651 on the Regulation of Publications on the Internet requires content providers to remove content upon administrative order. Turkey has periodically blocked Wikipedia, Twitter/X, YouTube, and other platforms. Press freedom cases frequently involve content-based prosecutions.

### 4.6.4 Iran

The Computer Crimes Law of 2009 criminalises broad categories of online content including "insulting religious sanctities" and "propaganda against the system." Internet surveillance is pervasive. Cases of Iranian journalists being prosecuted on content-based charges, sometimes involving claims of planted or auto-cached material, are documented by Article 19 and Human Rights Watch.

### 4.6.5 China

The Cybersecurity Law (2017), Data Security Law (2021), and Personal Information Protection Law (2021) form the backbone of China's regime. The "real-name registration" requirement in Article 24 of the Cybersecurity Law and the broad content prohibitions in the Internet Information Service Management Measures render privacy-preserving messengers largely unviable in China; WeChat dominates the market under extensive monitoring.

## 4.7 Summary of the legal framework

| Jurisdiction | Key possession offence | Minimum penalty | Strict / knowledge |
|:-------------|:----------------------|:---------------|:-------------------|
| Germany | §184b (3) StGB | 3 months | Vorsatz (dolus eventualis) |
| EU common baseline | Directive 2011/93/EU Art. 5 | Member State transposition | Member State transposition |
| USA federal | 18 U.S.C. §2252A(a)(5)(B) | None specified; up to 10 years | "Knowingly" |
| UK | Protection of Children Act 1978 s. 1 / CJA 1988 s. 160 | None specified; up to 10 years | Knowledge |

| Jurisdiction | Intermediary liability regime | Mandatory scanning status (April 2026) |
|:-------------|:------------------------------|:---------------------------------------|
| Germany | DDG / DSA | No (Chatkontrolle not enacted) |
| EU | DSA Art. 4-6, 8 | No (voluntary scanning derogation expired 3 April 2026) |
| USA | 47 U.S.C. §230 | Voluntary; NCMEC reporting mandatory under §2258A |
| UK | Online Safety Act | Section 122 notices possible but not deployed against E2EE |

---

# 5. Design Goals and Non-Goals

This section states what SimpleGoX with the integrated GoNode DCD architecture aims to achieve and, with equal clarity, what it does not aim to achieve. We state this early because the single most common failure mode for privacy-preserving systems is design-by-accretion, where incompatible goals are added over time and the resulting system satisfies none of them.

## 5.1 Primary design goals

**G1: No illegal content on user devices by default.** The baseline user experience does not cause any media from unconfirmed contacts to be written to persistent storage. This goal is satisfied by the combination of the no-auto-download policy (Section 11) and the RAM-only rendering of explicitly-requested content.

**G2: No individual operator can reconstruct user content.** Any single GoNode operator holds at most one of five Reed-Solomon shares of any file, and that share is independently encrypted with a subkey that is not held by the operator. The operator's full cooperation with a lawful warrant yields ciphertext from which no plaintext can be derived.

**G3: No individual operator can identify content by reference to known-bad hashes.** Because operators hold share-level ciphertext, server-side hash-matching is impossible. Hash-matching occurs exclusively on the user's device after share reassembly and before rendering.

**G4: Moderator effectiveness without moderator jeopardy.** Group administrators who opt into moderation can identify and act upon abusive content without themselves creating persistent artifacts of that content on their personal devices. This is achieved either through TEE-based classification (Section 12) or, where TEE is unavailable, through ephemeral RAM-only display with aggressive purging.

**G5: Legal defensibility in the Federal Republic of Germany.** The architecture is designed to satisfy §184b StGB, §202a StGB, §206 StGB, DSA Articles 4, 5, 6, 8, 16, 18, GDPR Articles 5, 6, 9, 25, 32, and the Telekommunikationsgesetz. We state the compliance analysis in Section 15 and invite adversarial legal review.

**G6: No crypto-asset under MiCA.** The operator economic model uses stake-based participation denominated in EUR-pegged e-money tokens (EURC, USDC) and does not issue any native token with floating value. This keeps GoNode outside the scope of MiCA's issuer provisions.

**G7: Minimum viable product within 12 months.** The architecture is designed so that a functional subset (no-auto-download defaults, (3,5) Reed-Solomon storage, client-side PDQ hash check) can be deployed to the existing 10 SMP + 1 XFTP operator infrastructure within a 12-month engineering effort. The TEE moderation layer and hardware-attested operator registration are Phase 2 deliverables.

## 5.2 Secondary design goals

**S1: Interoperability with existing SimpleX-derived protocols.** GoNode DCD is specified to coexist with the SMP and XFTP protocols operated by the existing SimpleGo Ecosystem infrastructure. Migration is incremental, not flag-day.

**S2: Backward-compatible user experience for confirmed contacts.** Users who have explicitly confirmed each other (mutual contact acceptance, verified key fingerprint) receive an approximately equivalent user experience to existing messengers, with media auto-fetching for confirmed contacts optional but permitted.

**S3: Operator decentralization across jurisdictions.** The erasure-coded storage layer selects operators across five distinct legal jurisdictions where feasible, reducing the risk that any single state actor can compel reconstruction of user content by coercing a majority of share-holders.

**S4: Tor-compatible transport.** All protocol operations must function over Tor v3 hidden services (the current SMP and XFTP infrastructure is deployed this way). Latency budgets accommodate Tor's typical 1-5 second round-trip times.

**S5: Post-quantum forward security.** Key encapsulation uses ML-KEM-768 (NIST FIPS 203, formally CRYSTALS-Kyber) in addition to X25519; symmetric encryption uses XChaCha20-Poly1305 (RFC 8439 XChaCha extension). The construction is hybrid such that compromise of either the classical or the post-quantum primitive does not break confidentiality.

## 5.3 Explicit non-goals

**N1: We do not aim to prevent determined offenders from distributing CSAM among themselves.** An offender who knowingly joins an abuse network, and whose counterparties knowingly accept their messages, can circumvent any system we build simply by modifying the client. SimpleX's content moderation RFC correctly notes that open-source clients can be modified; we accept this limit. Our goal is to prevent the weaponisation of the messenger against unwilling users, not to perform pervasive content policing.

**N2: We do not implement client-side scanning of outgoing messages.** The architecture scans only content that the user has explicitly requested for rendering, and only against a local hash list maintained for this purpose. This is materially different from the EU Chatkontrolle proposal's client-side scanning of all outgoing content.

**N3: We do not identify users to operators.** The GoNode operator model follows SimpleX's no-user-identifier architecture. Operators see queue addresses and ephemeral session keys, not persistent user identities.

**N4: We do not collect telemetry for abuse detection.** There is no server-side logging of user behavior, access patterns, or reassembly events. Abuse detection occurs on the reporting user's device at their explicit request.

**N5: We do not provide plausible deniability against state-level forensic analysis.** While RAM-only rendering and disk-cache avoidance substantially raise the bar for forensic recovery, we do not claim that a device seized with warm RAM and subjected to a cold-boot attack by a competent state actor within seconds of seizure cannot recover content. Users in extreme threat models should understand this residual risk and are advised to additionally use full-disk encryption and secure-boot devices.

**N6: We do not provide protection against Rubber-Hose cryptanalysis.** If the user is compelled under duress to operate their device, the architecture does not prevent the compelled retrieval of content. Some jurisdictions (UK under RIPA 2000 s. 49; France under L. 434-15-2 of the Code pénal) criminalise refusal to provide decryption keys. We cannot and do not claim to defeat such legal compulsion.

**N7: We do not solve the problem for messengers we do not control.** DCD is an architecture for the SimpleGo Ecosystem (SimpleGoX as the client, GoNode as the service-node infrastructure). We describe the underlying patterns so that other projects can adopt them, but we do not claim to fix Signal, WhatsApp, Telegram, or Matrix.

## 5.4 The solution in one page

For readers skimming this document, the solution is as follows, and SimpleGoX with integrated GoNode DCD is the SimpleGo Ecosystem's production implementation:

1. **On join.** When Alice joins Bob's group, Bob's SimpleGoX client does not fetch Alice's profile picture. Bob sees a deterministic silhouette derived from a hash of Alice's public key. If Bob later taps Alice's silhouette, the profile picture is fetched, assembled in RAM, PDQ-hashed against the local known-bad list, and displayed if clean. No disk write occurs unless Bob promotes Alice to confirmed-contact status.

2. **On group media.** When anyone posts media in a group Bob is in, Bob's client does not auto-fetch. A placeholder shows that media is available. If Bob taps, the same RAM-only assemble-hash-render workflow applies. Confirmed-contact media is configurable to auto-fetch.

3. **On upload.** When Bob posts a photo to a group, SimpleGoX encrypts it with a random key, splits it into five Reed-Solomon shares, re-encrypts each share with an HKDF-derived subkey, and distributes the shares to five GoNode operators selected via ECVRF from the current operator set. The master key is split via Shamir (3,5) and encrypted to each recipient's public key.

4. **On moderation.** A group admin who opts into moderation runs a classifier in the device's TEE. Flagged content triggers a structured report workflow. The admin's host OS never observes the flagged content in plaintext.

5. **On known-bad match.** If the local PDQ hash matches a known-bad entry, rendering is aborted, the content is not displayed, and a report is generated that identifies only the share addresses and a cryptographic proof of the hash match, not the plaintext.

6. **On economy.** Operators post a EUR-denominated stake to a smart contract on Arbitrum One. Payment for storage and routing is in EURC. Stake is slashable for documented misbehavior (serving garbage shares, refusing audit challenges). No token, no valuation, no MiCA.

This is the solution. The rest of this whitepaper explains how each of these steps is constructed, why the construction is cryptographically sound, why it is legally defensible, and what the residual risks are.

---

# 6. Formal Threat Model

We apply the STRIDE methodology [Howard and LeBlanc, "Writing Secure Code," 2nd ed., Microsoft Press, 2002] to the DCD architecture. STRIDE categorises threats into six classes: Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, and Elevation of privilege. For each class, we identify the assets, the adversaries, and the mitigations.

## 6.1 Assets

- **A1:** User identities (public keys, device keys).
- **A2:** Content plaintexts (photos, videos, documents, voice messages).
- **A3:** Group membership information (who is in which group).
- **A4:** Operator stake and reputation.
- **A5:** Moderator decisions (which content was classified how).
- **A6:** Known-bad hash list integrity.

## 6.2 Adversaries

- **AD1 (Passive network):** An observer of encrypted traffic on any network segment. Capabilities: read all packet headers and payloads. Cannot modify, delay, or inject.
- **AD2 (Active network):** AD1 plus ability to modify, delay, drop, and inject. Can perform MITM on connections not protected by forward-secret key agreement with pre-authenticated endpoints.
- **AD3 (Compromised operator):** An adversary controlling up to k-1 of n operators (for our (3,5) parameters, up to 2 operators). Capabilities: full access to the compromised operators' storage, logs, and cryptographic material.
- **AD4 (Compromised client):** An adversary with code execution on the user's client device. Capabilities: arbitrary access to application memory, storage, and cryptographic material on that device.
- **AD5 (Nation-state lawful):** An adversary acting with lawful authority in a jurisdiction. Capabilities: can compel cooperation from operators in that jurisdiction. Can execute device seizures with judicial authorisation.
- **AD6 (Nation-state pretextual):** A state actor acting under colour of law with the goal of prosecuting or harassing specific targets. Capabilities of AD5 plus willingness to fabricate or plant evidence.
- **AD7 (Operator collusion):** k or more operators colluding. For our (3,5) parameters, 3 or more of 5 operators. Capabilities: full reconstruction of files for which they collectively hold a sufficient share set.

## 6.3 Spoofing threats and mitigations

**T-S1: Operator identity spoofing.** An attacker presents themselves as a legitimate operator to a client. *Mitigation:* Operator identity is established by an Ed25519 public key registered in the GoNode operator registry smart contract on Arbitrum One. Clients verify operator signatures against the on-chain registry.

**T-S2: User identity spoofing in group membership.** An attacker creates a new identity that looks like an existing user. *Mitigation:* User identity is cryptographic. Each user is identified by a Ed25519 public key. Users verify each other out-of-band before promoting to confirmed-contact status. The DCD architecture explicitly does not rely on display names or profile pictures for identity.

**T-S3: Operator sybil attack.** An attacker creates multiple operators to bias share placement. *Mitigation:* Operator registration requires a minimum EUR-denominated stake posted to the smart contract. Share placement uses ECVRF [RFC 9381] deterministically per-file, preventing attacker selection bias.

## 6.4 Tampering threats and mitigations

**T-T1: Share tampering.** AD3 modifies one or more shares they hold. *Mitigation:* Each share carries an XChaCha20-Poly1305 AEAD tag that verifies during reassembly. Tampered shares are detected; Reed-Solomon (3,5) tolerates up to 2 lost or tampered shares without data loss.

**T-T2: Master key tampering.** AD3 modifies the Shamir share of the master key. *Mitigation:* Each Shamir share is encrypted to the recipient's public key using the recipient's X25519 and ML-KEM-768 hybrid KEM. Tampering breaks the KEM decryption and is detected.

**T-T3: Hash list tampering.** AD4 modifies the local known-bad hash list to miss content. *Mitigation:* Hash list is distributed signed by a committee of four maintainers (NCMEC liaison, IWF liaison, DCD Foundation, and a fourth rotating member). Client verifies signatures before use. Silent modification is not possible without compromising at least three of four committee keys.

## 6.5 Repudiation threats and mitigations

**T-R1: Operator repudiation of share storage.** An operator claims to have never received a share they did receive. *Mitigation:* Uploader retains a signed receipt from each operator at upload time. Audit challenge protocol (specified in Section 9) allows periodic proof-of-storage.

**T-R2: Moderator repudiation of decisions.** A moderator claims a decision was not theirs. *Mitigation:* Moderator decisions are signed with the moderator's operator key and logged to the group state tree.

## 6.6 Information disclosure threats and mitigations

**T-I1: Disclosure to a single operator.** AD3 with one operator compromised seeks to reconstruct user content. *Mitigation:* (3,5) Reed-Solomon with per-share AEAD encryption: no single share carries recoverable plaintext. Below the (3,5) threshold, Shamir provides information-theoretic security for the master key.

**T-I2: Disclosure to colluding operators below threshold.** AD3 with two operators compromised. *Mitigation:* Same as T-I1. Two shares yield zero information.

**T-I3: Disclosure to colluding operators at or above threshold.** AD7 with three or more operators. *Mitigation:* This is a genuine failure mode for confidentiality. Mitigations at the structural level: ECVRF-driven operator selection from a globally-distributed pool makes targeted collusion expensive; operator registry cryptographically commits operators to jurisdictional diversity; slashing penalties create economic disincentive. This threat is addressed in Section 18 as an acknowledged residual risk.

**T-I4: Disclosure via client device compromise.** AD4 reads assembled plaintext from RAM. *Mitigation:* `mlock(2)` prevents paging to disk; `explicit_bzero(3)` immediately after render reduces the window; FLAG_SECURE on Android and equivalent on other platforms prevents screenshot-class attacks. AD4 with full code execution is acknowledged as a failure mode; we address it by ensuring the client surface area is minimal and by supporting TEE-based rendering as an optional layer (Section 12).

**T-I5: Disclosure via known-bad hash comparison.** A client observer sees the hash comparison occur. *Mitigation:* Hash comparison is performed in constant time over the full list. Timing side-channels do not leak which entry matched; the matched entry is logged only locally with user consent.

**T-I6: Disclosure via pretextual legal process.** AD6 obtains a warrant for a targeted user's device. *Mitigation:* If the device is seized while powered-off and the user has not recently decrypted content, no plaintext is recoverable. This is a principal design goal and a principal value proposition.

## 6.7 Denial of service threats and mitigations

**T-D1: Share withholding.** AD3 refuses to serve held shares. *Mitigation:* (3,5) tolerates 2 missing shares; repair protocol regenerates lost shares from surviving ones. Slashing penalties for non-responsive operators create economic disincentive.

**T-D2: Upload flooding.** An attacker attempts to exhaust operator storage. *Mitigation:* Upload requires a signed credit from the operator; credits are obtained against EURC payment. Free-tier users have per-day credit limits.

**T-D3: Known-bad hash list denial of service.** An attacker floods the hash list with benign-file hashes. *Mitigation:* Hash list contents are signed by the maintainer committee; unauthorised entries are not accepted. Committee charter limits legitimate additions to content matching NCMEC, IWF, BKA, or equivalent national clearinghouse criteria.

## 6.8 Elevation of privilege threats and mitigations

**T-E1: Moderator impersonation.** An attacker issues moderator decisions on behalf of a legitimate moderator. *Mitigation:* Moderator role is cryptographically conferred by the group owner; moderator decisions are signed with the moderator's Ed25519 key.

**T-E2: TEE escape.** AD4 escapes the TEE sandbox. *Mitigation:* Fundamental TEE security property. DCD relies on the TEE implementation (ARM TrustZone, Apple Secure Enclave, Intel SGX) and does not attempt to provide TEE-level security in userspace code. TEE compromise is treated as a failure mode equivalent to client device compromise (T-I4).

**T-E3: Smart contract vulnerability.** AD4 or AD7 exploits a flaw in the Arbitrum One smart contracts. *Mitigation:* Smart contracts undergo at least two independent audits before mainnet deployment. Economic logic contains no upgrade mechanism after Phase 4 (month 36). Multi-sig timelock during Phase 0-3.

## 6.9 Threat model summary

| Threat | STRIDE category | Adversary | Mitigation status |
|:-------|:----------------|:----------|:------------------|
| Operator spoofing | S | AD2, AD3 | Full: registry + signatures |
| User identity spoofing | S | AD2 | Full: crypto identity + OOB verification |
| Operator sybil | S | AD3 | Full: stake + ECVRF |
| Share tampering | T | AD3 | Full: AEAD + (3,5) tolerance |
| Master key tampering | T | AD3 | Full: KEM authentication |
| Hash list tampering | T | AD4 | Partial: committee signatures |
| Operator repudiation | R | AD3 | Full: receipts + audits |
| Moderator repudiation | R | AD6 | Full: signed decisions |
| Single-operator disclosure | I | AD3 | Full: (3,5) Shamir + AEAD |
| Sub-threshold collusion | I | AD3, AD7 | Full: (3,5) Shamir |
| Threshold collusion | I | AD7 | **Residual risk** |
| Client compromise | I | AD4 | Partial: mlock + TEE optional |
| Pretextual seizure | I | AD6 | Full: no disk plaintext by default |
| Share withholding | D | AD3 | Full: (3,5) tolerance + slashing |
| Upload flooding | D | External | Full: credit system |
| Hash list DoS | D | External | Full: committee gatekeeping |
| Moderator impersonation | E | AD6 | Full: signed decisions |
| TEE escape | E | AD4 | Inherited from TEE |
| Smart contract exploit | E | AD4, AD7 | Partial: audits + timelock |

The single unmitigated residual risk is threshold collusion among operators, which we accept as a property inherent to any k-of-n threshold system and address through operator-pool economics rather than cryptographic bolting-on.

---

*End of Part 2 of 5. Continues in Part 3 with cryptographic foundations, system architecture, and protocol specification.*

---

# 7. Cryptographic Foundations

This section specifies the cryptographic primitives used throughout DCD, with bibliographic references to the standards and peer-reviewed constructions from which they are drawn. All parameter choices are conservative and align with NIST, IRTF, and IETF recommendations as of April 2026.

## 7.1 Notation

We use the following notation throughout:

- `||` for byte-string concatenation.
- `len(x)` for the length in bytes of x.
- `x[i..j]` for the slice of x from byte i (inclusive) to byte j (exclusive), zero-indexed.
- `H(x)` for a cryptographic hash of x (defaulting to SHA-256 unless otherwise specified).
- `HMAC(k, x)` for HMAC with key k and message x.
- `HKDF-Extract(salt, ikm)` and `HKDF-Expand(prk, info, L)` per RFC 5869.
- `Enc_k(n, aad, pt) -> ct` for XChaCha20-Poly1305 AEAD encryption with key k, nonce n, associated data aad, plaintext pt, yielding ciphertext ct including 16-byte authentication tag.
- `Dec_k(n, aad, ct) -> pt | ERROR` for the corresponding decryption.
- `Sign_sk(m) -> sig` for Ed25519 signature over m with private key sk.
- `Verify_pk(m, sig) -> {OK, FAIL}` for verification.
- `KEM.Encap(pk) -> (ss, ct)` for KEM encapsulation yielding shared secret ss and ciphertext ct.
- `KEM.Decap(sk, ct) -> ss | ERROR` for KEM decapsulation.

## 7.2 Symmetric primitives

**XChaCha20-Poly1305 AEAD.** We use the 192-bit nonce variant of ChaCha20-Poly1305 as specified in the IRTF CFRG draft [draft-irtf-cfrg-xchacha]. The extended nonce length permits random nonce generation without birthday-bound concerns and is the implementation reference in libsodium. Key length is 256 bits; tag length is 128 bits; maximum plaintext per nonce is 256 GiB, which is beyond any file size we encounter.

XChaCha20-Poly1305 is chosen over AES-GCM because (a) it has no catastrophic nonce-reuse failure mode in our nonce-by-random construction, (b) its constant-time software implementation is straightforward and avoids cache-timing attacks that have affected AES implementations in constrained environments, and (c) it is the primitive already in use in the existing SimpleGo hardware and SimpleGoX Rust codebase via libsodium.

**SHA-256 and SHA-3.** SHA-256 (FIPS 180-4) is used for non-security-critical integrity checks, HMAC, and as the hash underlying HKDF. SHA-3 (FIPS 202) variants are not required in the baseline but are permitted for future interoperability.

**BLAKE3.** BLAKE3 [O'Connor, Aumasson, Neves, Wilcox-O'Hearn 2020] is used as the hash function for the Reed-Solomon share integrity tree because its tree-hashing mode permits parallel verification of subsets of shares without recomputing the full hash. BLAKE3 is preferred over SHA-256 for this specific use case due to its performance advantage on modern CPUs (5-10x faster in single-threaded mode, substantially more in parallel).

**HKDF.** Key derivation uses HKDF-SHA-256 per RFC 5869. The construction is `HKDF-Extract(salt, ikm) = HMAC-SHA-256(salt, ikm)` followed by `HKDF-Expand(prk, info, L)` to produce L bytes of output. For per-share subkey derivation we use `info = "GoNode-DCD-Share-Subkey-v1" || share_index || file_hash`.

## 7.3 Asymmetric primitives

**Ed25519 for signatures.** Ed25519 per RFC 8032 is the default signature scheme. Key size is 32 bytes (public) and 32 bytes (secret seed), with signatures of 64 bytes. We use the reference `ed25519-donna` or `libsodium` implementation depending on platform. Ed25519 provides 128-bit security against classical adversaries and is the consensus choice across the SimpleX, Signal, and SSH ecosystems.

**X25519 for Diffie-Hellman.** X25519 per RFC 7748 is the default key agreement. Public keys are 32 bytes. For operator-to-operator connections we optionally use X448 (56-byte keys, higher security margin) but X25519 is sufficient for all client-facing operations.

**ML-KEM-768 for post-quantum key encapsulation.** We use ML-KEM-768 as standardised in NIST FIPS 203 [NIST August 2024], formerly known as CRYSTALS-Kyber. Parameter set ML-KEM-768 provides NIST security category 3 (roughly equivalent to AES-192 against quantum adversaries). Public keys are 1184 bytes, ciphertexts are 1088 bytes, shared secrets are 32 bytes.

The choice of ML-KEM-768 over ML-KEM-512 follows current guidance in migration strategies: the 128-bit classical security level of ML-KEM-512 is considered insufficient margin against future cryptanalytic advances. ML-KEM-1024 offers NIST category 5 security but at roughly 40% larger key and ciphertext sizes; we consider ML-KEM-768 the efficient Pareto point for our latency budget over Tor.

**Hybrid KEM construction.** For forward secrecy against adversaries that may break either the classical or the post-quantum primitive, all sensitive key agreements use a hybrid construction:

```
(ss_x, ct_x) := X25519-Encap(pk_recipient_x)
(ss_k, ct_k) := ML-KEM-768-Encap(pk_recipient_k)
ss := HKDF-Extract(0x00 * 32, ss_x || ss_k)
```

The resulting shared secret `ss` is secure against an adversary that breaks either X25519 or ML-KEM-768 in isolation, provided the HKDF extraction is secure. This construction is standard in post-quantum transition designs and follows the pattern established in TLS 1.3 hybrid drafts [Stebila and Fluhrer, draft-ietf-tls-hybrid-design].

## 7.4 Reed-Solomon erasure coding

Reed-Solomon codes [Reed and Solomon, 1960] are Maximum Distance Separable (MDS) codes with the property that any k of n shares suffices to reconstruct the original data, and fewer than k shares reveals no information about the original (in the case of systematic codes, the first k shares happen to be the original data split into k pieces, but the construction we use is non-systematic for reasons described below).

We use a (k=3, n=5) Reed-Solomon code over GF(2^8) as specified in the `klauspost/reedsolomon` Go implementation, which is also the implementation used by Storj [Plank's tutorial, USENIX 2013; Storj whitepaper 2018]. The code is parameterised by a Vandermonde or Cauchy matrix of dimensions k × n; we use the Cauchy construction because it generalises to different field sizes more cleanly and avoids the need for matrix inversion during decode in the common case.

**Non-systematic encoding.** In a systematic Reed-Solomon code, the first k shares are the original data. We use a non-systematic variant where all n shares are linear combinations of the original, because in the systematic case an operator holding the first share holds a portion of plaintext directly. While the plaintext is AEAD-encrypted before erasure coding (see Section 10), the non-systematic variant provides an extra layer of protection and costs approximately 5% more CPU for encode and decode.

**Share size.** For an input ciphertext of size B bytes, each share has size ceil(B/k) = ceil(B/3) bytes plus a small header. Total storage overhead is n/k = 5/3 ≈ 1.67x the plaintext size, which compares favourably to full replication (3x or 5x) while tolerating up to n-k = 2 share losses.

**Decode threshold.** Reconstruction requires any k = 3 of the n = 5 shares. We do not employ a repair threshold distinct from the decode threshold in the baseline design, because the system is optimised for unlinked-file storage rather than live-updated objects.

## 7.5 Shamir's Secret Sharing for master keys

While Reed-Solomon suffices for the ciphertext blob, the master AEAD key itself must be distributed to the intended recipients of the file. For this we use Shamir's Secret Sharing [Shamir, Communications of the ACM 22(11):612-613, 1979] with a (3, 5) threshold matching the Reed-Solomon parameters.

Shamir's scheme works over a finite field (we use GF(2^256) via the secp256k1 scalar field for consistency with other prime-field operations; in practice libsodium's `crypto_secretbox` and a dedicated Shamir implementation like `codahale/sss` or `hashicorp/vault/shamir` are used). A random polynomial of degree k-1 = 2 is generated with the secret as the constant term. Five points on the polynomial are evaluated and distributed. Any three points permit Lagrange interpolation to recover the constant term; fewer than three reveal information-theoretically nothing.

**Why Shamir in addition to Reed-Solomon?** Reed-Solomon is a linear erasure code optimised for bulk data. Shamir's scheme is information-theoretically secure below threshold, which matters for the master key specifically: an operator holding k-1 shares of the ciphertext also holds k-1 shares of the master key, and the information-theoretic security of Shamir guarantees that those k-1 key shares contain zero bits of entropy about the key. If we had used Reed-Solomon on the key directly, a computationally unbounded adversary might in principle exploit the algebraic structure.

**Encryption of Shamir shares to recipients.** Each Shamir share is encrypted to the intended recipient's hybrid KEM public key and bundled with the file shares. When a recipient downloads k file shares, they also download their encrypted Shamir share, decapsulate it, and reconstruct the master key.

## 7.6 ECVRF for operator selection

Verifiable Random Functions (VRFs) produce outputs that are both pseudorandom and verifiable: given a VRF public key, input, output, and proof, anyone can verify that the output is the unique pseudorandom value associated with the input under the holder of the corresponding private key.

We use ECVRF-EDWARDS25519-SHA512-TAI as specified in RFC 9381 for deterministic, verifiable selection of operators for share placement. The construction is as follows:

```
input := epoch_seed || file_hash
(output, proof) := ECVRF.Prove(sk_uploader, input)
operators[0..5] := select_weighted(output, operator_registry, stakes)
```

The `epoch_seed` is an on-chain randomness beacon that rotates every N blocks. The `file_hash` is the BLAKE3 hash of the encrypted blob. The selection function chooses 5 operators from the registry weighted by stake.

**Why ECVRF?** Alternatives include plain HMAC-based selection (not verifiable by third parties) and Chainlink VRF (verifiable but requires external oracle and payment). ECVRF is verifiable by any party with the uploader's public key and the proof, and requires no external infrastructure. An attacker cannot bias selection without controlling the uploader's key.

## 7.7 PDQ perceptual hash for known-bad content matching

PDQ [Davis, "Open-sourcing photo- and video-matching technology to make the internet safer," Meta Engineering Blog 1 August 2019; ThreatExchange PDQ specification] is a perceptual hash developed by Meta and released open-source under the BSD license. Unlike cryptographic hashes, PDQ produces similar hashes for perceptually similar images, which is the desired property for matching images that have been minorly transformed (re-compressed, slightly cropped, colour-adjusted) against a known-bad list.

PDQ produces a 256-bit hash. Matching is by Hamming distance: two hashes with a Hamming distance less than a configurable threshold (typically 90 for Meta's deployment, lower for higher confidence) are considered a match. The construction is:

1. Convert input image to luminance at 64×64 resolution.
2. Apply a Discrete Cosine Transform (DCT).
3. Extract the 16×16 low-frequency coefficients.
4. Threshold against the median, yielding a 256-bit hash.

**Why PDQ over PhotoDNA?** PhotoDNA (Microsoft) is proprietary, requires licensing, and is therefore unavailable to open-source projects without special permission. PDQ is open-source, has a published specification, and its reference implementation is available at github.com/facebook/ThreatExchange. NCMEC accepts PDQ-computed hashes for CyberTipline integration since 2022.

**Constant-time comparison.** We compare input hashes against the known-bad list in constant time (all list entries are compared for every input) to avoid revealing through timing side-channels which entry matched. For a 10,000-entry list, this is approximately 40,000 XOR-popcount operations per comparison, well under 1ms on modern hardware.

## 7.8 Double Ratchet and X3DH

For pairwise messaging between users, DCD inherits the Double Ratchet algorithm [Perrin and Marlinspike, Signal specification] and the X3DH key agreement [Marlinspike and Perrin, Signal specification]. These are used as implemented in the existing SimpleGoX Rust codebase and are not modified by DCD. We mention them here for completeness; their specification is maintained upstream by the Signal Foundation and we do not re-specify.

**Hybrid Kyber integration.** The SimpleGoX implementation uses an X3DH variant with ML-KEM-768 integrated into the initial key agreement, following the pattern adopted by Signal in the PQXDH specification [Kret and Kotov, "The PQXDH Key Agreement Protocol," Signal Foundation September 2023]. This provides forward-secrecy against harvest-now-decrypt-later attacks using quantum computers.

## 7.9 Summary of primitives

| Primitive | Purpose | Standard | Library |
|:----------|:--------|:---------|:--------|
| XChaCha20-Poly1305 | AEAD encryption | draft-irtf-cfrg-xchacha | libsodium |
| Ed25519 | Digital signatures | RFC 8032 | libsodium |
| X25519 | Classical DH | RFC 7748 | libsodium |
| ML-KEM-768 | Post-quantum KEM | NIST FIPS 203 | liboqs / pqclean |
| SHA-256 | Hashing, HMAC | FIPS 180-4 | libsodium / stdlib |
| BLAKE3 | Fast hashing for integrity trees | BLAKE3 reference | blake3 crate |
| HKDF-SHA-256 | Key derivation | RFC 5869 | libsodium / stdlib |
| Reed-Solomon (3,5) | Erasure coding | Reed-Solomon 1960, Plank 2013 | klauspost/reedsolomon |
| Shamir (3,5) | Threshold key sharing | Shamir 1979 | hashicorp/vault/shamir |
| ECVRF-EDWARDS25519-SHA512-TAI | Verifiable randomness | RFC 9381 | Algorand reference |
| PDQ | Perceptual hashing | Meta 2019 | facebook/ThreatExchange |
| Double Ratchet | E2EE messaging | Signal spec | upstream |
| X3DH / PQXDH | Initial key agreement | Signal spec | upstream |

---

# 8. System Architecture

This section specifies the overall system architecture of SimpleGoX with integrated GoNode DCD. We proceed from the top-level component view through the principal data flows.

## 8.1 High-level component diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                             │
│                                                                  │
│  ┌──────────────┐   ┌──────────────┐   ┌──────────────────┐    │
│  │  SimpleGoX   │   │  SimpleGoX   │   │   SimpleGoX      │    │
│  │  (mobile)    │   │  (desktop)   │   │  (ESP32 SimpleGo)│    │
│  └──────────────┘   └──────────────┘   └──────────────────┘    │
│         │                  │                    │                │
│         └──────────────────┼────────────────────┘                │
│                            │                                     │
│     ┌──────────────────────▼────────────────────────┐           │
│     │          DCD Client Library (Rust)             │           │
│     │  - No-auto-download policy engine              │           │
│     │  - RAM-only render pipeline                    │           │
│     │  - (3,5) RS encoder/decoder + Shamir           │           │
│     │  - PDQ hash engine                             │           │
│     │  - Known-bad list verifier                     │           │
│     │  - TEE attestation client                      │           │
│     └───────────────────────┬────────────────────────┘          │
└─────────────────────────────│───────────────────────────────────┘
                              │ Tor v3 hidden service
                              │ (SMP and XFTP transport)
                              │
┌─────────────────────────────▼───────────────────────────────────┐
│                      SERVICE NODE LAYER                          │
│                                                                  │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │              GoNode Operator Pool (N ≥ 50)                │  │
│  │                                                            │  │
│  │  Operator_1      Operator_2      Operator_3   ... N       │  │
│  │  ┌──────────┐    ┌──────────┐    ┌──────────┐            │  │
│  │  │SMP relay │    │SMP relay │    │SMP relay │            │  │
│  │  │Share     │    │Share     │    │Share     │            │  │
│  │  │storage   │    │storage   │    │storage   │            │  │
│  │  │(1 of 5)  │    │(1 of 5)  │    │(1 of 5)  │            │  │
│  │  │Audit svc │    │Audit svc │    │Audit svc │            │  │
│  │  └──────────┘    └──────────┘    └──────────┘            │  │
│  └───────────────────────────────────────────────────────────┘  │
└───────────────────────────────┬─────────────────────────────────┘
                                │
┌───────────────────────────────▼─────────────────────────────────┐
│                    COORDINATION LAYER                            │
│                                                                  │
│   ┌─────────────────────────┐    ┌──────────────────────────┐   │
│   │  Arbitrum One Smart     │    │   Hash List Committee    │   │
│   │  Contracts              │    │                          │   │
│   │  - OperatorRegistry     │    │   - NCMEC liaison        │   │
│   │  - Staking (EURC/USDC)  │    │   - IWF liaison          │   │
│   │  - Slashing             │    │   - GoNode Foundation    │   │
│   │  - Epoch Randomness     │    │   - Rotating 4th member  │   │
│   │    (ECVRF anchor)       │    │                          │   │
│   └─────────────────────────┘    └──────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

## 8.2 Component responsibilities

### 8.2.1 SimpleGoX client

SimpleGoX is the user-facing application. On mobile it is an Android APK and iOS IPA; on desktop it is a Linux/macOS/Windows binary; on embedded hardware it is the SimpleGo firmware for ESP32-based devices (LilyGo T-Deck Plus is the reference hardware).

The client embeds the DCD Client Library (Rust, no_std-capable subset for embedded) that handles all cryptographic operations, share management, and rendering policy. The UI layer on each platform is responsible for user-facing decisions (explicit tap to view media, confirmation dialogs, setting screens) but delegates all security-sensitive operations to the library.

### 8.2.2 GoNode operator

A GoNode operator runs a service node that combines:

- **SMP relay:** Forwards end-to-end encrypted messages between client queue addresses per the SimpleX Messaging Protocol. Operators observe only ephemeral queue identifiers, not persistent user identities.
- **Share storage:** Stores individual Reed-Solomon shares of encrypted files. Storage is content-addressed by the share hash.
- **Audit service:** Responds to audit challenges (Section 9.8) to prove continued possession of stored shares.

Operators are identified by an Ed25519 public key registered in the OperatorRegistry smart contract. Operator selection for share placement uses ECVRF over the current operator set weighted by stake.

### 8.2.3 Smart contract layer

Deployed on Arbitrum One (Layer 2 of Ethereum, chosen for low fees and EVM compatibility). Contracts:

- **OperatorRegistry:** Maps operator Ed25519 public keys to staked capital, jurisdiction declarations, and service endpoints.
- **Staking:** Holds EUR-denominated (EURC) stakes. Stakes are slashable under defined conditions.
- **Slashing:** Processes slashing events based on audit-failure evidence.
- **EpochRandomness:** Provides the periodic beacon used as ECVRF seed input.

Smart contracts are open-source, audited, and subject to a 24-hour timelock on parameter changes during Phase 0-3.

### 8.2.4 Hash list committee

Maintains the known-bad hash list used by clients for pre-render filtering. Structure:

- 4-of-4 multisig for list updates, rotating composition:
  - Seat 1: NCMEC liaison (U.S. CyberTipline coordination)
  - Seat 2: IWF liaison (UK Internet Watch Foundation coordination)
  - Seat 3: GoNode Foundation nominee (rotating annually)
  - Seat 4: Rotating independent civil-society nominee (EFF, EDRi, CCC, Chaos Computer Club, or equivalent, rotating every 6 months)

The committee publishes list updates signed with a 4-of-4 Ed25519 multisig over a Merkle tree of hash entries. Clients verify the signature before applying updates.

## 8.3 Trust model

We state explicitly what each party must trust and what each party is trusted to do:

| Party | Trusts | Is trusted to |
|:------|:-------|:--------------|
| User | Their own client, their own device, the hash list committee (to not omit known-bad entries), the crypto primitives | Operate the client faithfully, not share private keys |
| Sender | Recipient to not leak content post-decryption | Faithfully encrypt and distribute shares |
| Recipient | Sender to not send illegal content | Faithfully apply hash filter before render |
| Operator | Stake mechanism, audit protocol, the other operators to not all collude | Store shares, respond to audit, forward SMP messages |
| Moderator | TEE (if used), the crypto primitives | Act in good faith on flagged content |
| Foundation | Committee members, audit firms | Fund audits, coordinate protocol upgrades |

The system does not require any party to trust any other single party. The most trust-demanding component is the hash list committee, and that is mitigated by 4-of-4 multisig with publicly-auditable updates.

## 8.4 Deployment topology

Reference deployment on launch (Phase 0 to Phase 1):

- Initial operator pool: 10-20 operators recruited from the existing SimpleGo Ecosystem SMP operator community, primarily in Germany, the Netherlands, Iceland, Switzerland, and Panama. The user's existing 10 SMP servers and 1 XFTP server form the bootstrap set.
- Smart contract deployment on Arbitrum One testnet (Sepolia) for Phase 0, migration to Arbitrum One mainnet for Phase 1.
- Hash list committee constituted with founder members prior to Phase 0; rotation begins in Phase 1.
- Clients available for Linux x86_64 and aarch64 (desktop), Android aarch64, iOS arm64, and ESP32-S3 (firmware).

---

# 9. Protocol Specifications

This section specifies the wire formats and state machines for the principal DCD protocols. Wire formats are given in a pseudo-ASN.1 notation for clarity; the canonical implementation uses CBOR (RFC 8949) with defined tag assignments.

## 9.1 Operator handshake protocol

The operator handshake establishes a mutually-authenticated TLS 1.3 channel between a client and an operator for a session. The handshake is layered over Tor v3 hidden services, which themselves provide transport authentication of the operator to the client; this second layer authenticates the client's ephemeral session to the operator and provides forward secrecy independent of Tor.

```
Client                                                    Operator
  |                                                           |
  |------ ClientHello ---------------------------------------->|
  |       TLS 1.3 with ALPN = "gonode/1"                      |
  |       Supported groups: X25519, secp256r1                 |
  |       Hybrid KEM extension: ML-KEM-768                    |
  |                                                           |
  |<----- ServerHello, Certificate, CertificateVerify ---------|
  |       Operator Ed25519 cert issued by OperatorRegistry    |
  |       Certificate chains to smart contract root           |
  |                                                           |
  |------ Finished ------------------------------------------->|
  |                                                           |
  |<----- Finished ------------------------------------------- |
  |                                                           |
  |====== Application data (CBOR-over-TLS) ===================|
```

The operator's certificate is a self-signed X.509 certificate whose public key matches the Ed25519 key registered in the OperatorRegistry smart contract. The client verifies the registration on-chain (with local caching to avoid per-handshake RPC calls) and accepts the certificate if the registration is current and the operator is not slashed.

## 9.2 Share upload protocol

To upload a file, the client first encrypts the plaintext with a random XChaCha20-Poly1305 key, computes Reed-Solomon shares, and distributes them.

**Plaintext encryption.** Given plaintext `P`:

```
k := random(32)            // master key
n := random(24)            // nonce
aad := "GoNode-DCD-file-v1" || file_metadata
C := Enc_k(n, aad, P)      // ciphertext with 16-byte tag appended
file_hash := BLAKE3(C)
```

**Erasure coding.** Apply (3,5) Reed-Solomon to the ciphertext:

```
shares := ReedSolomon.encode(C, k=3, n=5)
  // shares[i] has length ceil(len(C)/3) for i in 0..5
```

**Per-share subkey derivation and re-encryption.** Each share is re-encrypted with a share-specific subkey:

```
for i in 0..5:
  subkey_i := HKDF-Expand(k, "GoNode-DCD-Share-Subkey-v1" || i || file_hash, 32)
  share_nonce_i := random(24)
  share_aad_i := "GoNode-DCD-share-v1" || file_hash || i
  wrapped_share_i := Enc_{subkey_i}(share_nonce_i, share_aad_i, shares[i])
```

**Operator selection.** Using ECVRF:

```
epoch_seed := current_epoch_seed()
(vrf_output, vrf_proof) := ECVRF.Prove(sk_uploader, epoch_seed || file_hash)
operators[0..5] := stake_weighted_select(vrf_output, operator_registry)
```

**Upload transaction.** For each selected operator, the client sends:

```
StoreShareRequest ::= SEQUENCE {
  version         INTEGER (1),
  file_hash       OCTET STRING (SIZE 32),
  share_index     INTEGER (0..4),
  wrapped_share   OCTET STRING,
  share_nonce     OCTET STRING (SIZE 24),
  upload_credit   Credit,            -- signed payment proof
  uploader_pubkey OCTET STRING (SIZE 32),  -- ephemeral, not persistent identity
  vrf_proof       OCTET STRING,
  signature       OCTET STRING (SIZE 64)   -- Ed25519 by uploader_pubkey over the above
}
```

The operator verifies the VRF proof (confirming they are a legitimate selection), accepts the upload credit, stores the wrapped share indexed by `file_hash || share_index`, and returns:

```
StoreShareResponse ::= SEQUENCE {
  receipt_sig     OCTET STRING (SIZE 64),  -- Operator's Ed25519 sig over file_hash || share_index || timestamp
  timestamp       INTEGER,
  ttl             INTEGER                   -- seconds
}
```

The client retains all five receipts as proof of upload.

**Master key distribution.** The master key `k` is split via Shamir (3,5):

```
shamir_shares := ShamirSSS.split(k, k=3, n=5)
```

For each recipient R_j of the file (each member of the target group):

```
(ss_xj, ct_xj) := X25519-Encap(pk_R_j_x)
(ss_kj, ct_kj) := MLKEM768-Encap(pk_R_j_kem)
wrap_key_j := HKDF-Extract(file_hash, ss_xj || ss_kj)
wrap_nonce_j := random(24)
wrapped_key_j := Enc_{wrap_key_j}(wrap_nonce_j, file_hash, shamir_shares[j % 5])
```

The wrapped keys plus KEM ciphertexts are distributed via the normal SMP message channel to recipients. A recipient receives notification that a new file is available, along with the file_hash and their wrapped Shamir share.

## 9.3 Share retrieval protocol

When a recipient explicitly requests a file:

1. **Key unwrapping.** The recipient decapsulates their wrapped key:

```
ss_x := X25519-Decap(sk_R_x, ct_x)
ss_k := MLKEM768-Decap(sk_R_kem, ct_k)
wrap_key := HKDF-Extract(file_hash, ss_x || ss_k)
shamir_share := Dec_{wrap_key}(wrap_nonce, file_hash, wrapped_key)
```

2. **Operator lookup.** The recipient computes the same ECVRF output as the uploader (using the uploader's public key and the file_hash) to identify the 5 operators. Note: the uploader must include their VRF proof in the file metadata for this to be verifiable, but since the recipient receives metadata via the authenticated E2EE channel, the uploader can simply list the operators directly.

3. **Share fetch.** The recipient sends `FetchShareRequest` to any 3 of the 5 operators:

```
FetchShareRequest ::= SEQUENCE {
  version         INTEGER (1),
  file_hash       OCTET STRING (SIZE 32),
  share_index     INTEGER (0..4),
  fetch_credit    Credit,
  requester_pubkey OCTET STRING (SIZE 32),  -- ephemeral
  signature       OCTET STRING (SIZE 64)
}
```

Operators respond:

```
FetchShareResponse ::= SEQUENCE {
  wrapped_share   OCTET STRING,
  share_nonce     OCTET STRING (SIZE 24),
  operator_sig    OCTET STRING (SIZE 64)    -- over hash of wrapped_share
}
```

4. **Decryption and reassembly.** The client unwraps each share with the corresponding subkey (derived from the master key), then feeds the 3 shares to Reed-Solomon decode:

```
for each returned share i:
  subkey_i := HKDF-Expand(master_key, "GoNode-DCD-Share-Subkey-v1" || i || file_hash, 32)
  share_plaintext_i := Dec_{subkey_i}(share_nonce_i, "GoNode-DCD-share-v1" || file_hash || i, wrapped_share_i)

C := ReedSolomon.decode(share_plaintexts)
P := Dec_k(n, aad, C)
```

5. **Pre-render hash check.** Before any rendering, the plaintext P is subjected to PDQ hash comparison (Section 13).

6. **Render.** If P passes the hash check, it is rendered in a locked-memory buffer per Section 11.

## 9.4 Group join protocol

When a user joins a group:

1. The group owner or an authorised member sends an invitation containing the group's public state:
   - Group identifier (a 32-byte hash)
   - Current member list with public keys
   - Group-specific DCD policy settings (e.g., whether confirmed-contact auto-download is permitted)
   - Moderator public keys and authorisation proof

2. The joining client does **not** fetch profile pictures for existing members. Each member is rendered with a deterministic silhouette:

```
silhouette_color := HKDF-Expand(member_pubkey, "GoNode-DCD-Silhouette-v1", 3)  // RGB
silhouette_shape := hash_to_shape_index(member_pubkey) mod 8  // 8 shape variants
```

The silhouette is deterministic across all clients that render this member, providing a stable visual identity without requiring fetch.

3. The joining client announces its own public key to the group. Other members receive the announcement and render a silhouette for the new member, also without fetching.

**No media fetch occurs at join time.** This is the central departure from all existing messengers.

## 9.5 Explicit fetch protocol

If a user taps on a silhouette or on a placeholder for a media message:

1. Client displays a confirmation dialog stating: "Fetch [profile picture / media] from this [contact / group member]? The content will be displayed once and not saved to disk."

2. On confirmation, the client executes the Share Retrieval Protocol (9.3).

3. Rendered content is displayed in a locked-memory buffer per Section 11.

4. On dismissal of the render surface, the buffer is overwritten with `explicit_bzero`.

For confirmed contacts, per-contact settings may disable the confirmation dialog and optionally enable persistent caching. Persistent caching is always opt-in per confirmed contact and is disabled by default.

## 9.6 Audit challenge protocol

To provide ongoing proof that operators hold the shares they claim to hold, a periodic audit challenge protocol is run. The design follows established proof-of-retrievability schemes [Juels and Kaliski, "PORs: Proofs of Retrievability for Large Files," CCS 2007; Ateniese et al., "Provable Data Possession at Untrusted Stores," CCS 2007].

**Challenge generation.** Per epoch (e.g., every 6 hours), the smart contract emits a random challenge nonce `chl`. Any party can challenge an operator to prove storage of a specific share:

```
ChallengeRequest ::= SEQUENCE {
  file_hash       OCTET STRING,
  share_index     INTEGER,
  chl             OCTET STRING (SIZE 32),  -- epoch challenge nonce
  positions       SEQUENCE OF INTEGER       -- random byte positions to prove
}
```

The operator responds:

```
ChallengeResponse ::= SEQUENCE {
  share_bytes_at_positions  OCTET STRING,
  blake3_proof              OCTET STRING,  -- BLAKE3 authentication path
  operator_sig              OCTET STRING
}
```

The `positions` are derived from `chl` and are unpredictable to the operator before challenge time, so the operator cannot pre-compute responses without retaining the share data.

**Slashing.** Failed challenges (timeout or incorrect response) accumulate in a slashing buffer. Beyond a threshold (e.g., 3 failures in 7 days), the operator's stake is partially slashed via the smart contract.

## 9.7 Repair protocol

When an operator is slashed, drops out, or loses data, their shares must be regenerated from surviving shares to maintain redundancy.

1. Upon slashing or drop-out detection, the OperatorRegistry emits a `RepairNeeded` event listing the file hashes affected.

2. A volunteer operator (typically one with surplus capacity, incentivised by a repair fee) fetches any 3 shares of the affected files, decodes to plaintext, re-encodes to 5 shares, and distributes the replacement share to a new operator selected by ECVRF.

3. **Confidentiality during repair.** The repair operator is not authorised to see plaintext. The architecture requires that repair is executed by a subset of the original 5 operators cooperating: 3 of them reassemble the ciphertext blob (not the AEAD-encrypted plaintext, which they lack the master key for) in a locked-memory enclave, re-encode, and distribute new shares. No party in the repair flow gains access to the master key.

This construction preserves the confidentiality property during repair and is a minor contribution of this whitepaper beyond the Storj design, which permits repair operators to observe full plaintext because Storj assumes client-side encryption was already applied before erasure coding.

## 9.8 Summary of protocols

| Protocol | Initiator | Responder | Purpose |
|:---------|:----------|:----------|:--------|
| Operator handshake | Client | Operator | Establish mutually-authenticated session |
| Share upload | Uploader client | 5 selected operators | Distribute encrypted shares |
| Share retrieval | Recipient client | 3+ operators | Fetch shares for reassembly |
| Group join | Joiner | Existing members | Become member without fetching media |
| Explicit fetch | User action | Share retrieval | User-initiated media view |
| Audit challenge | Auditor (any party) | Operator | Prove continued storage |
| Repair | Repair operator | Surviving operators | Regenerate lost shares |

---

# 10. Storage Layer: Distributed Erasure-Coded Design

This section specifies the storage layer in detail, with parameter justifications, performance characteristics, and failure-mode analysis.

## 10.1 Parameter choices

### 10.1.1 Why (3,5) Reed-Solomon

The choice of k=3, n=5 reflects a balance among:

- **Storage overhead:** 5/3 ≈ 1.67x plaintext size, comparable to 2x mirror and materially better than 3x replication.
- **Fault tolerance:** Can tolerate up to n-k = 2 simultaneous operator failures or compromises without data loss.
- **Confidentiality threshold:** Below 3 shares, information-theoretic (via Shamir for keys) and cryptographic (via AEAD for ciphertext) security.
- **Implementation simplicity:** (3,5) over GF(2^8) has very fast encode/decode on modern CPUs (>2 GB/s single-threaded).
- **Operational feasibility:** Selecting 5 operators from the pool is practical even for small operator pools (≥10 operators suffices for reasonable ECVRF distribution).

We considered (5,8), (10,16), (29,80) like Storj, and other parameterisations. The (3,5) choice is optimised for the target workload: messenger media with typical sizes of 100 KB to 20 MB, high upload volume, and user-expected latency of sub-second for thumbnails and a few seconds for full media.

For extremely large files (>100 MB), we support an optional (7,10) mode with lower storage overhead (10/7 ≈ 1.43x) at the cost of requiring 7 share fetches for reassembly. This mode is negotiated per-upload and is out of scope for the messenger baseline.

### 10.1.2 Why GF(2^8)

Reed-Solomon codes can be defined over any finite field. The choice of GF(2^8) (256-element field, elements fit in a single byte) is driven by:

- **CPU vectorisation:** GF(2^8) arithmetic vectorises to SSE/AVX/NEON with excellent throughput.
- **Library maturity:** The `klauspost/reedsolomon` implementation is production-proven in Storj, Backblaze, MinIO.
- **Sufficient for n ≤ 256:** GF(2^8) supports codes with up to 255 total shares, well beyond our 5-share or 10-share configurations.

## 10.2 Share layout and metadata

Each share stored on an operator consists of:

```
ShareRecord ::= SEQUENCE {
  version         INTEGER (1),
  file_hash       OCTET STRING (SIZE 32),
  share_index     INTEGER (0..4),
  wrapped_share   OCTET STRING,
  share_nonce     OCTET STRING (SIZE 24),
  upload_ts       INTEGER,
  uploader_pubkey OCTET STRING (SIZE 32),
  ttl             INTEGER,                -- seconds from upload_ts
  stake_lock      OCTET STRING            -- reference to stake slot guaranteeing availability
}
```

The operator stores this record keyed by `(file_hash, share_index)` and exposes it via the FetchShareRequest protocol (Section 9.3).

The operator does not store (and has no way to compute):
- The master AEAD key `k`
- The plaintext `P`
- The identities of other operators holding sibling shares
- The identities of the intended recipients

## 10.3 Operator selection via ECVRF

Share placement is determined by ECVRF output over the tuple (epoch_seed, file_hash, uploader_pubkey). The selection algorithm:

```
function select_operators(vrf_output, registry, n=5):
  operators := []
  seen := set()
  rand := prng_from_seed(vrf_output)
  while len(operators) < n:
    r := rand.next_uniform(0, total_stake)
    op := weighted_pick(registry, r)
    if op not in seen:
      operators.append(op)
      seen.add(op)
  return operators
```

The selection is:
- **Deterministic:** Same VRF output always yields same operator set.
- **Verifiable:** Any party with the VRF proof can recompute.
- **Weighted:** Operators with higher stake are more likely to be selected, aligning economic incentives.
- **Unbiasable:** Uploader cannot pre-compute favourable selections without breaking ECVRF security (tantamount to forging signatures).
- **Jurisdictionally diverse (soft constraint):** The selection algorithm includes a preference for jurisdiction diversity by applying a penalty to operators in the same jurisdiction as already-selected ones. This is implemented as a secondary weighting.

## 10.4 Jurisdiction declarations and metadata

Operators declare their operating jurisdiction at registration:

```
OperatorRegistration ::= SEQUENCE {
  pubkey          OCTET STRING (SIZE 32),
  endpoint        OCTET STRING,          -- Tor v3 onion address
  stake_amount    INTEGER,                -- in EURC wei
  jurisdiction    VisibleString,          -- ISO 3166-1 alpha-2
  operator_name   VisibleString OPTIONAL,
  contact_pgp     OCTET STRING OPTIONAL,
  sig             OCTET STRING (SIZE 64)
}
```

Jurisdiction declarations are self-reported and are a soft input to the selection algorithm rather than a verified fact. Operators who declare falsely and are discovered are subject to slashing. The goal is jurisdictional diversity for confidentiality against state-level actors, not absolute guarantees.

Typical target distribution in a healthy operator pool:
- 20-30% EU (Germany, Netherlands, Iceland, Finland)
- 20-30% Switzerland, Norway, Iceland, other EEA-adjacent
- 15-20% Central/South America (Panama, Costa Rica, Uruguay)
- 15-20% Asia-Pacific (Singapore, Taiwan, Australia)
- 10-15% North America (Canada, specific US states)

## 10.5 Storage durability calculation

Using the methodology from Storj's durability documentation [Storj Docs, "Understanding File Redundancy"]:

Given:
- n = 5, k = 3
- Per-operator availability p = 0.999 (achievable with 24/7 operators on commodity hardware)
- Monthly repair cycle

Probability that fewer than 3 of 5 operators are available at any moment:

```
P(failure) = Σ_{i=0}^{2} C(5,i) * p^i * (1-p)^(5-i)
           = C(5,0) * 0.999^0 * 0.001^5 + C(5,1) * 0.999^1 * 0.001^4 + C(5,2) * 0.999^2 * 0.001^3
           ≈ 1e-15 + 5e-12 + 1e-8
           ≈ 1e-8
```

Probability of durable loss per file per month (with monthly repair):

```
P(loss | month) ≈ 10^-8
```

This is approximately 8 nines of durability per month, exceeding typical cloud storage SLAs. With more operators and active repair, 10+ nines is achievable.

## 10.6 Deletion semantics

Files have a user-specified or group-policy-specified TTL. After TTL expiration:
- Operators are authorised to delete the share.
- Operators who delete retain a record of the deletion in their audit log.
- Clients attempting to fetch expired shares receive an `ExpiredShare` response.

For early deletion (user-initiated), the client issues a signed deletion request to each of the 5 operators:

```
DeletionRequest ::= SEQUENCE {
  file_hash       OCTET STRING,
  share_index     INTEGER,
  deletion_proof  OCTET STRING,          -- signature by uploader or authorised deleter
  timestamp       INTEGER
}
```

Operators delete and return a signed deletion receipt.

**Cryptographic deletion fallback.** If an operator refuses to honour deletion, the file still becomes cryptographically inaccessible once the recipient deletes their master key. Since the master key is split across recipients (not stored by operators), operators holding shares without any recipient holding the key cannot reconstruct plaintext. This is a principal advantage of the split-key architecture over naïve cloud storage.

## 10.7 Repair economics

Repair costs (CPU + bandwidth) are borne by volunteer repair operators. The smart contract compensates repair work from the slashed stake of the failed operator:

```
repair_fee = λ * slashed_stake
```

where λ is a governance parameter (initially 0.3) intended to cover the repair operator's CPU and bandwidth cost. Remaining slashed stake goes to the protocol treasury or is burned, depending on governance vote.

This creates an economic flywheel: operator failures pay for the repairs they necessitate, and honest operators are not cross-subsidising repair of failed operators.

## 10.8 Comparison with Storj and Sia

| Property | Storj | Sia | DCD |
|:---------|:------|:----|:----|
| Erasure code | Reed-Solomon (29,80) | Reed-Solomon (10,30) | Reed-Solomon (3,5) |
| Storage overhead | 2.76x | 3.0x | 1.67x |
| Recipient decrypt | Client holds full key | Client holds full key | Shamir threshold key |
| Repair sees plaintext | Yes | Yes | **No** |
| Content-aware filtering | No | No | **Yes (client-side PDQ)** |
| Token | STORJ (ERC-20) | SC (native) | None (EURC) |
| Smart contract platform | Ethereum mainnet | Sia native chain | Arbitrum One L2 |

The distinguishing features of DCD are: (a) split-key architecture where no repair operator sees plaintext, (b) client-side content-aware filtering integrated into the architecture, (c) no native token, and (d) much smaller erasure code parameters optimised for messenger workloads rather than general cloud storage.

---


# 11. Client Layer: No Auto-Download and RAM-Only Rendering

The client layer is where DCD's user-facing protection is implemented. All prior layers (storage, operators, smart contracts) matter only insofar as they support the client's ability to keep illegal content off the user's persistent storage by default.

## 11.1 The default contract

DCD establishes the following default contract with the user:

1. When you join a group, no media is fetched from any other member of that group.
2. When a new message arrives, no media is fetched until you explicitly indicate you want to see it.
3. When you explicitly indicate you want to see media, it is fetched, checked against the known-bad list, and displayed in a way that does not write it to your disk.
4. If you confirm a contact (exchange verified key fingerprints out-of-band), you can opt that specific contact into auto-fetch on a per-contact basis. The default remains no auto-fetch.

This contract is more conservative than any mainstream messenger and is the specific behavior that prevents the threat models documented in Section 2.

## 11.2 Silhouette generation

When a user is displayed in a UI context (contact list, group member list, message sender attribution) and their profile picture has not been fetched and confirmed, the client renders a deterministic silhouette derived from the user's public key.

**Deterministic colour:** 

```
rgb := HKDF-Expand(pubkey, "GoNode-DCD-Silhouette-Color-v1", 3)
```

Produces a 24-bit RGB value that is consistent across all clients. Colours are constrained to a palette of ~64 distinguishable shades to avoid accessibility issues (low-contrast or colour-blind unfriendly combinations are filtered out).

**Deterministic shape:**

```
shape_seed := HKDF-Expand(pubkey, "GoNode-DCD-Silhouette-Shape-v1", 4)
shape_index := int32_from_bytes(shape_seed) mod NUM_SHAPES
```

Shapes are drawn from a predefined set (initial set: 32 abstract geometric patterns designed to be visually distinct at thumbnail size).

**Anti-confusion property:** Two users with colliding silhouettes can be distinguished by mouse-over or long-press to reveal the full public-key fingerprint. The silhouette is never claimed to be a unique identifier; it is a visual hint.

## 11.3 Explicit fetch flow

When a user taps a silhouette or a media placeholder, the following state machine is traversed:

```
                  ┌─────────────┐
                  │  Idle       │
                  │  (silhouette│
                  │  displayed) │
                  └──────┬──────┘
                         │ user tap
                         ▼
                  ┌─────────────┐
                  │ Confirmation│
                  │  dialog:    │
                  │  "Fetch?"   │
                  └──────┬──────┘
                         │ user confirm
                         ▼
                  ┌─────────────┐
                  │  Fetching   │──── on timeout/error ──> Idle (with error)
                  │  (3 shares) │
                  └──────┬──────┘
                         │ 3 shares received
                         ▼
                  ┌─────────────┐
                  │  Reassembly │
                  │  (locked RAM│
                  │   buffer)   │
                  └──────┬──────┘
                         │ plaintext in buffer
                         ▼
                  ┌─────────────┐
                  │  Hash check │──── match ──> Abort, report
                  │  (PDQ)      │
                  └──────┬──────┘
                         │ clean
                         ▼
                  ┌─────────────┐
                  │  Render     │
                  │  (locked    │
                  │   surface)  │
                  └──────┬──────┘
                         │ user dismisses
                         ▼
                  ┌─────────────┐
                  │  Purge:     │
                  │  explicit_  │
                  │  bzero      │
                  └─────────────┘
```

Each transition is governed by explicit user action or deterministic timeout. No media reaches the Render state without passing the hash check.

## 11.4 Locked-memory buffer implementation

The reassembled plaintext is held in a memory region allocated with the following properties:

**POSIX implementation (Linux, macOS, *BSD):**

```c
void *buf = mmap(NULL, size, PROT_READ | PROT_WRITE,
                 MAP_PRIVATE | MAP_ANONYMOUS | MAP_LOCKED, -1, 0);
if (buf == MAP_FAILED) { /* handle */ }
if (mlock(buf, size) != 0) { /* handle: swap cannot be guaranteed */ }
madvise(buf, size, MADV_DONTDUMP);  // exclude from core dumps
```

`MAP_LOCKED` at mmap time plus `mlock` at post-allocation provides belt-and-braces swap avoidance. `MADV_DONTDUMP` ensures the region is not included in process core dumps, preventing a crash-time leak to disk.

**Linux-specific hardening:**

```c
prctl(PR_SET_DUMPABLE, 0);  // process-wide: no core dumps at all during sensitive operations
```

We temporarily disable dumpability for the process during the render session and re-enable afterward if required.

**Windows implementation:**

```c
VirtualLock(buf, size);
// No direct equivalent to MADV_DONTDUMP; rely on mlock-equivalent and process integrity
```

**Purge on dismiss:**

```c
explicit_bzero(buf, size);     // cannot be optimized away by compiler
munlock(buf, size);
munmap(buf, size);
```

`explicit_bzero(3)` is specifically designed for this use case and is guaranteed not to be elided by compiler optimizations. On platforms without `explicit_bzero`, we use `SecureZeroMemory` on Windows or a manual `volatile`-pointer loop as fallback.

## 11.5 Rendering surface

Plaintext image data must be rasterized for display. This creates two additional residues:

- **GPU memory.** Modern rendering pipelines upload image data to the GPU. GPU memory is not swept by `explicit_bzero` on the CPU side.
- **Display compositor.** Window system compositors (Wayland, Quartz, DirectComposition) may retain surface contents in their own buffers.

**GPU hardening:**

```
// OpenGL approach
glDeleteTextures(1, &texture_id);
glFlush(); glFinish();  // ensure GPU state is settled before we move on

// Vulkan approach
vkDestroyImageView(...);
vkFreeMemory(...);  // explicit free of backing memory

// Metal (iOS/macOS)
MTLResource.setPurgeableState(.empty)
```

These calls request that the GPU release and mark-as-reusable the texture memory. Whether this memory is actually zeroed depends on driver implementation; in practice modern drivers zero memory before reallocation to other processes, but do not zero immediately.

**Compositor hardening:**

On Android we set `FLAG_SECURE` on the window:

```java
getWindow().setFlags(LayoutParams.FLAG_SECURE, LayoutParams.FLAG_SECURE);
```

This prevents screenshots, recents-view previews, and screen recording. Similar mechanisms exist on iOS (prevent snapshot on background), macOS (`NSWindowSharingNone`), and Windows (`SetWindowDisplayAffinity(WDA_EXCLUDEFROMCAPTURE)`).

## 11.6 Cache policy for confirmed contacts

Once a user explicitly confirms a contact (out-of-band verification of the contact's public key fingerprint, typically via QR code in person or video call), a per-contact setting allows optional persistent caching:

```
ContactSettings ::= SEQUENCE {
  contact_pubkey        OCTET STRING,
  verified              BOOLEAN,
  verification_method   ENUMERATED {manual, qr_in_person, qr_video_call, ...},
  auto_fetch_media      BOOLEAN DEFAULT FALSE,
  persist_cache         BOOLEAN DEFAULT FALSE,
  cache_ttl             INTEGER DEFAULT 0
}
```

Default values are conservative: even after confirmation, auto-fetch and persist-cache are disabled unless the user opts in.

When `persist_cache = TRUE`, cached media is stored encrypted with a device-specific key derived from the OS keychain/keystore:

```
cache_key := HKDF-Extract(device_secret_from_keystore, "GoNode-DCD-Cache-v1")
cache_entry := Enc_{cache_key}(random_nonce, contact_pubkey, plaintext)
```

The device secret is held in the hardware-backed keystore (Android Keystore, iOS Keychain, macOS Keychain, Windows DPAPI). If the device is seized powered-off, the keystore is inaccessible without device unlock; the cache is therefore practically decrypted only while the user has authenticated.

## 11.7 Uninstall and data clearing

On user-initiated uninstall or data clearing:

1. All cached files are overwritten with `explicit_bzero` before unlinking.
2. The device secret is destroyed via keystore API.
3. All app data directories are securely wiped per platform-specific best practice.

## 11.8 Differences from existing messengers

| Behavior | Signal | WhatsApp | Telegram | SimpleX | DCD |
|:---------|:-------|:---------|:---------|:--------|:----|
| Auto-fetch profile pic on group join | Yes | Yes | Yes | Yes | **No** |
| Auto-download image in group | Yes (Wi-Fi) | Yes (Wi-Fi) | Yes | Yes (threshold) | **No** |
| Persistent disk cache for unconfirmed | Yes | Yes | Yes | Yes | **No** |
| FLAG_SECURE for sensitive surfaces | No (default) | No (default) | No | Partial | **Yes** |
| explicit_bzero on dismiss | No | No | No | No | **Yes** |
| Cache encrypted with device keystore | Partial | No | No | No | **Yes** |

The column for DCD represents a meaningful departure from the industry baseline.

---

# 12. Moderation Layer: TEE-Based Classification

Moderation in E2EE messengers is a well-known hard problem. The server-side scanning approach, deployed by Meta, Microsoft, and Google for non-E2EE services, is incompatible with E2EE by construction. The client-side scanning approach, proposed by Apple in 2021 (NeuralHash) and in the EU Chatkontrolle proposal, creates a surveillance apparatus that can be repurposed and was rejected in both cases after intense security-community pushback [EFF, "Apple's Plan to 'Think Different' About Encryption Opens a Backdoor to Your Private Life," August 2021].

DCD's approach occupies a narrow middle ground: moderation is performed by human moderators chosen by group members, but the moderators' own devices do not retain the moderated content in any recoverable form. This is achieved through Trusted Execution Environments (TEEs).

## 12.1 TEE options surveyed

**ARM TrustZone** [ARM Architecture Reference Manual]: The secure-world execution environment available on essentially all ARM application processors manufactured since approximately 2014. Provides a small isolated execution environment separated from the normal-world operating system by hardware. Mobile implementations commonly expose TrustZone via OP-TEE (open-source) or proprietary TEE OS (Qualcomm Trusted Execution Environment, Samsung TEEgris, etc.).

**Apple Secure Enclave** [Apple Platform Security Guide, 2023]: A dedicated coprocessor on Apple silicon with its own memory and boot process. Exposed to application developers via CryptoKit for limited cryptographic operations; general-purpose execution is not permitted to third-party apps.

**Intel SGX** [Intel SGX Programming Reference]: Software Guard Extensions on Intel CPUs (Skylake through Ice Lake client; server-class support continues on Xeon). Provides enclaves with encrypted memory. Deprecated on client Intel CPUs after approximately 2021; remains on server-class for confidential computing.

**AMD SEV (Secure Encrypted Virtualization)** [AMD SEV-SNP whitepaper]: Memory encryption at the hypervisor level, suited to server deployments rather than per-application enclaves.

**Intel TDX (Trust Domain Extensions)** [Intel TDX specification]: Successor to SGX, oriented toward confidential VMs.

**Google Titan M / Titan M2:** Dedicated security chip in Pixel phones; similar in role to Apple Secure Enclave.

## 12.2 TEE fragmentation problem

The brutal honest assessment: TEE availability on mobile in 2026 is fragmented and heterogeneous.

- iOS devices: Secure Enclave is universal but third-party developer access is limited to cryptographic primitives (key generation, signing, decapsulation). General-purpose classifier execution in Secure Enclave is not exposed.
- Android devices: TrustZone is present but application-level access requires either OEM-specific APIs (not portable across manufacturers) or the Android Keystore subset of functionality (again, cryptographic primitives only).
- Desktop: Intel SGX is deprecated on client CPUs. AMD SEV is a virtualisation technology, not per-app. TPM 2.0 is universal on Windows 11 but provides only a narrow set of operations.

This means a general-purpose content classifier running inside a TEE is, for most users in 2026, not available as a deployable primitive. The honest engineering response is to build for the cases where it is available and provide alternatives for the cases where it is not.

## 12.3 DCD moderation architecture

DCD offers three moderation modes, negotiated per group:

### Mode A: TEE-based classifier (strongest guarantees, limited availability)

On devices with suitable TEE (developer-mode Android with TrustZone access via Trusty, server-side SGX for centralised moderation groups, confidential-computing VMs), the moderation classifier runs inside the TEE:

```
┌─────────────────────────────────────────────┐
│  Host OS (untrusted for moderation content) │
│                                              │
│   ┌──────────────────────────────────┐     │
│   │  SimpleGoX Moderator App          │     │
│   │                                    │     │
│   │  - Receives encrypted shares       │     │
│   │  - Forwards to TEE                 │     │
│   │  - Receives Boolean + attestation  │     │
│   │                                    │     │
│   └────────────┬─────────────────────┘      │
│                │                             │
│   ═══════════ TEE boundary ══════════════    │
│                │                             │
│   ┌────────────▼──────────────────────┐    │
│   │  TEE enclave                       │    │
│   │                                     │    │
│   │  - Reassemble shares               │    │
│   │  - Run classifier (PDQ + small CNN)│    │
│   │  - Sign attestation of result     │    │
│   │  - Return Boolean                  │    │
│   │                                     │    │
│   │  (Plaintext never leaves enclave)  │    │
│   └───────────────────────────────────┘     │
└─────────────────────────────────────────────┘
```

The moderator's host OS sees: input shares (ciphertext), output Boolean ("flagged" / "not flagged"), and a signed attestation from the TEE that this is the output of the approved classifier code. The plaintext never traverses the TEE boundary to the host.

### Mode B: Ephemeral render (default, works everywhere)

When TEE is unavailable, moderators run the same no-auto-download and RAM-only rendering pipeline as ordinary users, but with a different UI context. The moderator opens the flagged item, the client reassembles it in locked memory, runs the PDQ hash check, and renders.

The moderator then makes a decision (flag / allow) and the content is purged. The moderator's device has the same exposure as any user who views that content once, which is lower than continuous auto-caching but not zero.

### Mode C: Community moderation via group vote

For groups where the moderator role is distributed, a vote-based mechanism allows multiple moderators to each view the content once and vote flag/allow. A majority-vote flag triggers the same propagation as a unilateral moderator flag.

This mode distributes the exposure across multiple moderators rather than concentrating it on one, which is useful when no single trusted moderator wishes to take the risk.

## 12.4 Classifier implementation

The classifier deployed in Mode A is a small convolutional neural network trained to identify CSAM. We do not train this model ourselves; instead, we integrate existing published models:

- **Meta's PDQ hash** (not a classifier, but deterministic hash matching against known content)
- **Thorn's Safer** (commercial, restricted availability)
- **Google's CSAI Match** (limited availability to vetted partners)

The baseline deployment uses PDQ hashing only, with a classifier tier as Phase 3 when integration agreements with NCMEC and IWF are complete. The classifier tier is necessary to detect *novel* CSAM (not previously hashed), which is an important complement to known-hash matching.

## 12.5 Attestation protocol

For Mode A, the TEE returns a signed attestation of the classification result:

```
ClassificationAttestation ::= SEQUENCE {
  version         INTEGER (1),
  tee_platform    ENUMERATED {trustzone, sgx, sev, titan, ...},
  enclave_hash    OCTET STRING,           -- MRENCLAVE or equivalent
  input_hash      OCTET STRING (SIZE 32), -- BLAKE3 of reassembled plaintext
  result          BOOLEAN,                 -- true = flagged
  confidence      REAL,                    -- 0.0 to 1.0
  classifier_ver  INTEGER,
  timestamp       INTEGER,
  tee_signature   OCTET STRING
}
```

Upon receipt, the client verifies:
- The `tee_signature` is valid under the published TEE platform attestation key (Intel IAS, Google Titan attestation, etc.).
- The `enclave_hash` matches the approved build hash published by the GoNode Foundation.
- The `classifier_ver` is current.

The client uses the `result` to act (block content, propagate flag) without ever seeing the plaintext.

## 12.6 Flag propagation

When a moderator flags content:

1. The moderator's client issues a signed `ContentFlag`:

```
ContentFlag ::= SEQUENCE {
  file_hash       OCTET STRING,
  group_id        OCTET STRING,
  flag_reason     VisibleString,          -- "CSAM", "spam", "off-topic", etc.
  attestation     ClassificationAttestation OPTIONAL,
  moderator_sig   OCTET STRING
}
```

2. The flag is distributed to all group members via the SMP channel.

3. Recipient clients apply the flag:
   - Future fetch requests for this file return "blocked" status.
   - Already-fetched (but not persistently cached) content is purged from in-memory caches.
   - UI shows "content blocked by moderator" placeholder.

4. Operators holding shares of the flagged content can optionally refuse future share serving (governed by per-operator policy and jurisdiction).

## 12.7 Accountability and appeal

Moderator flags are signed and logged to a per-group moderation log. Users whose content was flagged can appeal via:

- Direct appeal to the group owner
- Cross-posting to a moderation-review group
- (For Foundation-operated groups) appeal to the Foundation's moderation review

The moderation log is a transparent record that preserves user agency.

## 12.8 Legal defensibility of the moderation approach

Several features of this approach are specifically chosen to satisfy DSA and national-law requirements:

- **DSA Article 16 notice-and-action:** The flag protocol is a notice mechanism that can be invoked by any user.
- **DSA Article 14 terms of service:** Group rules are expressible in the group metadata and enforced by moderator flags.
- **DSA Article 18 notification of criminal offences:** Moderators who flag CSAM can also invoke a separate channel for notification to competent authorities (NCMEC CyberTipline via the Foundation's NCMEC liaison, BKA via ZAC NRW if in Germany).
- **§184b StGB compliance for moderators:** TEE-based classification means the moderator's device never holds the CSAM in plaintext form recoverable post-session. Mode B (ephemeral render) is a meaningful improvement over current practice but is not legally equivalent to Mode A; we counsel moderators operating in strict-liability jurisdictions to prefer Mode A where available.

---

# 13. Hash Matching Against Known-Bad Content

Before any plaintext is rendered to the user, it is hashed and compared against a known-bad list. This section specifies the list structure, distribution, and comparison protocol.

## 13.1 Hash function selection

We use PDQ hash [Davis 2019, Meta ThreatExchange] as the primary perceptual hash. Rationale repeated from Section 7.7: PDQ is open-source, has a published specification, is accepted by NCMEC, and has a mature reference implementation in C++ at github.com/facebook/ThreatExchange.

For video content, we use PDQF (PDQ-Frame), which extends PDQ to video by hashing frames at a consistent sampling rate. Alternative is TMK+PDQF (Temporal Match Kernel + PDQ Frame) [Douze et al., "TMK + PDQF - A TEST-WHO-IS-WHO Comparison for Video Copy Detection Evaluation," 2017].

## 13.2 Known-bad list sourcing

The known-bad list is compiled from:

- **NCMEC CyberTipline** hashes provided to NCMEC's industry partners. Access requires a partner agreement; the Foundation obtains such an agreement as a Phase 1 prerequisite.
- **Internet Watch Foundation (IWF)** hashes. UK-based nonprofit clearinghouse. Similar partnership model to NCMEC.
- **Bundeskriminalamt (BKA) Zentralstelle für anlassunabhängige Recherche in Datennetzen (ZaRD)** hashes for German-specific content. Access requires coordination with ZaRD in Wiesbaden.
- **Thorn's Safer** hash list, if commercial partnership is feasible.
- **Project Arachnid** (Canadian Centre for Child Protection) hashes.

These hash sources overlap substantially. A typical deployment integrates NCMEC + IWF as the minimum baseline.

## 13.3 List distribution

The combined hash list is published by the Hash List Committee (Section 8.2.4) as a Merkle tree of hash entries, signed by a 4-of-4 multisig:

```
HashListUpdate ::= SEQUENCE {
  version                INTEGER,
  epoch                  INTEGER,          -- monotonically increasing
  merkle_root            OCTET STRING (SIZE 32),  -- BLAKE3 of tree
  total_entries          INTEGER,
  new_entries            SEQUENCE OF HashEntry,
  revoked_entries        SEQUENCE OF HashEntry OPTIONAL,
  committee_sigs         SEQUENCE OF OCTET STRING  -- 4 Ed25519 sigs
}

HashEntry ::= SEQUENCE {
  hash_type              ENUMERATED {pdq, pdqf, sha256, ...},
  hash_value             OCTET STRING,
  source                 VisibleString,    -- "NCMEC", "IWF", etc.
  added_epoch            INTEGER
}
```

Clients download full list on first run and delta updates thereafter. Distribution is via the same operator network (shares of the list are distributed and fetched like any other file) or via direct download over Tor.

## 13.4 Client-side comparison

On plaintext reassembly, before render, the client computes the PDQ hash and compares:

```
input_hash := PDQ.compute(plaintext)
match := false
for each entry in known_bad_list:
  if entry.hash_type == pdq:
    distance := HammingDistance(input_hash, entry.hash_value)
    if distance < threshold (e.g. 90 out of 256):
      match := true
      break
```

For a list of 100,000 entries, this is 100,000 × 32 = 3.2 MB of comparison per input; on modern CPUs this completes in 5-20 ms with vectorised Hamming distance implementations (POPCNT on x86, VCNT on ARM).

## 13.5 Constant-time comparison for privacy

The simple loop above leaks, via timing, which entry matched. While the match fact itself is what matters, an operator observing fetch-then-no-render patterns could potentially correlate with hash list entries to infer which known-bad content a user is receiving.

We therefore implement comparison as strictly constant-time:

```c
uint32_t min_distance = UINT32_MAX;
for (size_t i = 0; i < list_size; i++) {
  uint32_t d = hamming_distance_constant_time(input_hash, list[i].hash_value);
  min_distance = (d < min_distance) ? d : min_distance;
  // alternatively use bitmask-based cmov to avoid branch
}
bool match = (min_distance < threshold);
```

The matching entry index is not retained; only the Boolean `match` is retained.

## 13.6 Match outcome

If `match == true`:

1. The plaintext buffer is immediately zeroed via `explicit_bzero` before any further processing.
2. A render-abort is signaled to the UI layer. User sees: "Content blocked. This item matched a known-bad content database."
3. A report is generated containing:
   - The file_hash (operators see this during fetch; not new information)
   - The group_id and sender_pubkey
   - The matched list source (NCMEC / IWF / etc.)
   - The user's decision to report or suppress
4. If the user chooses to report, the report is sent to the group owner for moderation action and optionally to the Foundation's NCMEC liaison for CyberTipline submission.

The report never contains the plaintext or its hash beyond the match indication.

## 13.7 False positive handling

PDQ is a perceptual hash, not a cryptographic hash. False positives occur. If the user believes the match is false:

- They can appeal to the group owner.
- They can review the blocked content by explicitly temporarily disabling the hash check (locally, with UI warning about legal risk).
- They can report the false positive to the Foundation for review.

False positives are governance-handled, not technically prevented. The list committee has a process for investigating reported false positives and issuing revocations via `revoked_entries` in the next epoch.

## 13.8 Hash list transparency

The hash list commits publicly to:

- The list source (NCMEC / IWF / etc.).
- The epoch of each entry.
- The Merkle root, which permits any party to verify that a specific hash is in the current list.

What is not public:

- The hash values themselves (these are confidential per NCMEC and IWF agreements; publishing them would enable evasion).

This is an inherent tension. The committee publishes aggregate statistics (total entries, per-source counts, per-epoch add/revoke rates) and is subject to annual independent audit.

## 13.9 Limits of the approach

The honest limits:

- **Novel CSAM evades PDQ.** Content not previously hashed is not matched. This is why Mode A TEE classifier (Section 12.4) is the Phase 3 complement.
- **Minor perturbations beyond PDQ threshold evade.** Sophisticated offenders can craft perturbations that push PDQ distance above the match threshold while keeping the content visually recognisable. This is an arms race; PDQ has been resilient to naive transformations but falls to deliberate adversarial perturbation.
- **The list is only as complete as its contributors.** NCMEC and IWF between them cover the substantial majority of known CSAM but are not exhaustive.

The approach is therefore not a complete solution. It is the best available first line of defence. Combined with the no-auto-download default (Section 11), it raises the bar substantially against both opportunistic and targeted threats.

---

*End of Part 3 of 5. Continues in Part 4 with economic model, legal compliance strategy, and comparison matrix.*

# 14. Economic Model: Stake-Based Operator Participation Without Tokens

This section specifies the economic model of the GoNode operator network. We state at the outset our central design decision: **GoNode does not issue a native token**. This is a deliberate departure from Storj (STORJ, ERC-20), Sia (Siacoin, native chain), Filecoin (FIL), Session (SESH, formerly OXEN), and every other major decentralized-storage project we are aware of. Section 14.1 explains why.

## 14.1 Why no native token

The architecture of GoNode is financially unremarkable: operators provide storage and bandwidth, clients pay for storage and bandwidth, there is no capital appreciation or speculative demand intrinsic to the protocol. Any token model would therefore be a design addition rather than a necessity. We enumerate three reasons to refrain.

**Reason 1: MiCA exposure.** Regulation (EU) 2023/1114 (Markets in Crypto-Assets) became fully applicable on 30 December 2024. Article 3(1)(5) defines a "crypto-asset" as "a digital representation of a value or of a right that is able to be transferred and stored electronically using distributed ledger technology or similar technology." Articles 16-47 impose obligations on issuers of asset-referenced tokens and e-money tokens; Articles 48-63 impose obligations on issuers of other crypto-assets ("utility tokens" in common parlance); Articles 59-77 impose obligations on crypto-asset service providers. The obligations include prospectus publication, white-paper filing with competent authorities, capital requirements, custody requirements, market-abuse prohibitions, and supervisory fees.

For a small operator network in its first years of operation, compliance cost is disproportionate. For a German-based issuer specifically, the competent authority is the BaFin (Bundesanstalt für Finanzdienstleistungsaufsicht), whose authorisation processes are not fast. Issuing a native GoNode token would consume engineering capacity that is better spent on the architecture itself.

**Reason 2: Operational simplicity.** A stake-based, EUR-denominated model is fully self-explanatory: operators post a bond in EUR stablecoin, earn EUR stablecoin for work performed, lose part of the bond if they misbehave. There is no tokenomics to explain, no price discovery, no market maker, no volatility hedging required by operators. A new operator can onboard by buying EURC on a regulated exchange and posting stake to the contract.

**Reason 3: Alignment of incentives with reliability, not speculation.** Projects with native tokens develop a constituency that is invested in token price appreciation rather than in protocol utility. This creates pressure for governance decisions that boost token metrics (burn mechanics, staking lockups with yield subsidies, foundation treasury deployment into price support) at the expense of protocol users. GoNode operators are paid for actual storage and bandwidth consumed; their incentive is to serve clients efficiently, and there is no speculative overhang.

## 14.2 Stake mechanics

Operators post a EUR-denominated stake to the `OperatorRegistry` smart contract on Arbitrum One. Stakes are held in EURC (Euro Coin, issued by Circle Internet Financial under its French EMI authorisation by the ACPR).

Minimum stake for a new operator: **10,000 EURC** (approximately 10,000 EUR). Higher stakes confer proportionally higher selection probability in the ECVRF operator selection and higher job throughput capacity.

Stakes are locked for a minimum of 90 days from posting. Unstaking requires a 30-day cooldown period during which the operator must continue honouring audits. If the operator fails audits during cooldown, the stake remains locked and slashable.

Stake is released back to the operator after:
- The 90-day minimum lock has elapsed.
- The 30-day cooldown has elapsed.
- No outstanding slashing claims exist against the operator.
- The operator's last-served shares have all expired or been repaired elsewhere.

## 14.3 Payment for service

Clients pay for upload and retrieval via signed credits:

```
Credit ::= SEQUENCE {
  version         INTEGER,
  issuer_sig      OCTET STRING,
  expiry_epoch    INTEGER,
  credit_value    INTEGER,                 -- denominated in EURC wei
  operator_pubkey OCTET STRING,            -- specific operator the credit is for
  nonce           OCTET STRING (SIZE 16)
}
```

Credits are issued by the client's payment processor (the `PaymentGateway` contract) against EURC deposits. When an operator serves an upload or retrieval, they claim the credit and the smart contract transfers the corresponding EURC from the gateway to the operator.

**Pricing baseline (indicative, subject to governance):**

- Storage: 0.01 EURC per GB per month
- Bandwidth (upload): 0.005 EURC per GB
- Bandwidth (retrieval): 0.01 EURC per GB

These prices approximate Storj's market pricing as of April 2026 and produce reasonable margins for operators running on commodity hardware (typical cost basis: 0.003-0.005 EURC per GB-month for storage on a home server with gigabit uplink).

For a typical messenger user with 500 MB of media per month:
- Upload cost: 500 MB × 0.005 EURC/GB × 1.67 (erasure overhead) ≈ 0.004 EURC
- Storage cost (assuming 1-year retention): 500 MB × 0.01 EURC/GB-month × 12 × 1.67 ≈ 0.10 EURC per year
- Retrieval cost (assuming 2x average retrieval): 1 GB × 0.01 EURC/GB ≈ 0.01 EURC per month

Annual cost per user: approximately 0.25 EURC, or 25 euro cents per year. This is recoverable from voluntary donations, Foundation subsidy, or a modest subscription tier. Commercial-scale SimpleGoX deployments for business customers would charge correspondingly more for higher retention and throughput.

## 14.4 Slashing conditions

The smart contract defines the following slashing conditions:

| Offence | Slash fraction | Trigger |
|:--------|:---------------|:--------|
| Failed audit challenge (single) | 0 (warning) | First miss in 7-day window |
| Failed audit challenge (repeated) | 1% of stake | 3 misses in 7 days |
| Proven share tampering | 20% of stake | Cryptographic proof of altered share |
| Proven share deletion before TTL | 30% of stake | Inability to respond to any audit during commitment period |
| Proven cooperation with an unauthorized share reconstruction | 100% of stake | Cryptographic evidence of share disclosure to non-authorised party |
| Operator offline exceeding 14 days | 10% of stake | No audit response, no liveness proof |

Slashing is executed by the smart contract upon submission of evidence. Evidence is cryptographically verifiable and does not require subjective judgement.

## 14.5 Distribution of slashed stake

Slashed stake is distributed:
- 30% to the repair operator(s) who restore the affected shares
- 20% to the report submitter (if externally reported)
- 40% to the protocol treasury (governed by the Foundation)
- 10% burned (sent to a non-recoverable address)

The 40% to treasury funds the Foundation operations (audits, development grants, committee compensation). Burn mechanic exists only to the extent that it reduces total EURC in circulation within the protocol, which has no effect on EURC's value (EURC is externally redeemable 1:1 for EUR regardless of protocol activity); it is included for symbolic cost rather than for tokenomic reasons.

## 14.6 Governance model

The Foundation structure is being constituted as a German Genossenschaft (eG) or alternatively an e.V. (eingetragener Verein), with operator members and a board elected by members. Governance operates on a one-operator-one-vote basis for most decisions, with stake-weighted votes reserved for economic parameter changes.

**Decisions subject to governance vote:**

- Pricing parameter adjustments (storage, bandwidth)
- Slashing rate adjustments
- Hash list committee composition changes
- Foundation treasury allocation
- Smart contract upgrades (only during Phase 0-3; after Phase 4 contracts are immutable)

**Decisions not subject to governance:**

- Cryptographic protocol specifications (subject to protocol RFC process with implementer review)
- Adding new operator jurisdictions (automatic upon stake posting)
- Individual slashing events (executed deterministically by contract)

The Foundation explicitly does not hold a veto over individual operators' participation.

## 14.7 Comparison with token-based projects

| Property | Storj | Filecoin | Session | DCD |
|:---------|:------|:---------|:--------|:----|
| Native token | STORJ | FIL | SESH | None |
| MiCA status (EU) | Likely "other crypto-asset" | Likely "other crypto-asset" | Likely "other crypto-asset" | Not applicable |
| Primary payment | STORJ (bridged to USDC) | FIL | SESH | EURC |
| Operator capital lockup | STORJ (volatile) | FIL (volatile) | SESH (volatile) | EURC (EUR-pegged) |
| Speculative demand | Yes | Yes | Yes | No |
| Staking yield subsidy | From token emissions | From token emissions | From token emissions | None |
| Registration jurisdiction | Delaware LLC | Delaware LLC | Lichtenstein Stiftung | Germany eG/eV |
| Regulatory strategy | Limited EU engagement | Limited EU engagement | Limited EU engagement | Proactive DE/EU compliance |

The absence of speculative demand is a feature. The operator's decision to run a node is based on whether they can profitably serve users, not on whether the token might appreciate. This produces a more stable long-term operator base.

## 14.8 Long-term sustainability

The economic model is sustainable if and only if:

```
User payments ≥ Operator costs + Foundation overhead + Replacement rate
```

At the indicative pricing above, this is satisfied with reasonable assumptions. The Foundation's operating budget (estimated 500,000 to 2,000,000 EUR per year depending on phase) is covered by:

- Treasury share of slashed stake (variable)
- Service fees on SimpleGoX Business tier (fixed subscription for business customers)
- Grants from civil society organisations (Mozilla, NLnet, OpenTech Fund, Prototype Fund)
- Optional operator surcharge (e.g. 2% of operator revenue to Foundation, voted by operators)

No component depends on token price appreciation or speculation. If SimpleGoX adoption grows, Foundation revenue grows proportionally via the Business tier; if adoption stagnates, costs also stagnate. There is no tokenomic pressure to subsidise user growth via token emissions.

---

# 15. Legal Compliance Strategy

This section walks jurisdiction by jurisdiction through the legal posture that DCD adopts. We state up front what this section is and is not: this is a design argument by the authors, grounded in primary legal sources. It is not legal advice. Before Phase 1 launch, the Foundation will obtain formal legal opinions from German and EU counsel; those opinions will supersede any positions taken here where they differ.

## 15.1 Germany

### 15.1.1 §184b StGB compliance posture

The core argument: the combined effect of the no-auto-download default and the hash-match pre-render filter is that DCD-compliant clients materially reduce the probability of §184b (3) triggering on any user's device. The user does not "undertake to retrieve" ("abrufen") or "obtain possession" ("sich den Besitz verschaffen") of child pornographic content because:

1. **No passive retrieval occurs.** Other messengers auto-fetch media on roster change or message receipt. In DCD, no fetch occurs without explicit user action (Sections 9.4, 11.1).

2. **Deliberate retrieval is filtered.** If a user explicitly requests fetch (taps a silhouette or placeholder), the PDQ hash filter runs before render (Section 13). Content matching the known-bad list is blocked at reassembly time and purged from RAM; it never reaches the rendering surface or persistent storage.

3. **Even if filtering is evaded, no persistent possession results.** Content that passes the hash filter is rendered in locked memory and purged on dismissal (Section 11.4). Unless the user explicitly confirms the contact and enables persistent caching (a double opt-in), no disk write occurs.

The user's position becomes: "I never chose to receive this content, I did not pre-fetch it, my client never had it on disk, I ran the known-bad filter before rendering, and when I realised what it was I reported it." This is a materially stronger defensive posture than any current messenger permits.

§184b (3) requires the offence: "es unternimmt, einen kinderpornographischen Inhalt ... abzurufen oder sich den Besitz an einem solchen Inhalt zu verschaffen." ("undertakes to retrieve child pornographic content or to obtain possession of such content"). The verb "unternimmt" requires deliberate action ("Tathandlung"). DCD architecturally ensures that no action producing retrieval occurs without explicit user consent, and that explicit user consent is filtered before it produces actual possession.

### 15.1.2 Operator posture under §184b StGB

Individual GoNode operators hold, at any moment, at most one of five encrypted shares of a file. No operator can reconstruct the plaintext without cooperation of two additional operators plus the master key held by the recipients. We argue the operator has no "Besitz" (possession) of kinderpornographischer Inhalt because:

1. The share on the operator is encrypted ciphertext, not an image. The content of the file is not present on the operator's system in any form recognisable as kinderpornographischer Inhalt.

2. Reconstruction is cryptographically impossible without cooperation of other parties.

3. The operator lacks the cognitive ability to know, from inspection of a single encrypted share, what the content is.

This position is analogous to the established treatment of encrypted email relays and of TLS-terminating CDN nodes under German and EU law: a party that transmits or stores ciphertext it cannot read is not a "Besitzer" of the plaintext. The position is further supported by the DSA's "mere conduit" liability exemption (see 15.2).

### 15.1.3 §202a StGB: Data protection as defensive architecture

§202a StGB protects data that is "besonders gegen unberechtigten Zugang gesichert" (specially secured against unauthorised access). DCD's shares are protected by XChaCha20-Poly1305 AEAD with 256-bit keys, distributed such that no single party can reconstruct without at least three of five cooperating. This clearly satisfies "besonders gesichert" and means:

- An operator who deliberately discloses shares to a non-authorised party commits an offence under §202a or §202b.
- A third party (e.g. a state actor) who coerces operators into cooperative reconstruction may face §202a exposure depending on lawful-authority colour.
- The user's shares are themselves data of the user, protected by §202a; unauthorised access is criminally prosecutable.

This is a useful legal framework because it positions the user as a "Rechtsinhaber" (rights-holder) whose data is protected, rather than as a potential suspect.

### 15.1.4 §206 StGB: Fernmeldegeheimnis

§206 StGB protects the secrecy of communications provided by telecommunications services. Operators who disclose communications data (even routing and timing metadata) face criminal liability. The provision is directly applicable to GoNode operators to the extent they qualify as telecommunications service providers under §3 No. 61 TKG.

Whether GoNode operators so qualify is a nontrivial question. The Federal Network Agency (BNetzA) has indicated in published guidance that operators of federated infrastructure (e.g. Matrix homeservers, XMPP servers) may or may not qualify depending on their relationship to the end-user; the traditional "Telekommunikationsdienst" categorisation was extended in 2021 to include "nummernunabhängige interpersonelle Telekommunikationsdienste" but whether pure-infrastructure operators (who do not have a direct user relationship) are captured is unsettled.

The Foundation will seek BNetzA guidance for the GoNode operator model specifically. In the interim, operators are advised to treat §206 as applicable conservatively, which in practice means the same privacy posture that the architecture already mandates.

### 15.1.5 TKG and TKÜV: Interception obligations

Under §170 TKG in conjunction with §3 TKÜV, providers of publicly available telecommunications services with more than 10,000 participants must implement technical interception capabilities per the TKÜV. For GoNode, the question is whether the operator network as a whole has 10,000 participants or whether each operator counts separately.

Our position: each operator is an independent service provider; the network is a coordination protocol, not a single service. This interpretation is supported by the decentralised architecture (no single entity can intercept across the network because of the threshold design). Individual operators with fewer than 10,000 participants do not face §170 TKG obligations.

If this interpretation is rejected by BNetzA, the fallback is that the network architecture itself makes compliance impossible: no single operator can intercept any given file without colluding with at least two others, and the cryptographic threshold design is not a matter of policy that can be waived. We argue this is analogous to end-to-end encryption, which has been repeatedly defended by German courts and by the Bundesverfassungsgericht as a legitimate architectural choice.

### 15.1.6 DDG (Digitale-Dienste-Gesetz)

The DDG implements the EU DSA into German national law. The intermediary liability privileges of DSA Articles 4-6 are directly applicable in Germany via the DDG. We address DSA compliance in the EU section (15.2).

### 15.1.7 GDPR Article 32: Technical and organisational measures

GDPR Article 32 requires "appropriate technical and organisational measures to ensure a level of security appropriate to the risk," including "(a) the pseudonymisation and encryption of personal data."

DCD satisfies Article 32 through:
- End-to-end encryption of all content (XChaCha20-Poly1305)
- Threshold distribution of ciphertext (3-of-5 Reed-Solomon)
- Threshold distribution of keys (3-of-5 Shamir)
- Device-level key management with hardware-backed keystores
- Opt-in rather than opt-out defaults (data minimisation per Article 25)

We argue that DCD is meaningfully more Article-32-compliant than the current industry default, which is to store plaintext (or trivially-decryptable ciphertext) on vendor-controlled servers without distribution. A DPIA (Data Protection Impact Assessment) for SimpleGoX with GoNode DCD will be published as a Phase 1 deliverable.

## 15.2 European Union

### 15.2.1 DSA Article 4 (Mere conduit)

For the SMP message-routing function (as distinct from file storage), GoNode operators satisfy the conditions of Article 4:

- They do not initiate the transmission (clients do).
- They do not select the receiver (the queue address determines routing; operators cannot read the queue association data because it is in SMP ephemeral keys).
- They do not select or modify the information (operators receive and forward ciphertext blobs whose contents they cannot decrypt).

The conditions in Article 4(2) are also satisfied: storage is "automatic, intermediate and transient," performed "for the sole purpose of carrying out the transmission," and "not stored for any period longer than is reasonably necessary."

### 15.2.2 DSA Article 5 (Caching)

Article 5 applies to caching services. The caching of shares by operators for the specified TTL is "automatic, intermediate and temporary storage ... performed for the sole purpose of making more efficient the information's onward transmission." Article 5 requires:

- No modification of the information: satisfied (AEAD tags detect modification).
- Compliance with access conditions: satisfied (fetch credits required).
- Compliance with rules on updating: satisfied (TTL expiry, deletion on request).
- No interference with technology used to obtain data on usage: satisfied (we do not interfere with audit metadata).
- Expeditious removal upon knowledge of source removal or court order: satisfied (deletion protocol, Section 10.6).

### 15.2.3 DSA Article 6 (Hosting)

For the share storage function, arguments under Article 6 apply. Article 6 requires that the provider:

- Does not have actual knowledge of illegal content.
- Upon obtaining knowledge, acts expeditiously.

Our position: an operator holding an encrypted share cannot have actual knowledge of illegal content because they cannot decrypt the share. Upon receiving a flag (via the moderation protocol, Section 12.6) or an external report identifying a specific file_hash as illegal, the operator can refuse to serve that share and can delete it. The deletion propagates across the 5 operators holding shares of the file; without any one share the file is partially unrecoverable, and with coordinated deletion the file is fully unrecoverable.

### 15.2.4 DSA Article 8 (No general monitoring)

Article 8 prohibits Member States from imposing general monitoring obligations. This protects GoNode operators from any Member-State demand to scan all stored shares. The architecture makes such scanning impossible in any case (shares are encrypted), so the Article 8 protection and the cryptographic protection coincide.

### 15.2.5 DSA Article 16 (Notice-and-action)

The DCD flag protocol (Section 12.6) implements a notice-and-action mechanism that allows any user to notify operators of content considered illegal. Upon receipt of a notice, operators are equipped to refuse future service of the identified file and to initiate deletion.

### 15.2.6 GDPR

DCD minimises personal data collection (no user identifiers beyond public keys, no telemetry), implements strong encryption (Article 32), and uses data protection by design and by default (Article 25). Processing bases under Article 6 are consent (for user actions) and legitimate interest (for operator service provision). Article 9 special-category data protections apply to any content that is biometric or concerns sex life; DCD's architecture ensures such data is never held in a form recoverable by any single party.

### 15.2.7 MiCA (addressed in Section 14)

Deliberate avoidance of MiCA's scope by operating without a native token. EURC usage is MiCA-compliant (Circle is an authorised EMI).

## 15.3 United States

### 15.3.1 Section 230

47 U.S.C. §230(c)(1) provides that "no provider or user of an interactive computer service shall be treated as the publisher or speaker of any information provided by another information content provider." GoNode operators, acting as infrastructure that transmits and stores content provided by users, fall within the "interactive computer service" definition in §230(f)(2) and are protected from being treated as the publisher.

§230(c)(2)(A) additionally provides Good Samaritan protection for "action voluntarily taken in good faith to restrict access to or availability of material that the provider or user considers to be obscene, lewd, lascivious, filthy, excessively violent, harassing, or otherwise objectionable." Operators who refuse to serve flagged content are acting within this protection.

### 15.3.2 18 U.S.C. §2258A (NCMEC reporting)

§2258A imposes reporting obligations on "electronic communication service providers" and "remote computing service providers" who obtain "actual knowledge" of apparent §2252 violations.

GoNode operators holding only encrypted shares cannot obtain actual knowledge of content. The Foundation, which integrates hash list signals and may receive user reports, can and will obtain actual knowledge when users report flagged content. The Foundation's NCMEC liaison handles CyberTipline submissions on behalf of the network.

The statutory immunity grants in §2258B apply to the Foundation's voluntary good-faith reporting.

### 15.3.3 First Amendment considerations

The First Amendment does not protect CSAM (New York v. Ferber, 458 U.S. 747 (1982); Ashcroft v. Free Speech Coalition, 535 U.S. 234 (2002) regarding virtual CSAM). DCD's filtering of known CSAM is constitutionally unproblematic. The First Amendment does protect private communications among consenting adults, which DCD is designed to enable; the known-bad filter does not scan lawful communications.

### 15.3.4 State-law CSAM possession offences

State laws parallel 18 U.S.C. §2252A with varying specifics. The architecture is equally defensive in state contexts.

## 15.4 United Kingdom

### 15.4.1 Online Safety Act 2023, Section 122

Section 122 empowers Ofcom to issue technology notices requiring "accredited technology" for CSAM and terrorism-related content identification. As of April 2026, no Section 122 notice has been issued against an E2EE provider, and the UK government has provided assurances that such notices will not be issued until technically feasible.

DCD's hash-matching architecture, executed on the client device before render, would satisfy the spirit of Section 122 without requiring provider-side scanning. If required, the hash list could be extended to incorporate terrorism-related content per UK Home Office designations.

### 15.4.2 Protection of Children Act 1978 and CJA 1988 Section 160

Parallel provisions to §184b StGB. The architectural defence is the same: no auto-download, pre-render filtering, no disk persistence for unconfirmed contacts.

## 15.5 Compliance matrix

| Provision | Requirement | DCD compliance |
|:----------|:-----------|:---------------|
| §184b StGB | No possession of CSAM | No auto-download + pre-render filter + ephemeral render |
| §202a StGB | Protect against unauthorised access | Threshold encryption + hardware keystores |
| §206 StGB | Fernmeldegeheimnis | No operator observes plaintext or persistent metadata |
| TKG §170 | Interception for >10k participants | Architectural impossibility |
| DSA Art. 4 (conduit) | No initiation, selection, modification | Satisfied by design |
| DSA Art. 5 (caching) | Automatic, intermediate, temporary | Satisfied by TTL-bounded share storage |
| DSA Art. 6 (hosting) | No actual knowledge, expeditious removal | Satisfied by encrypted storage + flag protocol |
| DSA Art. 8 | No general monitoring | Architectural impossibility |
| DSA Art. 16 | Notice-and-action | Implemented via flag protocol |
| DSA Art. 18 | Criminal offence notification | Foundation NCMEC liaison |
| GDPR Art. 25 | Data protection by default | No-auto-download default |
| GDPR Art. 32 | TOM: encryption and pseudonymisation | Threshold crypto + pubkey identifiers |
| 47 U.S.C. §230 | Intermediary protection | Satisfied |
| 18 U.S.C. §2258A | NCMEC reporting on actual knowledge | Foundation handles |
| UK OSA s.122 | Accredited tech for CSAM identification | Satisfied by client-side PDQ |

## 15.6 Open legal questions

The following questions remain open and will be addressed in the Foundation's legal opinion process:

1. **Whether GoNode operators qualify as "Telekommunikationsdienst" under §3 No. 61 TKG** (affects §206 applicability and §170 obligations).
2. **Whether the Shamir-distributed master key constitutes "possession" of the key by any individual recipient** (relevant to §184b posture where the recipient is the addressee of CSAM).
3. **Whether DSA Art. 18 reporting obligations attach to the Foundation, operators, or both** in cases where user reports reach the Foundation's NCMEC liaison.
4. **Whether the known-bad hash list constitutes "personal data" under GDPR** (the list itself is purely hash values, but unauthorised access could theoretically be combined with image databases to identify individuals depicted; this is a fringe case).
5. **Whether EURC custody by the stake contract constitutes "custody services" under MiCA Article 75** (we believe not because the contract is non-custodial in the traditional sense, but the question is untested).

Legal opinions will be obtained and published as part of the Foundation's transparency commitments.

---

# 16. Comparison Matrix: DCD vs Existing Messengers

This section returns to the thirteen messengers surveyed in Section 3 and compares each against DCD across ten evaluation criteria.

## 16.1 Evaluation criteria

- **C1:** Profile picture auto-fetch on group join (lower is better for our threat model)
- **C2:** Media auto-download for unconfirmed contacts (lower is better)
- **C3:** Persistent disk cache for unconfirmed contacts (lower is better)
- **C4:** Pre-render hash filtering against known-bad content
- **C5:** Storage architecture (centralised, federated, decentralised, P2P)
- **C6:** Whether any single server/operator can reconstruct user content
- **C7:** E2EE in direct messages (by default)
- **C8:** E2EE in group messages (by default)
- **C9:** Post-quantum key agreement
- **C10:** CSAM-pretextual-planting resistance (composite score)

## 16.2 Comparison table

Legend for C10: ★☆☆☆☆ = very poor, ★★☆☆☆ = poor, ★★★☆☆ = moderate, ★★★★☆ = good, ★★★★★ = strong

| System | C1 | C2 | C3 | C4 | C5 | C6 | C7 | C8 | C9 | C10 |
|:-------|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| SimpleX | Auto | Auto (size threshold) | Yes | No | Federated | Yes (single server holds ciphertext with keys on routing) | Yes | Yes | Planned | ★★☆☆☆ |
| Signal | Auto | Auto on Wi-Fi | Yes | No | Centralised | Yes (Signal servers with sealed sender caveat) | Yes | Yes | Yes (PQXDH) | ★☆☆☆☆ |
| WhatsApp | Auto | Auto on Wi-Fi | Yes | Server-side (pre-encryption?) | Centralised | Yes | Yes | Yes | Yes | ★☆☆☆☆ |
| Matrix/Element | Auto | Thumbnails auto | Yes | No | Federated | Yes (homeserver) | Yes | Yes (MegOlm) | No | ★☆☆☆☆ |
| Telegram | Auto | Auto | Yes | Server-side | Centralised | Yes | Opt-in only | No | No | ★☆☆☆☆ |
| Session | Auto | Auto | Yes | No | Service nodes | Yes (single service node) | Yes | Yes | No | ★★☆☆☆ |
| Briar | N/A (peer online) | Peer-dependent | Yes on receipt | No | P2P | N/A | Yes | Yes | No | ★★★☆☆ |
| Threema | Auto | Auto | Yes | No | Centralised | Yes | Yes | Yes | No | ★☆☆☆☆ |
| Delta Chat | Auto (Autocrypt) | Via IMAP | Yes (email) | No | Email | Yes (mail server) | Opt-in (Autocrypt) | Opt-in | No | ★☆☆☆☆ |
| Wire | Auto | Auto | Yes | No | Centralised | Yes | Yes | Yes (Proteus) | No | ★☆☆☆☆ |
| Conversations (XMPP) | Auto | Auto (threshold) | Yes | No | Federated | Yes | Yes (OMEMO) | Yes (OMEMO) | No | ★☆☆☆☆ |
| Keybase | Auto | Auto | Yes | No | Centralised | Yes | Yes | Yes | No | ★☆☆☆☆ |
| Discord | Auto | Auto | Yes | Server-side (PhotoDNA) | Centralised | Yes (fully cleartext) | No | No | No | ★☆☆☆☆ |
| **SimpleGoX + GoNode DCD** | **None (silhouette)** | **None** | **None for unconfirmed** | **Yes (client-side PDQ)** | **Decentralised (3,5 threshold)** | **No** | **Yes** | **Yes (MegOlm-equivalent)** | **Yes (ML-KEM-768 hybrid)** | **★★★★★** |

## 16.3 Analysis

Three observations stand out.

**First, the "C1 through C3" columns reveal that every mainstream messenger in 2026, with the narrow exception of Briar (which is P2P and therefore has its own limitations), defaults to auto-fetching at least profile pictures and typically other media. This is the central shared failure mode that DCD addresses.**

**Second, the "C6" column shows that every mainstream messenger has at least one party (usually a centralised vendor) that can reconstruct user content if compelled or compromised.** Signal's sealed sender reduces the metadata this party sees but not the content; Signal Messenger LLC retains the ability to see encrypted content and, in principle, the ability to modify or withhold it. SimpleX's federated design distributes this across operators but each operator still holds reconstructible-with-key-delivery data. Only a (k,n) threshold design like DCD's distributes this across multiple operators such that no single party can reconstruct.

**Third, the "C10" composite column attempts to rate each system's resistance to the CSAM-pretextual-planting threat model specifically.** Most mainstream messengers score one star because they combine auto-fetch, disk persistence, and no hash filter; an attacker who knows the target's identifier can plant CSAM and be assured it lands on disk. Briar scores three stars because its peer-online requirement means planting requires the attacker to be online and the target to open the chat, which gates the attack somewhat. DCD scores five stars because the no-auto-download default prevents passive landing, the pre-render filter blocks known-bad content even on deliberate fetch, the RAM-only render prevents disk persistence, and the threshold storage prevents any single operator from being compelled to assist the attack.

## 16.4 Relative performance costs

The DCD architecture imposes costs relative to naive implementations:

| Dimension | Cost vs. centralised baseline | Notes |
|:----------|:-----------------------------|:------|
| First-view latency for a media item | +1-3 seconds | Tor + 3-share fetch + reassembly + PDQ |
| Cumulative storage (network-wide) | +67% (due to erasure coding) | 1.67x overhead |
| Cumulative bandwidth for uploads | +67% | same reason |
| CPU for share encode/decode | Negligible | <10 ms per MB on commodity hardware |
| User experience for confirmed contacts | Comparable once opt-in is granted | Auto-fetch available per-contact |
| User experience for unconfirmed contacts | Different (silhouettes + explicit fetch) | Intentional departure |

The first-view latency is the most user-facing cost. For unconfirmed contacts this is an acceptable cost given the threat model reduction; for confirmed contacts, the per-contact opt-in brings latency back to approximately comparable to centralised baselines.

## 16.5 Conclusion of comparison

DCD's value proposition is not that it is the best at every dimension, but that it is the first system to genuinely address the auto-download threat model while maintaining most other properties that privacy-focused messenger users expect. Signal, SimpleX, and Matrix have excellent E2EE; DCD matches their E2EE. SimpleX has no persistent user identifiers; DCD inherits this from SimpleX's SMP foundation. Storj has mature erasure-coded storage; DCD borrows from Storj's design with confidentiality improvements. The composite is a system that is the best in the class for the specific threat we have documented to be pressing and unsolved.

---

*End of Part 4 of 5. Continues in Part 5 with implementation roadmap, open problems, conclusion, references, and appendices.*

# 17. Implementation Roadmap

This section maps the specification above to a concrete implementation plan, phased to reduce risk and allow incremental validation. The plan is scoped to the resources of a small team (IT and More Systems plus collaborators; estimated 2-4 full-time engineering equivalents) and leverages the existing SimpleGo Ecosystem infrastructure.

## 17.1 Phase 0: Specification and prototyping (months 0-3)

**Deliverables:**

- This whitepaper (v1.0 draft) for community review and public comment.
- Formal specifications of wire formats in CBOR (RFC 8949) with registered tags.
- Reference cryptographic implementations as Rust crates in the existing SimpleGoX repository:
  - `gonode-dcd-crypto`: XChaCha20-Poly1305 wrappers, HKDF, Ed25519, X25519, hybrid KEM with ML-KEM-768
  - `gonode-dcd-erasure`: (3,5) Reed-Solomon over GF(2^8) (wrapping klauspost/reedsolomon via FFI or using a pure-Rust port)
  - `gonode-dcd-shamir`: (3,5) Shamir secret sharing
  - `gonode-dcd-pdq`: PDQ hash computation in Rust (port of facebook/ThreatExchange C++ reference)
- Unit test coverage >= 90% for all cryptographic crates.
- Property-based testing via proptest / quickcheck for erasure-coding round-trip and Shamir reconstruction.

**Repository structure:**

```
github.com/saschadaemgen/GoNode/
├── docs/
│   ├── whitepaper/
│   │   └── dcd-v1.md              (this document)
│   ├── protocols/
│   │   ├── upload.md
│   │   ├── retrieval.md
│   │   ├── audit.md
│   │   └── wire-formats.md
│   └── threat-model/
├── crates/
│   ├── gonode-dcd-crypto/
│   ├── gonode-dcd-erasure/
│   ├── gonode-dcd-shamir/
│   ├── gonode-dcd-pdq/
│   ├── gonode-dcd-client/          (client library)
│   └── gonode-dcd-operator/        (operator daemon)
├── contracts/
│   ├── OperatorRegistry.sol
│   ├── StakingPool.sol
│   └── Slashing.sol
└── tools/
    ├── operator-cli/
    └── client-cli/
```

**Exit criteria:** All reference crates pass CI; whitepaper has completed one round of community review; at least two independent cryptographer reviews of the protocol specifications.

## 17.2 Phase 1: Alpha deployment (months 3-9)

**Deliverables:**

- Operator daemon (`gonode-dcd-operator`) running as a service node on the existing 10 SMP + 1 XFTP operators of the SimpleGo Ecosystem. Initial deployment over Tor v3 hidden services per existing operator topology.
- Client library (`gonode-dcd-client`) integrated into SimpleGoX Rust codebase as a feature-flagged module.
- SimpleGoX builds for Android (aarch64), Linux (x86_64, aarch64), and macOS (Apple Silicon) with DCD feature flag.
- Smart contract deployment on Arbitrum Sepolia testnet.
- Hash list committee formally constituted with founding members: NCMEC partnership application submitted, IWF partnership application submitted, GoNode Foundation member seated, independent civil-society member seated on rotating basis.
- Initial hash list populated from publicly available sources (NCMEC CyberTipline partner access pending; Project Arachnid public feeds; Hash Transparency Initiative if available).

**Alpha tester pool:**

- SimpleGo Ecosystem closed group members
- Collaborators (Cloudcoat, selected Privacy Guides contributors on invitation)
- Initial external testers recruited via Chaos Computer Club and CCC-adjacent channels
- Approximately 200-500 alpha testers

**Metrics tracked:**

- Upload/retrieval latency distributions
- Share availability (audit success rate)
- Operator uptime
- User-reported usability issues

**Exit criteria:** 30 consecutive days of stable operation with <1% audit failure rate; no unpatched security issues; smart contracts pass first-round audit.

## 17.3 Phase 2: Beta with public operator onboarding (months 9-15)

**Deliverables:**

- Smart contract audit completed (two independent firms).
- Public operator onboarding process launched (public documentation, minimum-stake EURC posting instructions, Tor v3 hidden service configuration guides).
- Target operator count: 30-50 by end of Phase 2, including operators in at least 5 distinct jurisdictions.
- iOS build of SimpleGoX with DCD (requires Apple Developer account and App Store review; this may be a TestFlight-only deliverable in Phase 2).
- ESP32 firmware build of SimpleGo with DCD client subset (for the user's existing LilyGo T-Deck Plus hardware target). Embedded constraints require simplified Shamir implementation and reduced erasure parameters for on-device storage; the embedded client participates as a reader but not as a moderator.
- Operator documentation including hardware recommendations (minimum specifications: 4 GB RAM, 1 TB storage, 100 Mbps uplink), jurisdiction declarations, and stake management.

**Beta user pool:**

- Approximately 5,000-20,000 users recruited from the broader privacy-tech community.

**Exit criteria:** Second cryptographic audit round complete; operator pool stable; user-reported issue rate trending downward.

## 17.4 Phase 3: Mainnet launch (months 15-24)

**Deliverables:**

- Smart contracts deployed to Arbitrum One mainnet.
- Public release of SimpleGoX with DCD enabled by default (feature flag flipped for new installations; upgrade path documented for existing users).
- Formal bug bounty programme operational (see SECURITY.md, Phase 2 onwards).
- Foundation legally constituted (German eG or e.V. with charter filed at local Amtsgericht in Recklinghausen or a chosen other venue).
- First annual transparency report published covering:
  - Hash list statistics (additions, revocations by epoch)
  - Moderation events (flags issued, files blocked)
  - Audit failures and slashing events
  - Financial report (EURC flows, Foundation treasury)
- Classifier integration (Mode A TEE classifier, Phase 3 priority): integration with NCMEC's Hash Sharing API using PDQ hashes; pilot deployment of TEE-based classifier on operators that offer moderation services.

**Launch criteria:** All prior audits clean; operator pool at target of 50+ across 5+ jurisdictions; documentation complete in English and German; integration tests passing across all supported platforms.

## 17.5 Phase 4: Maturity and immutability (months 24-36)

**Deliverables:**

- Smart contract upgrade mechanisms removed (contracts become immutable except for parameter changes under timelock).
- Multi-sig deployer keys burned (deposit to null address) to prevent any central party from re-deploying new contracts.
- Protocol specification reaches v1.0 frozen; subsequent changes require RFC process with operator approval.
- User base target: 100,000+ active users on SimpleGoX+DCD.
- Operator pool target: 100+ operators across 10+ jurisdictions.

**Post-Phase-4 operations:** Foundation continues operations under its charter. Protocol changes are rare and governed by RFC process. Hash list committee rotates members per schedule. Annual audits continue.

## 17.6 Risk factors and mitigations

| Risk | Probability | Mitigation |
|:-----|:-----------|:-----------|
| NCMEC partnership denied | Medium | Fall back to IWF + public sources; proceed without full NCMEC integration in Phase 1 |
| Smart contract audit finds critical issue | Medium | Timeline slippage 2-3 months; audit fund reserves in place |
| EU Chatkontrolle 2.0 enacted during roadmap | Medium | Architecture is robust to known versions of the proposal; contingency plans for geographically-restricted deployment |
| MiCA classification ambiguity for EURC | Low | EURC is clearly an e-money token under MiCA with a stated issuer; well-established |
| Key engineering departures | Medium | Cross-training, documentation in English, contracts in place for continuity |
| Apple App Store rejection | Medium | Prepare for TestFlight-only distribution; iOS may launch later |
| Tor network degradation | Low-Medium | Fallback to clear-net with TLS-only operation as emergency mode |

## 17.7 Parallel work streams

The phases above are organised by central deliverables, but parallel work streams proceed throughout:

- **Cryptographer review** (continuous): ongoing review of protocol specification and implementation by academic and industry cryptographers.
- **Legal consultation** (Phase 0-1): opinions from German, EU, and US counsel on the compliance positions in Section 15.
- **Usability research** (Phase 1-3): testing of the no-auto-download UX with typical users to refine silhouette rendering and explicit-fetch flows.
- **Integration testing** (ongoing): interoperability tests between SimpleGoX clients, operator daemons, and smart contracts.
- **Documentation localisation**: translations of key documentation into German, French, Spanish, Russian, Ukrainian, Belarusian, Farsi, and Arabic as community resources permit.

---

# 18. Open Problems and Future Work

This section states candidly the problems DCD does not solve, the residual risks that remain, and the directions for future research. A system that claims to solve all problems is a system that is lying; DCD is a meaningful improvement on current practice and has clear limits.

## 18.1 Residual risk: Threshold collusion

The (3,5) threshold is a probabilistic rather than information-theoretic protection against adversarial operator pools. If an adversary gains control of three or more of the five operators selected for a given file, they can reconstruct the ciphertext (though not the master key, which is protected separately by Shamir and KEM encryption to recipients).

**Why this is hard.** The ECVRF-driven selection is unbiasable by the uploader but not by the operator pool. If an adversary operates a sybil pool of many operators and the legitimate operator pool is small, the adversary can expect to control three or more of the five selected operators for a non-trivial fraction of uploads.

**Current mitigations:**
- Minimum stake requirement (10,000 EURC) raises the capital cost of sybil operation.
- Jurisdiction-diversity preference in selection.
- Slashing on provable misbehavior.

**Open work:** Research into non-sybil-resistant operator selection (anonymity-set-based selection, proof-of-space-and-time commitments that are harder to trivially replicate). We are tracking work on BLS12-381-based threshold signatures and multi-party computation primitives that may permit stronger selection guarantees at reasonable cost.

## 18.2 Residual risk: TEE fragmentation limits moderation

As discussed in Section 12, TEE availability for general-purpose classifier execution is limited on client mobile devices in 2026. Most moderators will operate in Mode B (ephemeral render) rather than Mode A (TEE-based classification), which means moderators still see the content they are moderating.

**Current mitigations:**
- Ephemeral render + locked memory + explicit_bzero reduces persistence.
- FLAG_SECURE prevents screenshot-class leaks.
- Moderator self-selection means only willing reviewers perform the role.

**Open work:** Improved TEE APIs from platform vendors (Google Titan remote attestation, Apple Secure Enclave expanded API). We are also monitoring work on secure multi-party computation (MPC) for distributed classification; MPC could permit multiple operators to jointly run a classifier without any single operator seeing plaintext. Current MPC latency (5-50 seconds per image) is prohibitive for interactive workloads but may improve.

## 18.3 Residual risk: Novel content not in hash list

The PDQ hash-matching in Section 13 detects only content already in the known-bad list. Novel CSAM (content newly produced, never before hashed) passes the filter.

**Current mitigations:**
- The Phase 3 classifier (Section 12.4) is intended to detect novel content via machine-learned classification.
- User reporting workflows allow recipients to flag novel content, which is then added to the hash list.

**Open work:** Improvements to open-source CSAM classifiers. We note that research in this area is sensitive: classifier training requires curated training datasets, which are themselves CSAM and therefore cannot be distributed. This bottleneck is well-recognised by NCMEC and IWF, who train classifiers on their own curated datasets and release only the classifier weights. Foundation engagement with NCMEC and IWF for classifier access is a Phase 3 priority.

## 18.4 Residual risk: Adversarial perturbation of known content

Sophisticated adversaries can perturb known-bad content with minor modifications that push PDQ Hamming distance above the match threshold while maintaining visual recognisability. This is an arms race.

**Current mitigations:**
- Multiple hash algorithms (PDQ primary; PDQF for video; potentially perceptual hashes from future standards) increase the cost of evasion.
- Shorter match threshold (tighter) reduces false negatives at the cost of more false positives.

**Open work:** Adversarial-robust perceptual hashing is an open research problem. Recent work on neural perceptual hashes [e.g. NeuralHash's abandoned design and subsequent academic analyses, Jain et al. 2022] shows that even neural-network hashes can be adversarially attacked. No known hash is robust against a well-resourced adversary.

## 18.5 Residual risk: Legal evolution

The legal environment of 2026 is not the legal environment of 2030. Specific scenarios we are monitoring:

- **Chat Control 2.0:** The EU Chatkontrolle proposal may return in altered form. The architecture is robust to most variants (mandatory server-side scanning is architecturally impossible because operators hold only ciphertext shares; mandatory client-side scanning would be a new user-facing feature that DCD's architecture neither implements nor prevents). The Foundation commits publicly not to deploy client-side scanning for any purpose other than the opt-in PDQ known-bad filter described in Section 13.

- **EARN IT Act or STOP CSAM Act in the US:** Would affect Section 230 availability. DCD's operator model leans on DSA and German law for primary liability analysis, but US-jurisdiction operators would face US-specific questions.

- **Online Safety Act s.122 notices in the UK:** If deployed against an E2EE provider, would precipitate a legal challenge. DCD's architecture would be an empirical data point in that challenge, demonstrating that content-filtering can be implemented client-side without breaking E2EE.

**Current mitigations:**
- Jurisdictional diversity of operators.
- Foundation relationships with EFF, EDRi, CCC, Chaos Computer Club, ARTICLE 19, and other civil-society groups for early warning and advocacy.
- Architectural flexibility: DCD does not enforce any specific political position, it simply provides a system that is resistant to the specific threat of unsolicited illegal content.

## 18.6 Residual risk: Client-device compromise

If the user's device is compromised (malware with root/kernel privileges), no application-level defence including DCD can fully protect the user. The compromised OS can:

- Read application memory including locked pages (by bypassing the kernel's enforcement).
- Observe network traffic.
- Inject code into the SimpleGoX process.
- Disable the DCD hash-filter before render.

**Current mitigations:**
- Support for verified boot (GrapheneOS for Android, iOS Secure Boot, macOS Secure Boot) as recommended user posture for high-risk users.
- Hardware-backed keystores (Keystore, Keychain, DPAPI).
- Minimised client attack surface (Rust safety, conservative dependency choices).

**Open work:** The SimpleGoX team is actively investigating ways to further minimise client surface area. The ESP32-based SimpleGo hardware is a particular area of interest because its attack surface is genuinely small (no general-purpose OS, custom firmware, USB-only input).

## 18.7 Future work: Post-quantum upgrades

ML-KEM-768 provides post-quantum security today. As cryptanalysis advances, both ML-KEM-768 and X25519 may require replacement. The hybrid KEM construction permits rotation of either component independently; this is an important future-proofing property.

The Foundation commits to:
- Monitoring NIST PQC standardisation and IRTF CFRG recommendations.
- Rotating primitives via protocol version bumps when NIST or CFRG recommends.
- Maintaining downgrade resistance in the protocol state machine.

## 18.8 Future work: Integration with Matrix federation

The Matrix protocol's federation model is similar in some respects to DCD's operator model. Integration of DCD shares into Matrix media repositories would be a useful interoperability contribution, allowing Matrix servers to participate as GoNode operators for the file-storage subsystem. This is tracked as future work pending Matrix Spec Change (MSC) review.

## 18.9 Future work: Fully-homomorphic filtering

In the long term (5-10 year horizon), fully homomorphic encryption (FHE) may become efficient enough to permit server-side content filtering on ciphertext without decryption. Current FHE (TFHE, CKKS, BGV) imposes latency and ciphertext expansion on the order of 1000x, which is prohibitive. If these ratios improve by two to three orders of magnitude, server-side PDQ matching on encrypted shares becomes feasible, at which point the moderation-classifier problem and the known-bad-filter problem could both be moved server-side without breaking confidentiality.

We note this as a research direction and do not assume it for the baseline design.

## 18.10 Call for partners

We invite:

- **Cryptographers:** for protocol review and attack discovery.
- **Lawyers:** for opinion work on the open questions in Section 15.6.
- **Child-safety organisations:** for hash list partnerships and guidance on CSAM prevention.
- **Civil society:** for advocacy and governance participation.
- **Operators:** willing to run infrastructure in diverse jurisdictions.
- **Funders:** for Foundation operations (NLnet, Mozilla MOSS, OpenTech Fund, Prototype Fund, German BMBF research grants).

Contact: `contact@simplego.dev`.

---

# 19. Conclusion

Every mainstream messenger in 2026, with the narrow exception of peer-to-peer outliers like Briar, ships with a design decision that has become a weaponizable vulnerability: when a user is exposed to new media, that media is automatically fetched and written to persistent storage. In jurisdictions where mere possession of certain content is a strict-liability offence, this design decision creates a trap that opportunistic abusers, targeted adversaries, and state-level actors have already begun to exploit.

The problem has been acknowledged by maintainers. The most candid acknowledgement we have found is SimpleX's own RFC of 30 December 2024 [SimpleX 2024], which we have quoted extensively in this whitepaper. The WhatsApp zero-click group-chat media download vulnerability disclosed by Google Project Zero on 27 January 2026 [Malwarebytes 2026a] is the most recent public confirmation. Russian journalist Ivan Golunov's 2019 case [Moscow Times 2020-2021, RFE/RL 2020] is the paradigmatic physical-evidence analogue.

SimpleGoX, the messenger client of the SimpleGo Ecosystem, with integrated GoNode Distributed Content Defense (DCD), is the first production architecture we are aware of that addresses this problem end-to-end. The architecture rests on six interlocking defences:

1. No auto-download for unconfirmed contacts; deterministic silhouettes instead.
2. Ephemeral RAM-only rendering with hardware-backed memory locking.
3. Distributed (3,5) Reed-Solomon erasure coding with per-share encryption, such that no single operator can reconstruct content.
4. Client-side PDQ perceptual-hash matching against known-bad content before render.
5. Optional TEE-based moderation for group administrators.
6. Stake-based operator economics denominated in EUR-pegged stablecoin, avoiding MiCA token classification.

Each defence is specified in this whitepaper with cryptographic detail, with reference to established standards and peer-reviewed literature, and with honest statement of its limits. The combination is meaningfully better than any mainstream messenger's current posture on the specific threat we have documented.

The architecture is designed to be legally defensible under German §184b StGB, the EU Digital Services Act, GDPR, 47 U.S.C. §230, and the UK Online Safety Act. Section 15 argues the compliance positions in detail. We invite adversarial legal review and commit to publishing the opinions we obtain.

The implementation plan (Section 17) is scoped to a small team, builds on the existing SimpleGo Ecosystem infrastructure (ten SMP relays and one XFTP server operated by IT and More Systems in Germany), and reaches mainnet within approximately 24 months under conservative assumptions. Phased deployment with independent audits at each gate manages the risk of catastrophic failure.

The open problems (Section 18) are honestly stated. DCD does not solve every problem. Threshold collusion among operators remains a risk. TEE fragmentation limits moderation. Novel content evades hash matching. Legal evolution may require architectural adaptation. Client-device compromise defeats any application-level defence. We acknowledge these limits rather than eliding them, because architecture secrets are architecture failures.

If the SimpleGoX + GoNode DCD system succeeds as designed, users of messenger infrastructure will be able to participate in open and public groups without the threat of having their devices weaponised against them. Journalists in hostile jurisdictions will have a messenger that does not betray them to pretextual prosecution. Whistleblowers will have a communication channel that cannot be compromised by a single hostile operator. Ordinary users will have the peace of mind of knowing that adding a new contact or joining a new group does not expose them to criminal liability for another's actions.

That is a goal worth building toward.

---

*The authors thank the contributors to the SimpleGo Ecosystem community group, the SimpleX Chat team for their candid RFC on content moderation, the Signal and Matrix engineering communities for open discussion of threat models, and the civil-society organisations (EFF, EDRi, CCC, Chaos Computer Club, ARTICLE 19, Reporters Without Borders, Access Now, Committee to Protect Journalists) that have documented the threat model the architecture addresses.*

*Any errors in this whitepaper are the authors' own. Feedback is welcome at* `contact@simplego.dev` *and via issue on github.com/saschadaemgen/GoNode.*

---


# References

References are organised by type: academic papers, standards and RFCs, legal sources, news and investigative sources, and technical documentation. URLs are provided where available; where sources are offline or behind paywalls, sufficient bibliographic information for retrieval is given.

## Academic papers and peer-reviewed sources

[Ateniese 2007] Ateniese, G., Burns, R., Curtmola, R., Herring, J., Kissner, L., Peterson, Z., and Song, D. "Provable Data Possession at Untrusted Stores." Proceedings of the 14th ACM Conference on Computer and Communications Security (CCS '07), 598-609. DOI 10.1145/1315245.1315318.

[Davis 2019] Davis, A. "Open-sourcing photo- and video-matching technology to make the internet safer." Meta Engineering Blog, 1 August 2019. Available at engineering.fb.com.

[Douze 2017] Douze, M., Revaud, J., Verbeek, J., Jegou, H., and Schmid, C. "Circulant temporal encoding for video retrieval and temporal alignment." International Journal of Computer Vision 119(3):291-306, 2017.

[Harvard HRJ 2023] Harvard Human Rights Journal. "Disrupting Digital Authoritarians: Regulating the Human Rights Abuses of the Pegasus Project." Volume 36, Spring 2023. Available at journals.law.harvard.edu/hrj.

[Howard 2002] Howard, M. and LeBlanc, D. "Writing Secure Code," 2nd ed. Microsoft Press, 2002. ISBN 0-7356-1722-8. Introduces the STRIDE threat modelling methodology.

[Jain 2022] Jain, S., Cretu, A.-M., and de Montjoye, Y.-A. "Adversarial Detection Avoidance Attacks: Evaluating the robustness of perceptual hashing-based client-side scanning." USENIX Security Symposium 2022.

[Juels 2007] Juels, A. and Kaliski, B. "PORs: Proofs of Retrievability for Large Files." Proceedings of the 14th ACM Conference on Computer and Communications Security (CCS '07), 584-597.

[O'Connor 2020] O'Connor, J., Aumasson, J.-P., Neves, S., and Wilcox-O'Hearn, Z. "BLAKE3: One function, fast everywhere." Technical specification, 2020. github.com/BLAKE3-team/BLAKE3-specs.

[Plank 2013] Plank, J. S. "Erasure Codes for Storage Systems: A Brief Primer." USENIX ;login: 38(6):44-50, December 2013. Available at usenix.org/system/files/login/articles/10_plank-online.pdf.

[Reed 1960] Reed, I. S. and Solomon, G. "Polynomial Codes Over Certain Finite Fields." Journal of the Society for Industrial and Applied Mathematics 8(2):300-304, 1960.

[Shamir 1979] Shamir, A. "How to Share a Secret." Communications of the ACM 22(11):612-613, November 1979. DOI 10.1145/359168.359176.

[Storj 2018] Storj Labs. "Storj: A Decentralized Cloud Storage Network Framework." Version 3.0, October 2018. Available at static.storj.io/storjv3.pdf.

[Walrus 2024] Danezis, G., Hofte, L., Kokoris-Kogias, L., Sonnino, A., and Spiegelman, A. "Walrus: An Efficient Decentralized Storage Network." arXiv:2505.05370, 2024.

## Standards and RFCs

[FIPS 180-4] National Institute of Standards and Technology. "Secure Hash Standard (SHS)." FIPS PUB 180-4, August 2015.

[FIPS 202] National Institute of Standards and Technology. "SHA-3 Standard: Permutation-Based Hash and Extendable-Output Functions." FIPS PUB 202, August 2015.

[FIPS 203] National Institute of Standards and Technology. "Module-Lattice-Based Key-Encapsulation Mechanism Standard." FIPS PUB 203, August 2024. Standardises ML-KEM (CRYSTALS-Kyber).

[RFC 5869] Krawczyk, H. and Eronen, P. "HMAC-based Extract-and-Expand Key Derivation Function (HKDF)." IETF RFC 5869, May 2010.

[RFC 7748] Langley, A., Hamburg, M., and Turner, S. "Elliptic Curves for Security." IETF RFC 7748, January 2016.

[RFC 8032] Josefsson, S. and Liusvaara, I. "Edwards-Curve Digital Signature Algorithm (EdDSA)." IETF RFC 8032, January 2017.

[RFC 8439] Nir, Y. and Langley, A. "ChaCha20 and Poly1305 for IETF Protocols." IETF RFC 8439, June 2018.

[RFC 8949] Bormann, C. and Hoffman, P. "Concise Binary Object Representation (CBOR)." IETF STD 94, RFC 8949, December 2020.

[RFC 9381] Papadopoulos, D., Wessels, D., Huque, S., Naslund, M., Goldberg, S., Vcelak, J., Papadopoulos, K., and Vivanco, L. "Verifiable Random Functions (VRFs)." IETF RFC 9381, August 2023.

[draft-irtf-cfrg-xchacha] Arciszewski, S. "XChaCha: eXtended-nonce ChaCha and AEAD_XChaCha20_Poly1305." IRTF CFRG Internet Draft, latest version.

[Kret 2023] Kret, R. and Kotov, V. "The PQXDH Key Agreement Protocol." Signal Foundation specification, 19 September 2023. Available at signal.org/docs/specifications/pqxdh.

[Perrin-Marlinspike] Perrin, T. and Marlinspike, M. "The Double Ratchet Algorithm." Signal Foundation specification, current. Available at signal.org/docs/specifications/doubleratchet.

[Marlinspike-Perrin X3DH] Marlinspike, M. and Perrin, T. "The X3DH Key Agreement Protocol." Signal Foundation specification, 4 November 2016. Available at signal.org/docs/specifications/x3dh.

[Stebila-Fluhrer draft] Stebila, D. and Fluhrer, S. "Hybrid key exchange in TLS 1.3." IETF draft-ietf-tls-hybrid-design, current version.

## Legal sources

[BGBl 2024 I Nr. 213] Bundesgesetzblatt. "Gesetz zur Anpassung der Mindeststrafen des § 184b Absatz 1 Satz 1 und Absatz 3 des Strafgesetzbuches - Verbreitung, Erwerb und Besitz kinderpornographischer Inhalte." Jahrgang 2024 Teil I Nr. 213, ausgegeben am 27. Juni 2024. In Kraft seit 28. Juni 2024.

[BGBl 2021 I S. 1810] Bundesgesetzblatt. "Gesetz zur Bekämpfung sexualisierter Gewalt gegen Kinder." Jahrgang 2021 Teil I, S. 1810, ausgegeben am 22. Juni 2021.

[BGBl 2024 I Nr. 149] Bundesgesetzblatt. "Digitale-Dienste-Gesetz (DDG)." Jahrgang 2024 Teil I Nr. 149, ausgegeben am 6. Mai 2024. In Kraft seit 14. Mai 2024.

[Bundestag 2024] Deutscher Bundestag. "Strafmaß bei Kinderpornografie soll angepasst werden." Bericht über die öffentliche Anhörung des Rechtsausschusses vom 10. April 2024 zu Drucksache 20/10540. Available at bundestag.de/dokumente/textarchiv/2024.

[StGB §184b] Strafgesetzbuch §184b "Verbreitung, Erwerb und Besitz kinderpornographischer Inhalte." Current version effective 28 June 2024 per BGBl. 2024 I Nr. 213. Available at dejure.org/gesetze/StGB/184b.html.

[StGB §202a] Strafgesetzbuch §202a "Ausspähen von Daten." Current version. Available at dejure.org/gesetze/StGB/202a.html.

[StGB §206] Strafgesetzbuch §206 "Verletzung des Post- oder Fernmeldegeheimnisses." Current version. Available at dejure.org/gesetze/StGB/206.html.

[TKG 2021] Telekommunikationsgesetz vom 23. Juni 2021 (BGBl. I S. 1858), zuletzt geändert durch Artikel [current] des Gesetzes vom [current date]. Available at gesetze-im-internet.de/tkg_2021.

[StPO §112a] Strafprozessordnung §112a "Haftgrund der Wiederholungsgefahr." Current version. Available at dejure.org/gesetze/StPO/112a.html.

[Regulation (EU) 2022/2065] Regulation (EU) 2022/2065 of the European Parliament and of the Council of 19 October 2022 on a Single Market For Digital Services (Digital Services Act). Official Journal L 277, 27.10.2022, p. 1-102. ELI eli/reg/2022/2065/oj.

[Regulation (EU) 2016/679] Regulation (EU) 2016/679 of the European Parliament and of the Council of 27 April 2016 on the protection of natural persons with regard to the processing of personal data and on the free movement of such data (General Data Protection Regulation). Official Journal L 119, 4.5.2016, p. 1-88.

[Regulation (EU) 2021/1232] Regulation (EU) 2021/1232 on a temporary derogation from certain provisions of Directive 2002/58/EC as regards the use of technologies by providers of number-independent interpersonal communications services for the processing of personal and other data for the purpose of combatting online child sexual abuse. Official Journal L 274, 30.7.2021, p. 41-51. Expired 3 April 2026.

[Regulation (EU) 2023/1114] Regulation (EU) 2023/1114 of the European Parliament and of the Council of 31 May 2023 on markets in crypto-assets (MiCA). Official Journal L 150, 9.6.2023, p. 40-205.

[COM/2022/209] European Commission. "Proposal for a Regulation of the European Parliament and of the Council laying down rules to prevent and combat child sexual abuse." COM(2022) 209 final, 11 May 2022.

[18 USC §2252A] 18 United States Code §2252A "Certain activities relating to material constituting or containing child pornography."

[18 USC §2258A] 18 United States Code §2258A "Reporting requirements of electronic communication service providers and remote computing service providers."

[47 USC §230] 47 United States Code §230 "Protection for private blocking and screening of offensive material."

[NY v. Ferber] New York v. Ferber, 458 U.S. 747 (1982).

[Ashcroft v. Free Speech] Ashcroft v. Free Speech Coalition, 535 U.S. 234 (2002).

[Online Safety Act 2023] Online Safety Act 2023 (United Kingdom), c. 50. Royal Assent 26 October 2023.

[Protection of Children Act 1978] Protection of Children Act 1978 (United Kingdom), c. 37, with subsequent amendments.

[Investigatory Powers Act 2016] Investigatory Powers Act 2016 (United Kingdom), c. 25.

[Federal Law No. 374-FZ] Federal Law of the Russian Federation No. 374-FZ of 7 July 2016 "On Amending the Federal Law 'On Counteracting Terrorism'" (the Yarovaya package).

## Technical documentation

[Android Keystore] Google. "Android Keystore system." developer.android.com/training/articles/keystore.

[Apple Platform Security 2023] Apple Inc. "Apple Platform Security Guide." May 2023 revision. support.apple.com/guide/security.

[ARM TrustZone] Arm Limited. "Arm Architecture Reference Manual." Current edition. Includes specification of TrustZone secure-world.

[Intel SGX Programming] Intel Corporation. "Intel Software Guard Extensions Programming Reference." Latest revision.

[Intel TDX] Intel Corporation. "Intel Trust Domain Extensions." Specification, current version.

[Meta ThreatExchange] Meta / Facebook Open Source. "ThreatExchange PDQ specification." github.com/facebook/ThreatExchange.

[Signal-Android #8714] Signal-Android repository, GitHub issue #8714 "Update download should obey 'Media auto-download' settings," opened 27 March 2019. github.com/signalapp/Signal-Android/issues/8714.

[Signal Support 2024] Signal Messenger. "Data usage and media auto-download." support.signal.org/hc.

[SimpleX 2024] SimpleX Chat. "Evolving content moderation." RFC document at docs/rfcs/2024-12-30-content-moderation.md in github.com/simplex-chat/simplex-chat, commit 821f034d1, 30 December 2024.

[SimpleX Chat #6207] SimpleX Chat GitHub issue #6207 "SimpleX won't allow me to change profile picture, send images or go through my file system," 20 August 2025.

[SimpleX Chat #4328] SimpleX Chat GitHub issue #4328 "5.8 can't change profile picture and send image files," 15 June 2024.

[Storj Docs] Storj Labs. "Introduction to Storj." storj.dev/learn. Current version.

[klauspost/reedsolomon] Klaus Post. "Reed-Solomon Erasure Coding in Go." github.com/klauspost/reedsolomon. Go library used by Storj and others.

## News and investigative sources

[Atomic Mail 2025] Atomic Mail Blog. "Chat Control Retreats: Europe's Privacy Win - For How Long?" November 2025. atomicmail.io/blog/chat-control-retreats-europe-big-privacy-win-but-for-how-long.

[Awakened 2019] "Awakened" (security researcher). "How a double-free bug in WhatsApp turns to RCE." awakened1712.github.io/hacking/hacking-whatsapp-gif-rce, October 2019. Documents CVE-2019-11932.

[Envista Forensics 2026] Envista Forensics. "Digital Forensics in CSAM Cases: Attorney Resource Guide." January 2026. envistaforensics.com/knowledge-center.

[Help Net Security 2025] Zorz, Z. "WhatsApp vulnerability could be used to infect Windows users with malware (CVE-2025-30401)." Help Net Security, 9 April 2025. helpnetsecurity.com/2025/04/09/whatsapp-vulnerability-windows-cve-2025-30401.

[Malwarebytes 2025] Malwarebytes Labs. "WhatsApp fixes vulnerability used in zero-click attacks." Malwarebytes Blog, September 2025. malwarebytes.com/blog/news/2025/09/whatsapp-fixes-vulnerability-used-in-zero-click-attacks.

[Malwarebytes 2026a] Malwarebytes Labs. "A WhatsApp bug lets malicious media files spread through group chats." Malwarebytes Blog, 27 January 2026. malwarebytes.com/blog/news/2026/01/a-whatsapp-bug-lets-malicious-media-files-spread-through-group-chats.

[Moscow Times 2020] The Moscow Times. "Russian Officers Charged With Framing Investigative Journalist Golunov." 30 January 2020. themoscowtimes.com.

[Moscow Times 2021] The Moscow Times. "Ex-Policemen Jailed for Planting Drugs on Russian Journalist." 28 May 2021. themoscowtimes.com.

[Moscow Times 2023] The Moscow Times. "Russian Investigative Journalist Wins Damages in Falsified Drug Case." July 2023. themoscowtimes.com.

[RFE/RL 2020] Radio Free Europe / Radio Liberty. "Former Moscow Police Officers Accused Of Fabricating Case Against Journalist Golunov." 29 January 2020. rferl.org/a/former-moscow-police-officers-detained-in-journalist-golunov-s-fabricated-case/30403643.html.

[RSF 2025] Reporters Without Borders / Reporters sans frontières. "World Press Freedom Index 2025." rsf.org/en.

[State of Surveillance 2026] State of Surveillance. "Chat Control Is Dead. Long Live Chat Control." April 2026. stateofsurveillance.org.

---

# Appendix A: Wire format summary

All DCD protocol messages are encoded as CBOR (RFC 8949) with the following tag assignments. Tags are requested from the IANA CBOR Tags Registry as part of the Phase 1 specification work.

| Tag (provisional) | Purpose |
|:------------------|:--------|
| 64000 | DCDStoreShareRequest |
| 64001 | DCDStoreShareResponse |
| 64002 | DCDFetchShareRequest |
| 64003 | DCDFetchShareResponse |
| 64004 | DCDChallengeRequest |
| 64005 | DCDChallengeResponse |
| 64006 | DCDContentFlag |
| 64007 | DCDClassificationAttestation |
| 64008 | DCDHashListUpdate |
| 64009 | DCDDeletionRequest |
| 64010 | DCDCredit |

Each CBOR object is a map with string keys corresponding to the ASN.1 field names given in Section 9. Unknown fields are ignored (forward compatibility). All signatures and hashes are represented as CBOR byte strings.

---

# Appendix B: Selected legal text excerpts

For the reader's convenience, the most important legal provisions are reproduced here in full.

## B.1 §184b StGB (Germany)

Current version per BGBl. 2024 I Nr. 213, in force 28 June 2024. Full text given in Section 4.1.1 above. Jurisprudence: 909 decisions by German higher courts referencing §184b are catalogued on dejure.org as of the whitepaper's publication date.

## B.2 DSA Article 4 (Mere conduit)

Full text given in Section 4.3.1 above. Regulation (EU) 2022/2065, Article 4.

## B.3 GDPR Article 32

> "1. Taking into account the state of the art, the costs of implementation and the nature, scope, context and purposes of processing as well as the risk of varying likelihood and severity for the rights and freedoms of natural persons, the controller and the processor shall implement appropriate technical and organisational measures to ensure a level of security appropriate to the risk, including inter alia as appropriate:
> (a) the pseudonymisation and encryption of personal data;
> (b) the ability to ensure the ongoing confidentiality, integrity, availability and resilience of processing systems and services;
> (c) the ability to restore the availability and access to personal data in a timely manner in the event of a physical or technical incident;
> (d) a process for regularly testing, assessing and evaluating the effectiveness of technical and organisational measures for ensuring the security of the processing.
>
> 2. In assessing the appropriate level of security account shall be taken in particular of the risks that are presented by processing, in particular from accidental or unlawful destruction, loss, alteration, unauthorised disclosure of, or access to personal data transmitted, stored or otherwise processed.
>
> 3. Adherence to an approved code of conduct as referred to in Article 40 or an approved certification mechanism as referred to in Article 42 may be used as an element by which to demonstrate compliance with the requirements set out in paragraph 1 of this Article.
>
> 4. The controller and processor shall take steps to ensure that any natural person acting under the authority of the controller or the processor who has access to personal data does not process them except on instructions from the controller, unless he or she is required to do so by Union or Member State law."
>
> Source: Regulation (EU) 2016/679, Article 32.

## B.4 18 U.S.C. §2252A(a)(5)(B)

> "(a) Any person who--
> ...
> (5) either--
> ...
> (B) knowingly possesses, or knowingly accesses with intent to view, any book, magazine, periodical, film, videotape, computer disk, or any other material that contains an image of child pornography that has been mailed, or shipped or transported using any means or facility of interstate or foreign commerce or in or affecting interstate or foreign commerce by any means, including by computer, or that was produced using materials that have been mailed, or shipped or transported in or affecting interstate or foreign commerce by any means, including by computer;
> ...
> shall be punished as provided in subsection (b)."
>
> Subsection (b) provides up to 10 years for a first offence and up to 20 years for repeat offences.
>
> Source: 18 U.S.C. §2252A, current text.

---

# Appendix C: Threat model extended tables

## C.1 Asset-Adversary matrix

| Asset | AD1 passive | AD2 active MITM | AD3 1-2 operators | AD4 compromised client | AD5 state lawful | AD6 state pretextual | AD7 3+ operators |
|:------|:-----------:|:---------------:|:----------------:|:---------------------:|:----------------:|:--------------------:|:----------------:|
| A1 identities (pubkeys) | Visible | Not fakeable | Visible | Accessible | Accessible via warrant | Accessible via seizure | Visible |
| A2 content plaintexts | Not accessible | Not accessible | Not accessible | Accessible if user rendered it | Accessible on seized+unlocked device | Accessible on seized+unlocked device | **Potentially accessible** |
| A3 group membership | Visible on SMP traffic pattern | Not decryptable | Not visible per-operator | Accessible | Accessible via warrant + collusion | Accessible via seizure | Aggregable |
| A4 operator stake | Visible on-chain | Visible on-chain | Own stake | Client doesn't hold | Public | Public | Aggregable |
| A5 moderator decisions | Not visible | Not visible | Flag visibility | Accessible on that client | Accessible via warrant | Accessible via seizure | Flag visibility |
| A6 known-bad hash list | Public merkle root | Public merkle root | Could host shares of list | Accessible | Accessible | Accessible | Visible |

## C.2 Defence-in-depth summary

The DCD architecture provides defence-in-depth for the central threat (unsolicited illegal content leading to user prosecution):

- **Layer 1 (transport):** Tor v3 hidden services prevent network-level association between client and operators.
- **Layer 2 (identity):** Ephemeral session keys and SMP queue addresses prevent persistent identification.
- **Layer 3 (encryption):** Threshold encryption with Shamir and Reed-Solomon prevents single-operator reconstruction.
- **Layer 4 (policy):** No-auto-download policy prevents passive client exposure.
- **Layer 5 (content):** Pre-render PDQ hash filter blocks known-bad content at reassembly.
- **Layer 6 (rendering):** RAM-only rendering with explicit_bzero prevents persistent storage.
- **Layer 7 (hardware):** Device keystore and FLAG_SECURE reduce cross-app leakage.
- **Layer 8 (legal):** Mere-conduit and hosting-privilege analysis under DSA Art. 4-6 protects operators.

Compromise of any single layer does not result in catastrophic failure. Compromise of multiple layers is required for end-to-end failure, and the residual risks of such multi-layer failures are explicitly documented in Section 18.

---

# Appendix D: Glossary

- **AEAD:** Authenticated Encryption with Associated Data. A primitive providing both confidentiality and integrity.
- **BaFin:** Bundesanstalt für Finanzdienstleistungsaufsicht, the German Federal Financial Supervisory Authority.
- **BGBl:** Bundesgesetzblatt, the German Federal Law Gazette.
- **BKA:** Bundeskriminalamt, the German Federal Criminal Police Office.
- **BNetzA:** Bundesnetzagentur, the German Federal Network Agency.
- **CBOR:** Concise Binary Object Representation (RFC 8949), a binary serialisation format.
- **CSAM:** Child Sexual Abuse Material.
- **DCD:** Distributed Content Defense, the architecture specified in this whitepaper.
- **DDG:** Digitale-Dienste-Gesetz, Germany's national implementation of the DSA.
- **DSA:** Digital Services Act, Regulation (EU) 2022/2065.
- **E2EE:** End-to-End Encryption.
- **ECVRF:** Elliptic Curve Verifiable Random Function, specified in RFC 9381.
- **eG:** eingetragene Genossenschaft, a registered cooperative under German law.
- **EMI:** Electronic Money Institution (EU licence category).
- **ePrivacy Directive:** Directive 2002/58/EC concerning the processing of personal data and the protection of privacy in the electronic communications sector.
- **EURC:** Euro Coin, an EU euro-pegged e-money token issued by Circle Internet Financial.
- **e.V.:** eingetragener Verein, a registered association under German law.
- **FHE:** Fully Homomorphic Encryption.
- **GDPR:** General Data Protection Regulation, Regulation (EU) 2016/679.
- **GoNode:** The decentralized service-node network being built by IT and More Systems as part of the SimpleGo Ecosystem.
- **HKDF:** HMAC-based Extract-and-Expand Key Derivation Function (RFC 5869).
- **IWF:** Internet Watch Foundation, UK CSAM clearinghouse.
- **KEM:** Key Encapsulation Mechanism.
- **MiCA:** Markets in Crypto-Assets Regulation, Regulation (EU) 2023/1114.
- **ML-KEM:** Module-Lattice-based Key-Encapsulation Mechanism, standardised as NIST FIPS 203 (formerly CRYSTALS-Kyber).
- **NCMEC:** National Center for Missing and Exploited Children, U.S. CSAM clearinghouse.
- **PDQ:** Perceptual hash developed by Meta, published open-source via ThreatExchange.
- **PQXDH:** Post-Quantum Extended Diffie-Hellman, the Signal Foundation's key agreement with post-quantum additions.
- **RFC:** Request for Comments, the IETF standards document series.
- **SimpleGo:** The hardware-focused subsystem of the SimpleGo Ecosystem, including the LilyGo T-Deck Plus firmware target.
- **SimpleGoX:** The Rust-based messenger client of the SimpleGo Ecosystem.
- **SimpleX:** SimpleX Chat, the upstream messenger project whose SMP protocol is used as the transport foundation.
- **SMP:** SimpleX Messaging Protocol, used for message routing.
- **STRIDE:** Threat modelling methodology covering Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege.
- **TEE:** Trusted Execution Environment (ARM TrustZone, Intel SGX, Apple Secure Enclave, etc.).
- **TKG:** Telekommunikationsgesetz, the German Telecommunications Act.
- **TKÜV:** Telekommunikations-Überwachungsverordnung, the implementing regulation for lawful interception in Germany.
- **TTL:** Time-to-Live, the period after which stored shares expire.
- **VRF:** Verifiable Random Function.
- **X3DH:** Extended Triple Diffie-Hellman, the Signal Foundation's initial key agreement protocol.
- **XFTP:** SimpleX File Transfer Protocol, used for file transfer in the SimpleX ecosystem.

---

*End of Whitepaper v1.0 Draft.*

*GoNode Distributed Content Defense Whitepaper*
*IT and More Systems, Recklinghausen, Germany*
*April 2026*
*Licensed under CC BY-SA 4.0*
*Repository: github.com/saschadaemgen/GoNode*
