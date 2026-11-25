# PR Review Lab

Review a GitHub pull request, repair supported findings, and decide whether the current revision is eligible for approval. The repository's base branch defines the policy.

## Run a review

GitHub Actions runs the built-in review when a pull request opens or changes. The job logs show the findings and decision for the reviewed commit. Run the CLI to add Codex, commit a repair, or submit a policy-authorized approval.

Install Python 3.10+ and GitHub CLI. Sign in with `gh auth login` and run these commands from a trusted checkout of the lab.

```sh
python3 review.py OWNER/REPO PR_NUMBER
python3 review.py OWNER/REPO PR_NUMBER --fix
python3 review.py OWNER/REPO PR_NUMBER
```

The built-in reviewer checks simple relative Markdown links. The steward can repair a link when the intended file has a unique matching name. It commits only matching paths to a branch in the same repo and GitHub rejects the commit if the branch has moved. Rerun after a repair to evaluate the new revision. Ambiguous links and Codex findings are for a person to resolve.

Add `--codex` to include a review of the diff through your authenticated Codex CLI. Use it only where your organization allows sending the diff to the configured model provider. Codex is optional for the built-in review and repair. A Claude subscription is unnecessary.

## Approval

`.review-policy.json` defines eligible paths, repair paths, and any required GitHub checks by name and app slug. The current policy is in observe mode and allows example documentation changes. Drafts, forks, conflicts, findings, and missing required checks hold the decision.

To enable native GitHub approvals, set `mode` to `approve` on the base branch and run `python3 review.py OWNER/REPO PR_NUMBER --codex --approve` from a GitHub account authorized to review the PR. GitHub requires a different account from the PR author. The approval is attached to the reviewed commit. GitHub branch rules still govern whether the PR can merge and whether a new commit dismisses an earlier approval.

## End-to-end lab

Add `examples/walkthrough.md` with a link to `old/guide.md`. Open a PR. Review should flag the link, repair should change it to `guide.md`, and a fresh review should find the repaired revision eligible in observe mode.
