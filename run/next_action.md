next_agent: orchestrator
task: select_next_action
reason: bootstrap
read_files:
  - run/story_state.md
write_files:
  - run/next_action.md
  - run/run_log.md
