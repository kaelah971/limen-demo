# R0 Validation Summary

This is a sanitized HOLD-to-PASS record for the controlled same-repository PR. No secrets, wallet keys, payment signatures, raw API responses, or raw Telegraph responses are stored.

## Timeline

1. Vulnerable dependency introduction: Lodash `4.17.20`, commit `0143583f45dd5147fe396a776bad16bbae5bdf6a`.
2. Live HOLD validation: run https://github.com/kaelah971/limen-demo/actions/runs/33654301781, head `84bda870ae3b90713f3d3a01a4b6a50f647d98c3`.
3. Patched dependency: Lodash `4.18.1`, commit `394d98d9d8aac8c02134abda6db4116b3f64c7ee`.
4. Live PASS validation: run https://github.com/kaelah971/limen-demo/actions/runs/33655468552, head `394d98d9d8aac8c02134abda6db4116b3f64c7ee`.

## HOLD

- Overall decision: `HOLD`
- Policy: `LP-fde4ac5cdba2`
- Telegraph: `5` real `CVE_LOOKUP` requests
- Telegraph cost: `$0.05`
- Miner: `PREFLIGHT Infrastructure Signals`

## PASS

- Overall decision: `PASS`
- Policy: `LP-fde4ac5cdba2`
- Telegraph: `0` requests
- Telegraph cost: `$0.00`
- Reason: No blocking dependency vulnerability was introduced by this pull request.

## Scope

- Pull request: https://github.com/kaelah971/limen-demo/pull/1
- PR remains open and unmerged.
- Workflow and `limen.yml` were not changed for the patch result.
