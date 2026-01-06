# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains automation scripts designed to run on a schedule (e.g., via Cronicle, cron, or systemd timers). Currently it has a single Todoist automation script.

## Running Scripts

```bash
# Run the Todoist auto-today script (requires TODOIST_TOKEN env var)
TODOIST_TOKEN=your_token python3 todoist_auto_today.py

# Optional: Set timezone (defaults to America/New_York)
TZ=America/Los_Angeles TODOIST_TOKEN=your_token python3 todoist_auto_today.py
```

## Dependencies

- Python 3.9+ (uses `zoneinfo` module)
- `requests` library
- `tzdata` package (for timezone support)

Install with: `pip install requests tzdata`

## Architecture

**todoist_auto_today.py**: Fetches all Todoist tasks with the `@today` label and sets their due date to today. Handles recurring tasks specially by preserving the recurrence pattern string rather than setting a fixed date.

Key design decisions:
- Uses functional programming style (no classes)
- Logs at DEBUG level for troubleshooting scheduled runs
- Continues processing remaining tasks if one update fails
