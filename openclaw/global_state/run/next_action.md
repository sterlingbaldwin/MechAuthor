next_agent: orchestrator
task: select_next_action
reason: bootstrap
chapter: 0
scene: 0
read_files:
  - <STATE_ROOT>/run/story_state.md
write_files:
  - <STATE_ROOT>/run/next_action.md
  - <STATE_ROOT>/run/run_log.md
