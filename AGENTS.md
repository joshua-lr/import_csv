# AGENTS.md

## Issue and branch

1. Start with a GitHub issue. Reuse an existing issue when it covers the work. Describe the problem, expected behavior, and acceptance criteria. For a bug, include steps to reproduce it.
2. Run `git status --short --branch` before editing and preserve unrelated work. Start from the repository's default branch, updated from its remote when one is configured.
3. Use one branch per issue, named `feat/42-short-description` or `fix/42-short-description`. Keep commits focused and use imperative subjects that describe the change.
4. If the repository has no GitHub remote, record the acceptance criteria locally and do the branch and test work. Report that the issue and pull request still need a GitHub repository.

## Test-driven Rust development

1. **Red.** Add a test for the expected behavior. For a bug, reproduce it with a regression test. Run `cargo test <test_name>` and confirm it fails for the expected reason.
2. **Green.** Make the smallest implementation change that satisfies the test. Rerun the targeted test.
3. **Refactor.** Improve names and structure while preserving behavior. Rerun the relevant tests after refactoring.
4. Put unit tests near the code in a `#[cfg(test)]` module. Use `tests/` for public API and CLI behavior. Keep fixtures small and deterministic. For CSV changes, cover the relevant quoting, header, or malformed-input case when it affects the issue.

## Checks before review

Run the repository's documented CI checks. For a standard Cargo workspace, start with:

```sh
cargo fmt --all -- --check
cargo clippy --workspace --all-targets -- -D warnings
cargo test --workspace
git diff --check
```

Run any feature combinations required by CI. Record the checks you ran and report failures or unavailable checks in the pull request.

## Pull request and merge

1. Review the diff for scope and confirm it satisfies the issue's acceptance criteria.
2. When authorized to push and open a pull request, push the issue branch and target the default branch. Summarize the behavior change, include verification results, and add `Closes #42` with the actual issue number if merging completes that issue. Use a draft while work is in progress.
3. Address review feedback on the same branch and rerun affected checks. Merge only when authorized and after required checks and reviews pass. Follow the repository's merge policy.
