# Limen Demo

This public repository is a controlled validation fixture for the Limen GitHub Action.

The base branch intentionally has no vulnerable dependency. The validation PR added Lodash `4.17.20` and produced a live `HOLD`; updating that PR to Lodash `4.18.1` produced a live `PASS`.

The workflow has `contents: read`, does not check out the pull request, and pins Limen to immutable commit `697aa46256935a52ff1490258470b8d1ceab1fb8`.

Repository configuration required for the paid path:

- Variable `TELEGRAPH_ENGINE_URL`: the validated Telegraph Engine `/v1/ask` endpoint.
- Secret `LIMEN_TELEGRAPH_PRIVATE_KEY`: a dedicated funded Base Sepolia test wallet key.

No production credentials belong in this repository.
R0 validation rerun..
R0 validation rerun after config diagnostics.
