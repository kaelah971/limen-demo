# Limen Demo

This public repository is a controlled demonstration of Limen, a release evidence gate. It is not production adoption evidence and does not represent external-user evidence.

Limen has four separate roles:

- GitHub and Dependency Review establish repository-specific dependency context.
- Telegraph supplies separately routed CVE evidence when a relevant CVE exists.
- `limen.yml` defines the release policy.
- Limen returns `PASS`, `HOLD`, or `REVIEW`.

A Telegraph response alone does not prove repository exploitability. The repository-specific dependency state and the policy decision remain separate evidence.

## Current Hardened Workflow

The current reproducible workflow uses the immutable canonical Limen Action revision:

```yaml
name: Limen

on:
  pull_request:
    types:
      - opened
      - synchronize
      - reopened

permissions:
  contents: read

jobs:
  limen:
    runs-on: ubuntu-latest
    steps:
      - name: Evaluate release evidence
        uses: kaelah971/limen@a91d36bfe8eaab5d95f791e39449878239bf948d
        with:
          github-token: ${{ github.token }}
          telegraph-private-key: ${{ secrets.LIMEN_TELEGRAPH_PRIVATE_KEY }}
          telegraph-engine-url: ${{ vars.TELEGRAPH_ENGINE_URL }}
          usage-class: demo
```

The workflow needs only `contents: read`. It does not checkout the pull request, install dependencies, execute repository code, or publish a receipt.

Configure the paid path in the repository settings:

- GitHub Secret: `LIMEN_TELEGRAPH_PRIVATE_KEY`
- GitHub Variable: `TELEGRAPH_ENGINE_URL`
- Current validated Telegraph testnet endpoint: `http://13.237.89.59:7044/engine/v1/ask`
- Expected network: Base Sepolia, `eip155:84532`

The private key belongs only in GitHub Actions Secrets. The demo uses a funded Base Sepolia test wallet for paid lookups, and Limen's validated Telegraph requests used USDC. The x402 challenge supplies the actual payment requirement. Do not assume that Base Sepolia ETH is required.

Limen reads `limen.yml` from the pull request base SHA. A policy edit on the pull request head cannot change the policy used for that same evaluation.

Ledger persistence is optional and is not configured here. Receipt publication is not automatic from the Action. The active historical HOLD receipt ID is `LM-REC-B1306724D0B84B6EBDDF7E36`; no deployed canonical public host is confirmed for linking it. The historical PASS receipt `LM-REC-1463B3EF54DC4CA3827ED3DC` was intentionally revoked and must not be treated as active.

## P14 Hardened Judge Mode

The fresh controlled P14 sequence used the hardened Action above:

