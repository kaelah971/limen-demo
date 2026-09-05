# P14 Controlled Judge-Mode HOLD

**CONTROLLED JUDGE-MODE VALIDATION**

This document records a fresh live validation using the hardened Limen Action.
It is not production adoption evidence or external-user evidence.

## Run

- Observed: 2026-09-05 UTC
- Repository: `kaelah971/limen-demo`
- Pull request: [#1](https://github.com/kaelah971/limen-demo/pull/1)
- Canonical Limen Action: `kaelah971/limen@a91d36bfe8eaab5d95f791e39449878239bf948d`
- Demo commit: `a0b41e6447e4924efd9ac710811d0a79f56be8c5`
- Base SHA: `2f2cd0bbcffd00c562c82d834fe2669afc3352f7`
- Head SHA: `a0b41e6447e4924efd9ac710811d0a79f56be8c5`
- Policy version: `LP-fde4ac5cdba2`
- Action run: [33958836557](https://github.com/kaelah971/limen-demo/actions/runs/33958836557)
- Job: [101286969714](https://github.com/kaelah971/limen-demo/actions/runs/33958836557/job/101286969714)
- Limen run ID: `LM-759f566d-f8e9-4d18-9cb2-1ea2561ce155`
- GitHub run attempt: `1`

## Dependency And Decision

- Controlled vulnerable dependency: `lodash@4.17.20`
- Overall decision: `HOLD`
- Overall reason: `AFFECTED_BLOCKING_DEPENDENCY`
- Decision count observed by the decision stage: `5`
- Evaluated CVEs:
  - `CVE-2021-23337`
  - `CVE-2026-4800`
  - `CVE-2020-28500`
  - `CVE-2025-13465`
  - `CVE-2026-2950`
- Skipped CVEs: none observed; finding selection reported five requests with the default five-lookup budget.
- Individual per-CVE decision rows and PASS/HOLD/REVIEW counts were not exposed by the public GitHub job/check APIs and are not inferred here.

## Telegraph And Payment

- Telegraph request count: `5`
- Known cost per request: `$0.01`
- Total known cost: `$0.05`
- Miner: `PREFLIGHT Infrastructure Signals` for all five requests
- Network: `eip155:84532` (Base Sepolia)
- Payment scheme: `exact`
- Provider durations: `1124 ms`, `306 ms`, `302 ms`, `617 ms`, `431 ms`
- Client durations: `7008 ms`, `4247 ms`, `5613 ms`, `4719 ms`, `4832 ms`
- The hardened Judge-Mode asset allowlist and amount ceilings were active in the pinned Action. The raw challenge asset, amount fields, signatures, and signed payloads are intentionally not emitted here.
- Every paid lookup completed through the hardened client without a payment-policy rejection.
- No redirect or repeated paid request was observed. Each request had `attempt=1` and `maxAttempts=1` in safe observability output.

## Observability And Security

- Event validation, trusted-base policy retrieval, policy parse, dependency review, advisory enrichment, finding selection, Telegraph initialization, decision evaluation, summary output, and aggregate decision completed successfully.
- Dependency review used attempt `1` of `3`, with retry count `0`.
- Ledger persistence was skipped because this workflow has no Action-reachable ledger configuration.
- The Action exposed no private key, bearer token, `PAYMENT-SIGNATURE`, signed payload, or reusable x402 proof.
- P13 controls remained enabled: trusted GitHub origin, canonical Telegraph origin, redirect rejection, Base Sepolia payment validation, per-request limit `50,000` base units, and per-run limit `250,000` base units.

This fresh P14 HOLD run validates the controlled GitHub -> Telegraph -> policy -> decision path. It does not create a receipt or claim ledger persistence.
