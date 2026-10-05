# Copilot CLI tool mapping for pstack

pstack skills share one skills tree, but their workflows name Claude Code tools, agent types, model aliases, and configuration paths. On Copilot CLI, use this mapping instead of copying those names literally.

## Tool actions

| pstack / Claude action | Copilot CLI equivalent |
| --- | --- |
| Read, search, or list files | Use the available file-reading, search, and listing tools. |
| Create, edit, or delete files | Use the available file-editing tools. |
| Run a shell command | Use the shell tool; follow the session's permission prompts. |
| Fetch a URL or search the web | Use the available web tools. |
| Invoke a skill (`Skill`, `/command`) | Use the skill by name, for example `/poteto-mode`; request it explicitly if it was not selected automatically. |
| Dispatch an agent (`Agent` / `Task`) | Delegate through Copilot CLI's subagent orchestration. Name the Copilot custom agent when the workflow requires one. Do not pass Claude-only fields such as `subagent_type`, `run_in_background`, or Claude model aliases. |
| Dispatch several agents | Use independent Copilot subagent assignments when parallelism is useful and available. Give each writer a disjoint scope; the coordinator integrates and verifies all results. |
| Ask a fixed-choice question (`AskUserQuestion`) | Ask the user conversationally only when a genuine decision is needed. |
| Track tasks (`TaskCreate`, `TaskUpdate`, `TodoWrite`) | Use Copilot's available task tracking. If none is available, keep a concise `tasks/todo.md` checklist in the workspace. |

## Delegation

Use Copilot custom agents by their CLI IDs, without Claude's `pstack:` namespace:

- `poteto-agent` follows the pstack style. Give it a fresh, bounded assignment and require it to read the `poteto-mode` skill before working.
- `comment-sicko` performs the no-comments review and reports only.
- `explorer` and `researcher` are suitable for read-only investigation when available.
- `worker` is suitable for one scoped implementation task when available.

Copilot decides which models and execution modes its agents use. Do not translate pstack's Claude model names, reasoning levels, or background flags into guessed Copilot settings. If a required custom agent is unavailable, use a suitable available agent or complete the work directly, and report the limitation.

## Runtime configuration

- Personal skills live in `~/.agents/skills/` or `~/.copilot/skills/`.
- Personal custom agents live in `~/.copilot/agents/` as `.agent.md` files.
- Personal instructions live in `~/.copilot/copilot-instructions.md` and may include this installation's `copilot-instructions.md`.
- Skills added during a live session can be refreshed through the skill manager. Restart Copilot CLI after adding custom agents.
- Use Copilot's model selector, custom-agent browser, instruction-source viewer, and skill manager for their respective settings.

## Workflow limits

The shared skills are discoverable on Copilot, but workflows that depend on a Claude-only driver, hook, plugin command, transcript layout, model selector, or tool are not automatically portable. Use the Copilot equivalent only when verified; otherwise skip that substep and state the limitation. Skills-only discovery does not install the Claude Code or Codex routing hooks.
