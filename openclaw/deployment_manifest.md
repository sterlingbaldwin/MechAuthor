# Deployment Manifest

## Workspaces to create in OpenClaw

1. `orchestrator` -> source: `openclaw/agents/orchestrator`
2. `planner` -> source: `openclaw/agents/planner`
3. `writer` -> source: `openclaw/agents/writer`
4. `continuity_editor` -> source: `openclaw/agents/continuity_editor`

## Shared state mount

Mount `openclaw/global_state` as the shared writable state volume for all agents.
Each agent should set `STATE_ROOT` to that mounted path.

## Required files in shared state

- `run/story_state.md`
- `run/next_action.md`
- `run/run_log.md`
- `seed/seed.md`
- `outline/*`
- `draft/*`
- `memory/*`
