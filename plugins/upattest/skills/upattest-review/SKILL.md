---
name: upattest-review
description: Ask a verified human professional to review the current change (or a named file) through UpAttest, within a budget the person states.
argument-hint: "[what to focus on] [max $ total]"
disable-model-invocation: true
---

The person asked for a human review through UpAttest. Their words: "$ARGUMENTS"

Follow the `request-human-attestation` skill from this plugin, starting at step 2. In short:

1. Call `upattest_check_connection` and mention the account and environment.
2. Work out what to review. With no file named, use the current change: the staged and unstaged diff against the
   base branch (`git diff` plus `git diff --staged`; if both are empty, the last commit). Show the person the list of
   files and the size, and name anything you will leave out (generated files, lockfiles, secrets).
3. Pick the attestation type from the content and the focus they gave (security wording → rubric `code.security`;
   otherwise `software.change_review` for code, or the matching licensed type for documents and calculations).
4. If they gave a maximum, use it as `max_total_cents` (it includes the 8% fee). If they did not, ask for one before
   proposing anything.
5. Ask once for consent to share exactly that material, unless their words already gave it. Then register it,
   find reviewers with `size_bytes`, offer two or three options with totals, and continue with the proposal,
   waiting and funding only within the limits in the skill.

Do not merge, deploy or mark anything approved because a review was requested or completed.
