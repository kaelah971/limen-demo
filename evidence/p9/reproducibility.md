# P9 Reproducibility

P9 is a fresh controlled HOLD-to-PASS sequence using the canonical Limen Action. The final demo branch remains patched at `lodash@4.18.1`.

## Verified Repository Configuration

- Secret name exists: `LIMEN_TELEGRAPH_PRIVATE_KEY`
- Variable name exists: `TELEGRAPH_ENGINE_URL`
- Variable value matches: `http://13.237.89.59:7044/engine/v1/ask`
- The private key value was never retrieved, printed, or stored.

## Reproduce

Use a disposable pull request branch rather than leaving the demo branch vulnerable:

1. Configure the secret and variable above.
2. Start from the patched fixture and run `npm install lodash@4.17.20 --save-exact`.
3. Commit and push `package.json` and `package-lock.json` to trigger the `pull_request` workflow.
4. Inspect the failed Limen job and its `HOLD` annotation.
5. Run `npm install lodash@4.18.1 --save-exact`.
6. Commit and push the patched files to trigger the workflow again.
7. Inspect the successful Limen job and its `PASS` annotation.

The workflow requires only `contents: read`, does not checkout or execute pull request code, and does not configure ledger persistence or receipt publication.

## P9 Sequence

| State | Commit | Dependency | Result |
|---|---|---|---|
| Vulnerable | `71e9e6106b00a4b3301adfe45e768aaa25b9d9ce` | `lodash@4.17.20` | [HOLD run 33883733362](https://github.com/kaelah971/limen-demo/actions/runs/33883733362) |
| Evidence package | `342c2696bda6f0cb6a381a05bc95c86e92c56bca` | `lodash@4.17.20` | Repeat HOLD run 33884227371 |
| Patched | `074409601f081b4c66d5f331cb7c4ff5b9b5fc63` | `lodash@4.18.1` | [PASS run 33884426709](https://github.com/kaelah971/limen-demo/actions/runs/33884426709) |

## History Boundary

The existing `evidence/r0/hold-33654301781.md`, `evidence/r0/pass-33655468552.md`, and `evidence/r0/summary.md` remain unchanged. Their older Action references and recorded request data are historical and are not reused as fresh P9 values.
