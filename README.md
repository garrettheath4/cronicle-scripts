# Cronicle Scripts

A collection of automation scripts designed to run on a schedule via [Cronicle V2 Python](https://github.com/jhuckaby/Cronicle), cron, or other job schedulers.

## Scripts

### todoist_auto_today.py

Automatically sets all Todoist tasks with the `@today` label to be due today. This enables a workflow where you can quickly tag tasks with `@today` and have them automatically scheduled for the current date.

**Features:**
- Finds all tasks with the `@today` label
- Sets their due date to today
- Preserves recurring task patterns (e.g., "every day" tasks keep their recurrence)

## Requirements

- Python 3.9+
- `requests`
- `tzdata`

## Installation

```bash
pip install requests tzdata
```

## Configuration

| Environment Variable | Required | Default            | Description |
|----------------------|----------|--------------------|-------------|
| `TODOIST_TOKEN`      | Yes      | -                  | Your Todoist API token ([get one here](https://todoist.com/app/settings/integrations/developer)) |
| `TZ`                 | No       | `America/New_York` | Timezone for determining "today" |

## Usage

```bash
# Basic usage
TODOIST_TOKEN=your_api_token python3 todoist_auto_today.py

# With custom timezone
TZ=America/Los_Angeles TODOIST_TOKEN=your_api_token python3 todoist_auto_today.py
```

### Scheduled Execution

For best results, schedule this script to run periodically (e.g., every hour or at the start of each day).

**Cron example (every hour):**
```bash
0 * * * * TODOIST_TOKEN=your_token /usr/bin/python3 /path/to/todoist_auto_today.py
```

## License

MIT
