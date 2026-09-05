# P14 Hardened Judge Mode

**CONTROLLED JUDGE-MODE VALIDATION**

P14 used the current hardened Limen Action and the existing controlled demo PR:

```text
kaelah971/limen@a91d36bfe8eaab5d95f791e39449878239bf948d
        |
        v
lodash@4.17.20 -> real GitHub evidence -> real paid Telegraph -> HOLD
        |
        v
lodash@4.18.1 -> fresh GitHub evidence -> no relevant finding -> PASS
```

## Fresh Sequence

| State | Commit | Dependency | Decision | Telegraph | Run |
|---|---|---|---|---|---|
| Vulnerable | `a0b41e6447e4924efd9ac710811d0a79f56be8c5` | `lodash@4.17.20` | `HOLD` | 5 requests / `$0.05` known | [33958836557](https://github.com/kaelah971/limen-demo/actions/runs/33958836557) |
| Patched | `6094dcc71b69df24c2b4bde0daa22b82c5930e42` | `lodash@4.18.1` | `PASS` | 0 requests / `$0.00` known | [33959096100](https://github.com/kaelah971/limen-demo/actions/runs/33959096100) |

Detailed records:

- [Fresh P14 HOLD](judge-hold.md)
- [Fresh P14 PASS](judge-pass.md)
- [Fresh P14 PR](https://github.com/kaelah971/limen-demo/pull/1)

The vulnerable run used five real paid `CVE_LOOKUP` requests. Safe output
reported Base Sepolia (`eip155:84532`), the `exact` payment scheme, the safe
Miner name, and `$0.01` per request. The raw x402 asset payload, amounts,
signatures, signed payloads, and private key are not published.

P13 payment limits, trusted origins, redirect rejection, and secret redaction
were active in both evaluations. The final demo branch remains patched.

## Evidence Boundaries

- R0 is historical validation and remains unchanged.
- P9 is the previous reproducibility validation and remains unchanged.
- P14 is this fresh hardened Judge-Mode sequence.
- The workflow uses `usage-class: demo` and only `contents: read`.
- No checkout, `pull_request_target`, ledger configuration, or receipt publication was added.
- Fresh P14 GitHub runs were not persisted to the hosted ledger because no public Action-reachable ledger endpoint is configured.
- Hosted ledger and receipt infrastructure were live-validated separately in P5/P6; those evidence chains are not merged with these P14 runs.
- This demo is controlled validation, not external adoption evidence.
