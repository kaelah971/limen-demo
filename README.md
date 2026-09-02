# Limen Demo

This public repository is a controlled validation fixture for the Limen GitHub Action.

The base branch intentionally has no vulnerable dependency. The validation PR adds Lodash `4.17.20`, which should produce a real `HOLD` when the configured Base Sepolia Telegraph evidence is available. Updating that PR to Lodash `4.17.21` should produce a real `PASS`.

The workflow has `contents: read`, does not check out the pull request, and pins Limen to immutable commit `697aa46256935a52ff1490258470b8d1ceab1fb8`.

Repository configuration required for the paid path:

- Variable `TELEGRAPH_ENGINE_URL`: the validated Telegraph Engine `/v1/ask` endpoint.
- Secret `LIMEN_TELEGRAPH_PRIVATE_KEY`: a dedicated funded Base Sepolia test wallet key.

No production credentials belong in this repository.
