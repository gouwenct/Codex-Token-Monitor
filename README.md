# Codex Token Monitor

VS Code status bar extension for realtime Codex token monitoring.

It watches the Codex JSONL sessions folder, reads `event_msg` entries whose payload type is `token_count`, and shows:

```text
19:32  +320 (in:200 / out:120)  today:12.4k
```

## Features

- Watches `~/.codex/sessions` by default.
- Supports nested Codex session folders such as `sessions/2026/04/30/*.jsonl`.
- Shows latest request tokens, input tokens, output tokens, and today's total.
- Uses ccusage-compatible accounting: each `token_count` event is treated as a cumulative total, and usage is computed as the positive delta from the previous cumulative event in the same session file.
- Avoids double-counting repeated `token_count` events because repeated cumulative totals produce a zero delta.
- Opens a visual dashboard from the VS Code status bar with today's token timeline, 7-day usage, 30-day usage, recent sessions, and today event details.
- Supports account filtering. Configure multiple accounts by mapping account labels to different Codex sessions folders.
- Links the Today Timeline scatter points with the matching Today Events table rows on hover.
- Draws hollow prompt/session rings on the Today Timeline and links them to Recent Sessions rows.
- Includes commands for refresh, opening the latest session, showing details, and selecting a custom sessions folder.

## Commands

- `Codex Token Monitor: Refresh`
- `Codex Token Monitor: Open Latest Session`
- `Codex Token Monitor: Choose Sessions Folder`
- `Codex Token Monitor: Show Details`

## Settings

- `codexTokenMonitor.sessionsRoot`: custom Codex sessions folder. Empty means `~/.codex/sessions`.
- `codexTokenMonitor.accounts`: optional account list for comparing multiple Codex sessions folders.
- `codexTokenMonitor.refreshIntervalMs`: fallback polling interval. Default is `1000`.

Example multi-account configuration:

```json
"codexTokenMonitor.accounts": [
  {
    "label": "Work",
    "sessionsRoot": "C:\\Users\\PC\\.codex-work\\sessions"
  },
  {
    "label": "Personal",
    "sessionsRoot": "C:\\Users\\PC\\.codex\\sessions"
  }
]
```

## Local Development

Open this folder in VS Code and press `F5` to launch an Extension Development Host.

To run syntax checks:

```powershell
npm.cmd run check
```

To create a local VSIX without installing `vsce`:

```powershell
npm.cmd run package
```

The VSIX will be written to `dist/codex-token-monitor-0.2.2.vsix`.
