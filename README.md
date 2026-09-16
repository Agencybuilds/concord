# Concord

Reconciliation between tokenized securities on Stellar and the official books kept by transfer
agents, custodians and fund administrators.

When a security lives both on-chain and in a register, someone has to prove the two agree, every
day. Dividends, splits, freezes and clawbacks have to land on both sides. Today that work is
manual. Concord does it from ledger events.

**Status:** pre-build. Nothing here runs yet. The product brief, evidence and kill criteria are in
[`BRIEF.md`](./BRIEF.md).

## Why now

- DTCC's tokenization service plans to connect to Stellar in **H1 2027**. First assets: Russell
  1000 stocks, major index ETFs, US Treasuries (DTCC press release, 2026-05-27).
- Stellar already holds about **$4B** of tokenized RWAs (SDF Dune dashboard, 2026-08-29). Spiko,
  Franklin Templeton (BENJI), Ondo and WisdomTree all keep official registers alongside the chain.
- CAP-67 (Final, Protocol 23) makes classic Stellar operations emit `transfer`, `mint`, `burn`,
  `clawback` and `set_authorized` events in the same format as Soroban. For the first time,
  regulated-asset activity can be indexed without decoding every operation type by hand.

## What it will do

| Module | Job |
|---|---|
| Indexer | Read CAP-67 events for a watched set of regulated assets (classic and SEP-57) |
| Reconciler | Match on-chain holdings and movements against the register export, daily and on demand; flag breaks |
| Corporate actions | Record-date snapshots; dividend, split and redemption reconciliation |
| Controls log | Every freeze, authorisation change and clawback, tied to the instruction that caused it |
| Audit export | Regulator- and auditor-ready reports |

Read-only. Concord never holds keys or moves money.

## Who buys it

Transfer agents, custodians and fund administrators serving issuers on Stellar. Priced as
software: per asset and per seat.

## Relationship to other projects

Concord is a stand-alone company. It was split from the Ballast idea set on 2026-09-16 because
it shares no buyer, balance sheet or regulatory load with Ballast. See
`../ballast/README.md` for the reasoning.

## First step

Check whether this already exists: StellarExpert, Mercury/Zephyr, SDF Hubble, Vertalo,
Securitize's transfer agent, and DTCC's own tooling. If one of them ships reconciliation for
Stellar, stop.
