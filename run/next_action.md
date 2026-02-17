next_agent: orchestrator
task: select_next_action
reason: bootstrap
read_files:
  - /vol/projects/MechAuthor/run/story_state.md
write_files:
  - /vol/projects/MechAuthor/run/next_action.md
  - /vol/projects/MechAuthor/run/run_log.md
