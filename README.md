# merge-ready

Human-gated merge readiness for agent workflows.

`merge-ready` uses task-routed OpenCode models as read-only second opinions across branch diffs, security, documentation, conflicts, CI, and frontend design. Every finding returns to the active host session for evaluation before any fix, commit, push, or PR update. The skill never merges a PR.

## Install

```bash
npx skills add https://github.com/vizuh/merge-ready --skill merge-ready
```

## What it does

1. Inspects the repository contract, feature branch, worktrees, PR, related open work, complete diff, and merge-conflict forecast.
2. Routes isolated read-only review axes across code, reasoning, free NVIDIA Nemotron, and documentation models; Kimi K3 is reserved for frontend/design work.
3. Verifies and reports every finding, then stops for a human decision.
4. Applies only approved fixes, checkpointing base integration and review repairs.
5. Runs the repository's own CI-equivalent checks.
6. Pushes and opens or updates a PR only after explicit authorization.
7. Stops for human review and merge.
8. After GitHub confirms the merge, prunes only the verified clean local branch/worktree.

## Requirements

- Git
- GitHub remote and authenticated GitHub CLI
- OpenCode with access to the task-routed models declared in the skill, or user-approved active replacements
- A host agent capable of returning findings and waiting for explicit evaluation

The OpenCode invocation disables external plugins and denies every tool. It reviews only secret-screened attachments prepared by the host. Git and native/remote CI remain the sources of truth.

Current preferred routing uses `opencode/north-mini-code-free` for general diff
and CI review, `opencode-go/grok-4.5` for security,
`opencode/deepseek-v4-flash-free` for documentation,
`opencode/nemotron-3-ultra-free` for NVIDIA conflict review, and
`opencode-go/kimi-k3` only for conditional frontend/design review. The skill
verifies availability and obtains destination-specific authorization before
sending non-public material.

## Hard boundaries

- No automatic merge, approval, force-push, issue closure, or remote-branch deletion.
- No silent remediation.
- No secret-bearing files sent to OpenCode.
- No cleanup before GitHub-confirmed merge.
- No forced worktree or branch deletion.

The [skill contract](skills/merge-ready/SKILL.md) is the authoritative procedure.

## Design references

This is an original Vizuh workflow. It was informed by, but does not copy:

- [every-app/open-seo — `merge-ready`](https://github.com/every-app/open-seo/tree/main/.agents/skills/merge-ready): whole-branch review, verified findings, checkpoints, and human-final merge.
- [neolabhq/context-engineering-kit — `git-worktrees`](https://github.com/neolabhq/context-engineering-kit/tree/main/plugins/git/skills/git-worktrees): worktree isolation, inspection, and safe cleanup. The repository's current skill name differs from the older `git:merge-worktree` listing.
- [mattpocock/skills — `resolving-merge-conflicts`](https://github.com/mattpocock/skills/tree/main/skills/engineering/resolving-merge-conflicts): resolve from both sides' intent and primary sources.
- [github/awesome-copilot — `memory-merger`](https://github.com/github/awesome-copilot/tree/main/skills/memory-merger): propose, stop, evaluate, then mutate.
- [expo/skills — `eas-workflows`](https://github.com/expo/skills/tree/main/plugins/expo/skills/eas-workflows): discover current CI truth and validate against authoritative sources. The current repository path differs from the older `expo-cicd-workflows` listing.
- [addyosmani/agent-skills — `ci-cd-and-automation`](https://github.com/addyosmani/agent-skills/tree/main/skills/ci-cd-and-automation): CI feedback loops and explicit quality gates.

## License

MIT © 2026 Vizuh OÜ
