# pstack on GitHub Copilot CLI

For non-trivial tasks, use the `/poteto-mode` skill as the workflow coordinator. Keep simple tasks direct. Follow explicit user instructions over automatic routing.

Before applying pstack instructions that mention Claude Code tools, agents, models, or paths, read `plugins/pstack/skills/poteto-mode/references/copilot-tools.md` and translate the workflow to Copilot CLI. Do not invoke Claude-only tool names or assume Claude model aliases exist.

Use Copilot CLI custom agents `poteto-agent` for pstack-style delegated implementation and `comment-sicko` for the no-comments review. Delegate read-only research to `explorer` or `researcher`, and scoped changes to `worker`, when those agents are available. Keep each assignment bounded, avoid overlapping file edits, and verify delegated results yourself.

Request `/poteto-mode` explicitly if automatic skill selection does not load it.
