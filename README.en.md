# Fleet

[简体中文](README.md) | English

A skill for bounded multi-agent collaboration in Codex: **delegate only when it is worthwhile, choose models, reasoning effort, and context to fit the task, and keep integration and acceptance with the lead agent.**

Fleet is an instruction package, not a new agent runtime. It does not install services, connect to external paid models, create background monitors, or grant additional permissions.

## What it helps with

- **Delegate for a reason, not just for parallelism.** Keep tightly coupled decisions with the lead agent. Delegate work that can be handled independently and verified.
- **Avoid inheriting the most expensive settings by default.** Choose the model, reasoning effort, and input scope separately. Account for implementation, handoff, verification, and rework costs.
- **Assign clear ownership of shared resources.** Files, browser sessions, and databases need explicit write ownership. Confirm that the previous worker has stopped writing before handing over control.
- **Collect evidence, not just a completion message.** Subagents return actual outputs and supporting evidence; the lead agent integrates and verifies them in proportion to the risk.
- **Treat long-running work as coordination, not a requirement to use more agents.** Multi-stage tasks need continuity, but do not require filling every concurrency slot or adding a governance process.

## Installation

Copy the entire `skills/fleet` folder into a skill directory used by your Codex installation. For example:

- Personal use: `~/.agents/skills/fleet`
- Project-only use: `<project>/.agents/skills/fleet`

If a skill with the same name already exists, compare and back it up before replacing it. Include `references/core.md`: the entry point depends on this bundled guide.

You can also ask Codex:

> Install skills/fleet from https://github.com/Woltziara/fleet-skill.

Follow the [current Codex documentation](https://learn.chatgpt.com/docs/build-skills) for installation and skill discovery in your environment.

## Usage

Invoke the skill explicitly:

> Use $fleet to complete this task. Decide which work is worth parallelizing, choose suitable subagent models and reasoning effort, retain overall ownership, and integrate and verify the results.

You can also ask to “use Fleet” or “coordinate a team of agents.” In environments that support implicit skill selection, Fleet also applies to tasks spanning multiple substantive stages where intermediate feedback changes what happens next.

**If subagents are unavailable or delegation is not permitted, the lead agent continues with the work it can do. It must not pretend that delegation occurred.** Tool names, concurrency limits, models, and parameters depend on the host environment.

The bundled skill instructions are currently written in Chinese. This README provides an English introduction and usage guide; it is not a separate English translation of the skill itself.

## End-of-task usage report

Fleet reports which model handled each subtask, its reasoning effort, the outcome, and available input, output, and total token counts, with a summary by model. The inventory includes failed runs, rework, and nested delegation. Lead-agent overhead is shown separately to avoid double-counting parent and child usage.

Exact counts depend on attributable usage records from the host. Missing values are marked as unavailable, with a known-usage subtotal and coverage count rather than a misleading complete total. Quota percentages, budgets, and model estimates are not actual usage. A snapshot cannot include tokens for the final response that has not yet been generated.

## Contents

```text
skills/fleet/
├── SKILL.md
├── agents/openai.yaml
└── references/core.md
```

- `SKILL.md`: Codex-specific coordination guidance, model selection, and invocation constraints.
- `references/core.md`: When to delegate, shared-resource ownership, costs, stopping or reassigning work, and integration.
- `agents/openai.yaml`: Display metadata and the default invocation prompt.

## Scope and limitations

This is a portable release of a personal workflow. The shared coordination guide is bundled in the repository, private instruction paths have been removed, and specific model names have been replaced with capability tiers. No private conversations, project data, credentials, or local configuration are included.

Fleet does not promise a fixed percentage of cost savings or consistent results across every model, task, and host. Evaluate quality, cost, and benefits using actual deliveries and rework. This project is not an official OpenAI release and is not endorsed by OpenAI.

## License

[MIT](LICENSE) © 2026 [Woltziara](https://github.com/Woltziara)
