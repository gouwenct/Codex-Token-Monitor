# Codex Token Monitor

语言：[EN](./README.md)

Codex Token Monitor 是一个用于实时监控、费用估算和可视化 Codex token 使用情况的 VS Code 扩展。

Codex Token Monitor 会监视你的 Codex JSONL 会话文件，读取 `event_msg` 中 `payload type` 为 `token_count` 的事件，并把最新 token 用量直接显示在 VS Code 状态栏中。

```text
18:41  +56k(in 54.6k, cache 50k, 91%)  $0.12
```

状态栏会显示最新一轮 session 的 token 用量，包括总 token、输入 token、缓存命中 token、缓存命中百分比和本轮估算费用。

点击状态栏中的 token usage 项目，可以打开更详细的可视化仪表盘。

![Codex Token Usage Dashboard](docs/dashboard.png)

## 功能

- 默认监视 `~/.codex/sessions`。
- 支持嵌套的 Codex 会话目录，例如 `sessions/2026/04/30/*.jsonl`。
- 在 VS Code 状态栏中显示最新一轮 session 的总 token、输入 token、缓存命中 token、缓存命中百分比和估算费用。
- 使用与 ccusage 兼容的统计方式：把每个 `token_count` 事件视为累计值，并通过同一会话文件中连续累计值之间的正向差值计算用量。
- 避免重复统计重复出现的 `token_count` 事件，因为重复的累计值会产生 0 增量。
- 根据 Codex session 日志中解析到的实际模型 ID 估算费用，分别计算非缓存输入、缓存输入、输出和 fast mode 费用。
- 可以从状态栏打开可视化仪表盘，包含今日时间线、7 日用量、30 日用量、最近会话、详细事件记录和模型费用明细。
- 支持账号筛选。你可以通过把不同账号标签映射到不同的 Codex 会话目录来配置多个账号。
- Today Timeline 上的点会在悬停时和 Today Events 表格中的对应行联动。
- 在 Today Timeline 上绘制空心的 prompt/session 圆环，并将它们与 Recent Sessions 表格联动。
- Today Events 和 Recent Sessions 中会显示每行费用，鼠标悬停费用时可以查看计算过程。
- 提供刷新数据、打开最近会话、显示详情和选择自定义会话目录等命令。

## 安装

### 方式 1：从 VS Code Marketplace 安装

1. 打开 VS Code。
2. 打开扩展视图。
3. 搜索 `Codex Token Monitor`。
4. 点击 **Install**。

### 方式 2：从 VSIX 安装

1. 下载最新的 `.vsix` 文件。
2. 打开 VS Code。
3. 打开扩展视图。
4. 点击扩展面板右上角的三点菜单。
5. 选择 **Install from VSIX...**。
6. 选择已下载的 `.vsix` 文件完成安装。

## 使用方法

安装后，Codex Token Monitor 会自动监视你的 Codex sessions 文件夹，并在 VS Code 状态栏显示 token 用量。

点击状态栏项可以打开详细仪表盘。仪表盘会展示今日时间线、最近事件、最近会话、模型费用表，以及最近 7 天和 30 天的使用趋势。

费用会根据 Codex session 中解析到的模型名称计算。无法识别价格的模型会显示为未计价，不会静默套用 fallback 模型价格。

当前内置价格表包含：

- `gpt-5.5`
- `gpt-5-codex`
- `gpt-5.1-codex`
- `gpt-5.1-codex-max`
- `gpt-5.2-codex`
- `gpt-5.3-codex`

## 命令

- `Codex Token Monitor: Refresh`
- `Codex Token Monitor: Open Latest Session`
- `Codex Token Monitor: Choose Sessions Folder`
- `Codex Token Monitor: Show Details`

## 设置

- `codexTokenMonitor.sessionsRoot`：自定义 Codex sessions 文件夹。留空时使用默认的 `~/.codex/sessions`。
- `codexTokenMonitor.accounts`：可选账号列表，用于对比多个 Codex sessions 文件夹。
- `codexTokenMonitor.refreshIntervalMs`：备用轮询间隔。默认是 `1000`。

多账号配置示例：

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

## 本地开发

在 VS Code 中打开这个文件夹，然后按 `F5` 启动 Extension Development Host。

运行语法检查：

```powershell
npm.cmd run check
```

在不安装 `vsce` 的情况下生成本地 VSIX：

```powershell
npm.cmd run package
```

生成的 VSIX 会输出到 `dist/` 目录。

## 许可证

本项目采用 [MIT License](./LICENSE)。
