# File I/O Rules

- Read only files listed in the task context.
- Write only files listed in the task context.
- If required input is missing, emit a structured failure note instead of guessing.
- Never overwrite unrelated sections in shared files.
- Preserve existing Markdown structure unless task requires schema migration.
