# PR Review Lab

A small lab for reviewing pull requests, fixing broken Markdown links, and deciding when a change is ready to approve.

- **Review.** GitHub Actions checks relative Markdown links when a pull request opens or changes. The run logs show `hold` or `eligible` for that commit.
- **Fix.** `--fix` commits a link repair when exactly one file matches the target name. The default policy limits repairs to `examples/*.md` on branches in this repo.
- **Approve.** The base branch’s [policy](.review-policy.json) starts in observe mode. To submit a GitHub approval, switch it to `approve` and use `--codex --approve` with an authenticated Codex CLI and a GitHub reviewer account other than the PR author’s.

## Try it

With Python 3.10+ and GitHub CLI signed in, run from the repo:

```sh
python3 review.py plattenschieber/pr-review-lab 1
```

[Demo PR #1](https://github.com/plattenschieber/pr-review-lab/pull/1) shows the broken link, repair commit, and both review runs. Add `--codex` to include AI review of the diff.