- Vulnerable state: `lodash@4.17.20` at commit `a0b41e6447e4924efd9ac710811d0a79f56be8c5`
- [Fresh P14 HOLD run](https://github.com/kaelah971/limen-demo/actions/runs/33958836557)
- Patched state: `lodash@4.18.1` at commit `6094dcc71b69df24c2b4bde0daa22b82c5930e42`
- [Fresh P14 PASS run](https://github.com/kaelah971/limen-demo/actions/runs/33959096100)
- [P14 evidence package](evidence/p14/)

The vulnerable run made five real paid Telegraph lookups and returned `HOLD`.
The patched run made zero Telegraph requests and returned `PASS`. These are
run-specific observations, not historical R0/P9 metrics and not adoption claims.

## Current Policy

The root `limen.yml` is intentionally unchanged:

```yaml
production:
  block_severity:
    - high
  dependency_scopes:
    - runtime
  missing_external_evidence: review
  severity_conflict: review
  cve_identity_conflict: review
  telegraph_failure: review
```

This policy blocks `high` runtime dependency findings. It does not list `critical` in `block_severity`. Unknown fields, malformed values, duplicate YAML keys, and empty required arrays are rejected by the Limen policy parser. `limen.yaml` is only a fallback when `limen.yml` is absent.

## Decision Semantics

- `PASS`: the workflow succeeds. Available evidence supports proceeding under policy. This is not a claim of universal security.
- `HOLD`: the workflow fails. Repository evidence matched a blocking policy condition.
- `REVIEW`: the workflow fails. Evidence is uncertain, missing, conflicting, malformed, unavailable, or otherwise unresolved.

Setup and configuration failures are not `REVIEW`; they stop the Action without fabricating a release decision.

## Reproduce The Sequence

The final demo branch is patched at `lodash@4.18.1`. Use a disposable branch or the existing PR history to reproduce the controlled sequence. Do not leave the final branch vulnerable.

1. Configure the secret and variable above.
2. On a disposable PR branch, install the vulnerable fixture with `npm install lodash@4.17.20 --save-exact`.
3. Commit and push the changed `package.json` and `package-lock.json` to trigger the `pull_request` workflow.
4. Inspect the failed Limen job and its `HOLD` annotation.
5. Replace the fixture with `npm install lodash@4.18.1 --save-exact`.
6. Commit and push the patched state to trigger the workflow again.
7. Inspect the successful Limen job and its `PASS` annotation.

No local Limen application or local Action build is required. The package lockfile is updated by normal npm tooling. The Action reads repository and pull request data through GitHub APIs and does not checkout the target repository.

## Proof

R0 is historical evidence from earlier Action revisions. P9 is the fresh canonical validation. All entries are controlled demo evidence.

| Proof | Decision | Dependency | Action revision | Telegraph | Run |
|---|---|---|---|---|---|
| Historical R0 HOLD | `HOLD` | `lodash@4.17.20` | `7a5604433449dc03e4eff0e2ca6f6f6269425963` recorded by evidence | 5 requests / `$0.05` recorded by evidence | [33654301781](https://github.com/kaelah971/limen-demo/actions/runs/33654301781) |
| Historical R0 PASS | `PASS` | `lodash@4.18.1` | Not recorded | 0 requests / `$0.00` recorded by evidence | [33655468552](https://github.com/kaelah971/limen-demo/actions/runs/33655468552) |
| [Fresh P9 HOLD](evidence/p9/fresh-hold.md) | `HOLD` | `lodash@4.17.20` | `0fd2494ee5390e12b7ec8a287aeb5bb7db0caf82` | Not exposed by public check output | [33883733362](https://github.com/kaelah971/limen-demo/actions/runs/33883733362) |
| [Fresh P9 PASS](evidence/p9/fresh-pass.md) | `PASS` | `lodash@4.18.1` | `0fd2494ee5390e12b7ec8a287aeb5bb7db0caf82` | Not exposed by public check output | [33884426709](https://github.com/kaelah971/limen-demo/actions/runs/33884426709) |
| [Fresh P14 HOLD](evidence/p14/judge-hold.md) | `HOLD` | `lodash@4.17.20` | `a91d36bfe8eaab5d95f791e39449878239bf948d` | 5 requests / `$0.05` known | [33958836557](https://github.com/kaelah971/limen-demo/actions/runs/33958836557) |
| [Fresh P14 PASS](evidence/p14/judge-pass.md) | `PASS` | `lodash@4.18.1` | `a91d36bfe8eaab5d95f791e39449878239bf948d` | 0 requests / `$0.00` known | [33959096100](https://github.com/kaelah971/limen-demo/actions/runs/33959096100) |

Fresh P9 runs used the current Engine variable and `usage-class: demo`. Public GitHub output exposed the final decision and job status but did not expose policy version, decision counts, evaluated or skipped CVEs, Telegraph request counts, costs, Miner names, latency, or reason codes. Those values are not inferred from R0.

The fresh HOLD run's job status is failed because `HOLD` intentionally fails the workflow. The fresh PASS run's job status is successful. The fresh HOLD job is [101058345652](https://github.com/kaelah971/limen-demo/actions/runs/33883733362/job/101058345652), and the fresh PASS job is [101060624627](https://github.com/kaelah971/limen-demo/actions/runs/33884426709/job/101060624627).

## Historical R0 And P9

The files under `evidence/r0/` are preserved unchanged. They describe earlier validation and retain their original Action references. New canonical P9 metadata is under [`evidence/p9/`](evidence/p9/). The repository does not claim that an old Action revision is current, that a revoked PASS receipt is active, or that the demo represents production operation.

The P9 package also records the current setup contract, reproducibility steps, live run links, and fields unavailable from public GitHub output. No P9 receipt was published.
