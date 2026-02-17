# BOOTSTRAP.md

At startup:
1. Read `/vol/projects/mechauthor/openclaw/global_state/run/next_action.md`.
2. Confirm `next_agent: writer`.
3. Resolve chapter/scene target.
4. Load scene plan, chapter spec, memory context, and style guide.
5. Write only assigned prose segment.
6. Set `validation_required: true` in story state and log run.
