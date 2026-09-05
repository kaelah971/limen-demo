# P14 Controlled Judge-Mode PASS

**CONTROLLED JUDGE-MODE VALIDATION**

This document records the fresh patched-state validation using the hardened
Limen Action. It is not production adoption evidence or external-user
evidence.

## Run

- Observed: 2026-09-05 UTC
- Repository: `kaelah971/limen-demo`
- Pull request: [#1](https://github.com/kaelah971/limen-demo/pull/1)
- Canonical Limen Action: `kaelah971/limen@a91d36bfe8eaab5d95f791e39449878239bf948d`
- Demo commit: `6094dcc71b69df24c2b4bde0daa22b82c5930e42`
- Base SHA: `2f2cd0bbcffd00c562c82d834fe2669afc3352f7`
- Head SHA: `6094dcc71b69df24c2b4bde0daa22b82c5930e42`
- Policy version: `LP-fde4ac5cdba2`
- Action run: [33959096100](https://github.com/kaelah971/limen-demo/actions/runs/33959096100)
- Job: [101287671662](https://github.com/kaelah971/limen-demo/actions/runs/33959096100/job/101287671662)
- Limen run ID: `LM-e0ffd7ac-f64b-4d45-9b8d-9f4197426a44`
- GitHub run attempt: `1`

## Dependency And Decision

- Controlled patched dependency: `lodash@4.18.1`
- Overall decision: `PASS`
- Overall reason: `NO_RELEVANT_VULNERABILITY`
- Decision count: `0`
- Evaluated CVEs: none
- Skipped CVEs: none

This records the exact patched Judge-Mode state used by this run. It does not
claim that `lodash@4.18.1` is universally safe.

## Telegraph And Payment

- Telegraph request count: `0`
- Known total cost: `$0.00`
- Telegraph initialization: skipped because no relevant CVE was selected
- No payment, signature, signed payload, or x402 proof was generated in this run.

## Observability And Security

- Event validation, trusted-base policy retrieval, policy parse, dependency review, advisory enrichment, finding selection, decision evaluation, aggregate decision, summary output, and workflow result completed successfully.
- Dependency review used attempt `1` of `3`, with retry count `0`.
- Ledger persistence was skipped because this workflow has no Action-reachable ledger configuration.
- The Action exposed no private key or bearer token.

This fresh P14 PASS run validates the patched end of the controlled GitHub ->
policy -> decision path. It does not create a receipt or claim ledger
persistence.
