# Agent Team: Specs

A multi-agent team that defines product work: it turns a request into an
initiative with its specs (PRD, TRD, PLAN) and a phased roadmap of roadmap
items, recorded in [VisionStudio](https://github.com/ProductBuildersHQ/visionstudio).
It defines work for an implementation team to execute; it does not write code.

Definitions use the [multi-agent-spec](https://github.com/plexusone/multi-agent-spec)
format.

## Agents

| Agent | Role |
|---|---|
| [`spec-writer`](specs/agents/spec-writer.md) | Creates the initiative, writes its specs and roadmap, and records them in VisionStudio |

## Layout

```
specs/                 # source of truth (multi-agent-spec)
├── plugin.json        # plugin metadata
├── agents/            # agent definitions (Markdown with YAML frontmatter)
└── deployments/       # generation targets
plugins/
└── claude/            # generated Claude Code plugin; do not edit
```

## Claude Code

`plugins/claude/` is generated from `specs/` with
[assistantkit](https://github.com/plexusone/assistantkit). Regenerate it after
changing a spec:

```sh
go run github.com/plexusone/assistantkit/cmd/assistantkit@v0.15.0 generate --specs=specs --target=local
```

To use the agents in a project, copy them into its `.claude/agents/`:

```sh
cp plugins/claude/agents/*.md /path/to/project/.claude/agents/
```

## Requirements

The agents use the `visionstudio` MCP server (`visionstudio mcp`), pointed at
a local VisionStudio database or a VisionStudio Cloud organization. Register
it under the name `visionstudio`: the agents' tool lists name its tools as
`mcp__visionstudio__<tool>`.

## License

MIT. See [LICENSE](LICENSE).
