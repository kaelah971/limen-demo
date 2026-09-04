# P9 Fresh HOLD Evidence

This file records sanitized metadata from the fresh canonical P9 HOLD validation. It is controlled demo evidence, not production adoption or external-user evidence. No raw GitHub responses, Telegraph responses, payment signatures, wallet material, private keys, or tokens are stored.

- Run: https://github.com/kaelah971/limen-demo/actions/runs/33883733362
- Job: https://github.com/kaelah971/limen-demo/actions/runs/33883733362/job/101058345652
- Pull request: https://github.com/kaelah971/limen-demo/pull/1
- Event: `pull_request`
- Branch: `demo/lodash-vulnerable`
- Base commit: `2f2cd0bbcffd00c562c82d834fe2669afc3352f7`
- Head commit: `71e9e6106b00a4b3301adfe45e768aaa25b9d9ce`
- Action ref: `kaelah971/limen@0fd2494ee5390e12b7ec8a287aeb5bb7db0caf82`
- Usage class: `demo`
- Dependency: `lodash@4.17.20`
- Scope: `runtime`
- Telegraph Engine URL: `http://13.237.89.59:7044/engine/v1/ask`
- Expected network: Base Sepolia default; the run log does not expose a normalized chain identifier
- Overall decision: `HOLD`
- Job status: failed, as HOLD intentionally fails the workflow
- Action annotation: `Limen: HOLD. Evidence is sufficient and the active policy blocks at least one dependency.`
- Policy version: not exposed by the public check-run output
- Decision counts: not exposed by the public check-run output
- Evaluated CVEs: not exposed by the public check-run output
- Skipped CVEs: not exposed by the public check-run output
- Telegraph request count: not exposed by the public check-run output
- Telegraph cost: not exposed by the public check-run output
- Telegraph Miner: not exposed by the public check-run output
- Latency: not exposed by the public check-run output
- Reason code: not exposed by the public check-run output
- Receipt: none published; receipt publication is not automatic from the Action

The repository policy blocks `high` runtime dependency findings. This run's public output confirms the HOLD decision but does not publish a CVE identifier or raw evidence details. Those values are intentionally not inferred from R0.
