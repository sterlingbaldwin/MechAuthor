next_agent: orchestrator
task: select_next_action
reason: bootstrap
read_files:
  - /vol/projects/mechauthor/run/story_state.md
write_files:
  - /vol/projects/mechauthor/run/next_action.md
  - /vol/projects/mechauthor/run/run_log.md
