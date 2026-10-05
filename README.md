# pstack-copilot

GitHub Copilot CLI adaptation of [pstack](https://github.com/cursor/plugins/tree/main/pstack), originally created by Lauren Tan. It builds on [Michael Denyer's pstack-claude port](https://github.com/michael-denyer/pstack-claude), adding Copilot-specific skill guidance, routing instructions, and custom-agent setup while preserving upstream attribution and licenses.

Tell `poteto-mode` your goal and it will guide the work through the appropriate pstack workflow. Use it for non-trivial tasks; Copilot CLI handles tool use, models, and delegation according to its own runtime.

For concurrency bugs and invariants that tests cannot reach, see the separate [agent-formal-verify](https://github.com/michael-denyer/agent-formal-verify) plugin, which adds TLA+ model checking and Lean proofs.

## Install

### GitHub Copilot CLI

Clone this repository and register its shared skills directory:

```shell
git clone https://github.com/thawee/pstack-copilot.git ~/.copilot/pstack-copilot
copilot skill add ~/.copilot/pstack-copilot/plugins/pstack/skills
```

Register the two pstack custom agents:

```shell
mkdir -p ~/.copilot/agents
ln -s ~/.copilot/pstack-copilot/plugins/pstack/agents/poteto-agent.md \
  ~/.copilot/agents/poteto-agent.agent.md
ln -s ~/.copilot/pstack-copilot/plugins/pstack/agents/comment-sicko.md \
  ~/.copilot/agents/comment-sicko.agent.md
```

Add this line to `~/.copilot/copilot-instructions.md` so Copilot uses the pstack coordinator and translates Claude-specific instructions for Copilot:

```text
@pstack-copilot/copilot-instructions.md
```

Keep any existing instructions in that file. Restart Copilot CLI after adding the custom agents or changing instructions. In a running session, reload skills with `/skills reload`.

Start a non-trivial task with:

```text
Use /poteto-mode to fix the search filter resetting when I change pages.
```

This is a skills-and-instructions adaptation, not a native Copilot plugin. Copilot uses its own models and agent orchestration; Claude-specific hooks, model routing, and tool calls do not automatically carry over. Read the [Copilot tool mapping](plugins/pstack/skills/poteto-mode/references/copilot-tools.md) for supported equivalents and limitations.

### Other runtimes

The Claude Code, Codex, and Pi installation instructions are maintained by the upstream [pstack-claude project](https://github.com/michael-denyer/pstack-claude). This repository's documented setup and adaptation target is GitHub Copilot CLI.

## Getting started

[Other playbooks](plugins/pstack/skills/poteto-mode/SKILL.md#playbooks) cover planning, features, refactoring, performance issues, investigations, prototypes, PR maintenance, shipping, and longer projects.

![pstack coordinates bounded specialist work, integrates useful changes, verifies the result, and reports the evidence. Copilot CLI uses its own agent and tool behavior with the shared pstack skills.](assets/pstack-overview.png)

## Details

- [Skills and slash commands](docs/reference.md#slash-commands)
- [Runtime setup](docs/reference.md#runtime-support)
- [Models and dependencies](docs/reference.md#configuration-and-dependencies)
- [Maintenance and port scope](docs/reference.md#maintenance)

## Data handling

pstack has no server or telemetry. Anything its skills ask your agent to read, including session transcripts, goes to your model provider. Scripts run locally, and PR tools use your GitHub CLI login.

## Contributing

Contributions to the Copilot CLI adaptation are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for checks and guidance on upstream-derived changes. Report vulnerabilities privately as described in [SECURITY.md](SECURITY.md).

## License

This repository is MIT-licensed. It preserves the original pstack attribution to Lauren Tan, the pstack-claude port attribution to Michael Denyer, and the Cursor attribution for imported cursor-team-kit skills. Copilot-specific changes are maintained in this repository. See [LICENSE](LICENSE), [LICENSE-cursor-team-kit](LICENSE-cursor-team-kit), and [NOTICE.md](NOTICE.md) for copyright and provenance details.
