# anarm-tools — Claude Code marketplace

Personal marketplace with one plugin, **orchestrate**:

- Skill `orchestrate-code` — Google-style engineering change process (framing → author → presubmit → review → integration → release → learning), bypass mode by default.
- 8 subagents: **Рекс** (requirements/architecture), **Спец** (spec), **Дима** (author), **Денис** (debug), **Фил** (finance review), **Зевс** (UI review), **Ральф** (code review), **Гена** (release ops).

## Install in the terminal (global, all projects)

```text
/plugin marketplace add anarm/claude-plugin-orchestrate
/plugin install orchestrate@anarm-tools
```

(Replace `anarm/claude-plugin-orchestrate` with the actual GitHub `owner/repo` once pushed.)

Then `/orchestrate-code <task>` works in any session, and the 8 agents appear in `/agents`.

## Use in cloud sessions (claude.ai/code)

Cloud sessions do NOT read your local `~/.claude/`. To make this plugin auto-install in a repo's cloud sessions, add to that repo's `.claude/settings.json` (see `example-settings.json`):

```json
{
  "extraKnownMarketplaces": {
    "anarm-tools": {
      "source": { "source": "github", "repo": "anarm/claude-plugin-orchestrate" }
    }
  },
  "enabledPlugins": {
    "orchestrate@anarm-tools": true
  }
}
```

On session start (after workspace-trust), the marketplace is registered and the plugin auto-enabled — `/orchestrate-code` and the agents become available.

## Structure

```text
.claude-plugin/marketplace.json     # marketplace manifest
plugins/orchestrate/
  .claude-plugin/plugin.json        # plugin manifest
  skills/orchestrate-code/SKILL.md  # the skill
  agents/*.md                       # 8 subagents
```
