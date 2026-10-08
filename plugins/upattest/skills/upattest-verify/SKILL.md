---
name: upattest-verify
description: Check whether an UpAttest attestation exists for a file, a sha256 hash or an attestation id, and whether its signatures verify.
argument-hint: "[file path | sha256 | attestation id]"
disable-model-invocation: true
---

Verify: "$ARGUMENTS"

- An attestation id (starts with `att_`): call `upattest_verify` with the id.
- A 64-character hex string: call `upattest_verify` with it as the artifact hash.
- A file path: compute its SHA-256 (for a diff, normalize line endings to LF first) and verify by hash. Say which
  bytes you hashed.

Report for each result: whether it is valid or revoked, the verdict when the record is public, who signed it, when,
and the record link. A private record shows only that it exists and its status.

Say plainly that a record covers only that exact artifact. A different version, even a small edit, is not covered.
A valid record is a professional's signed opinion, not permission to merge, deploy or act.
