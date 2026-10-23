@AGENTS.md

<!--
This file exists only so Claude Code picks up AGENTS.md.

Recent Claude Code versions read AGENTS.md directly, but only when no CLAUDE.md
is present at or above the working directory — and support is unavailable on
older versions, on third-party providers such as Amazon Bedrock, and with
telemetry or hooks disabled. This one-line import makes AGENTS.md reach every
session regardless: https://code.claude.com/docs/en/memory

Put shared agent instructions in AGENTS.md — the vendor-neutral convention that
Cursor, Copilot, Codex and others read directly. Only genuinely Claude-specific
instructions belong in this file, below the import.

A symlink would also work, but creating one on Windows needs Administrator
privileges or Developer Mode, so the import is the portable choice for this team.
-->
