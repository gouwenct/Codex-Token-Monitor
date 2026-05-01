# Changelog

## 0.2.3

- Added reverse hover linking from Today Events rows to timeline event points.
- Added reverse hover linking from Recent Sessions rows to timeline session rings.
- Increased session ring stroke weight to make hollow timeline circles easier to target.

## 0.2.2

- Reduced Today Timeline event point size and line thickness.
- Changed Recent Sessions to question-level totals by summing all ccusage-style event deltas for the same prompt.
- Added hollow prompt/session rings on the Today Timeline and hover highlighting for matching Recent Sessions rows.

## 0.2.1

- Improved Today Timeline with colored scatter points, gradient line segments, readable time ticks, and hover linking to Today Events.
- Aligned Recent Sessions and Today Events to the same ccusage-style delta accounting.
- Added input, output, total, and prompt snippet columns with token-intensity row colors.
- Added hover tooltips for 7-day and 30-day bars.

## 0.2.0

- Added a status-bar dashboard webview with today timeline, 7-day totals, and 30-day totals.
- Added account selection with optional multi-account session folder configuration.
- Added recent sessions and today event detail tables.

## 0.1.2

- Fixed VSIX packaging to create a real ZIP archive that VS Code can install.

## 0.1.1

- Changed accounting to match ccusage-style cumulative deltas.
- Repeated `token_count` events no longer affect latest usage or today's total.

## 0.1.0

- Initial VS Code extension.
- Realtime status bar monitor for Codex JSONL token usage.
- Commands for refresh, latest session opening, details, and sessions folder selection.
