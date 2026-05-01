# Codex Token Monitor

Codex Token Monitor 是一个用于实时检测并可视化 Codex token 消耗的 VS Code 插件。

它会监听 Codex 的 JSONL session 文件，读取 payload type 为 `token_count` 的 `event_msg` 记录，并直接在 VS Code 状态栏中显示最新 token 用量。

```text
19:32  +320 (in:200 / out:120)  today:12.4k
```

点击状态栏中的 token 用量，即可进入详情可视化界面。

![Codex Token Usage Dashboard](docs/dashboard.png)

## 功能特性

- 默认监听 `~/.codex/sessions`。
- 支持嵌套的 Codex session 目录，例如 `sessions/2026/04/30/*.jsonl`。
- 在 VS Code 状态栏中显示最近一次请求的 token 增量、input tokens、output tokens，以及今日累计用量。
- 使用与 ccusage 兼容的统计方式：每个 `token_count` 事件会被视为累计值，同一个 session 文件中的用量会通过相邻累计值的正向差值计算。
- 可避免重复 `token_count` 事件造成的重复计数，因为重复累计值会产生 0 增量。
- 点击状态栏可打开可视化面板，查看今日 token 时间线、最近 7 天用量、最近 30 天用量、最近会话以及今日事件详情。
- 支持多账号筛选。你可以通过配置不同账号标签与 Codex sessions 目录来对比多个账号的用量。
- Today Timeline 中的散点可与 Today Events 表格行联动，高亮对应事件。
- Today Timeline 会绘制空心的 prompt/session 圆环，并与 Recent Sessions 行联动。
- 内置刷新数据、打开最新 session、显示详情、选择自定义 sessions 文件夹等命令。

## 安装方法

### 方法一：在 VS Code 中搜索安装

1. 打开 VS Code。
2. 打开左侧的扩展面板。
3. 搜索 `Codex Token Monitor`。
4. 点击 **Install** 安装。

### 方法二：通过 VSIX 文件安装

1. 下载最新的 `.vsix` 文件。
2. 打开 VS Code。
3. 打开左侧的扩展面板。
4. 点击扩展面板右上角的三个小点。
5. 选择 **从 VSIX 中安装...**。
6. 选择下载好的 `.vsix` 文件，即可完成安装。

## 使用方法

安装后，Codex Token Monitor 会自动监听你的 Codex sessions 文件夹，并在 VS Code 状态栏中显示 token 用量。

点击状态栏中的 token 用量，可以打开详情可视化界面，查看今日时间线、最近事件、最近会话，以及最近 7 天和 30 天的用量趋势。

## 命令

- `Codex Token Monitor: Refresh`
- `Codex Token Monitor: Open Latest Session`
- `Codex Token Monitor: Choose Sessions Folder`
- `Codex Token Monitor: Show Details`

## 设置项

- `codexTokenMonitor.sessionsRoot`：自定义 Codex sessions 文件夹。留空时默认使用 `~/.codex/sessions`。
- `codexTokenMonitor.accounts`：可选的账号列表，用于对比多个 Codex sessions 文件夹。
- `codexTokenMonitor.refreshIntervalMs`：兜底轮询间隔，默认值为 `1000`。

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

在 VS Code 中打开该项目文件夹，按 `F5` 启动 Extension Development Host。

运行语法检查：

```powershell
npm.cmd run check
```

在不安装 `vsce` 的情况下创建本地 VSIX：

```powershell
npm.cmd run package
```

生成的 VSIX 文件会输出到 `dist/` 文件夹。
