# Claude 完整使用教學 — 學習路徑總覽

## 大綱結構

本教學共分 10 大模組、30 個章節，從零基礎到進階自動化、企業部署、AI 工具生態整合，最後以台股分析 Agent 實作收尾。

```
基礎認識 → 介面操作 → 本地端安裝 → 外部工具整合(MCP)
        → Skills 系統 → API 開發 → 自動化實戰
```

## 模組一覽

| 模組  | 主題               | 章節數 | 建議時間    |
| --- | ---------------- | --- | ------- |
| 模組一 | [認識 Claude 生態系](module1-overview/01_claude-product-family.md) | 2 | 第 1 週 |
| 模組二 | [Claude.ai 介面操作](module2-claudeai/03_basic-prompting.md) | 3 | 第 1 週 |
| 模組三 | [Desktop + MCP 整合](module3-desktop-mcp/06_claude-desktop-install.md) | 3 | 第 2 週 |
| 模組四 | [Claude Code 開發環境](module4-claude-code/09_claude-code-install.md) | 4 | 第 3 週 |
| 模組五 | [Skills 系統（核心）](module5-skills/13_skills-concepts.md) | 5 | 第 4 週 |
| 模組六 | [Claude API 開發](module6-api/18_api-setup.md) | 3 | 第 5 週 |
| 模組七 | [實戰應用與自動化](module7-automation/21_prompt-engineering.md) | 3 | 第 6–7 週 |
| 模組八 | [Claude 在企業環境的部署](module8-enterprise/24_enterprise-overview.md) | 3 | 第 8 週 |
| 模組九 | [Claude 與 AI 工具生態整合](module9-ai-ecosystem/27_ai-tools-comparison.md) | 3 | 第 9 週 |
| 模組十 | [壓軸實作：台股分析 Agent](module10-capstone/30_taiwan-stock-agent.md) | 1 | 第 10 週 |

## 學習路徑圖

```
[模組一] 產品認識
    │
    ▼
[模組二] Claude.ai 網頁操作（日常使用入口）
    │
    ▼
[模組三] Claude Desktop + MCP
    │  MCP = 給 Claude 外部工具能力
    ▼
[模組四] Claude Code CLI
    │  本地端 AI 輔助開發
    ▼
[模組五] ★ Skills 系統
    │  讓工作流標準化、可重複使用
    ▼
[模組六] Claude API
    │  自行開發 Claude 應用
    ▼
[模組七] 實戰自動化
    │  完整 Agent 架構整合
    ▼
[模組八] 企業環境部署
    │  方案治理 / 安全合規 / 大規模推廣
    ▼
[模組九] AI 工具生態整合
    │  Claude vs Cursor / Copilot / ChatGPT / Gemini
    │  個人 AI 工具組合設計
    ▼
[模組十] ★ 壓軸實作
       台股分析 Agent：工具呼叫 + ReAct + Multi-agent + 排程自動化
```

## Skills 與其他模組的關聯

```
模組三 Claude Desktop
    ├─ MCP（賦予外部工具能力）
    └─ Skills（定義行為規範）← 模組五

模組四 Claude Code
    ├─ CLAUDE.md（專案記憶）
    ├─ MCP Servers（外部連結）
    ├─ Skills（工作流標準化）← 模組五
    └─ Subagents（平行任務委派）

模組七 實戰自動化
    ├─ Skills 作為 System Prompt 注入 API
    └─ 自訂 Skills 建立團隊標準
```

## Windows 使用者

本教學範例以 macOS 為主。如果你使用 Windows，建議先閱讀 [Windows 差異說明](00_windows-differences.md)，裡面整理了所有章節的指令對照（路徑、nvm 安裝、環境變數、AppleScript 替代方案、Task Scheduler 等）。

## 官方資源

- Claude 文件：[https://docs.anthropic.com](https://docs.anthropic.com)
- Claude Code 文件：[https://docs.anthropic.com/en/docs/claude-code/overview](https://docs.anthropic.com/en/docs/claude-code/overview)
- Claude.ai：[https://claude.ai](https://claude.ai)
- MCP 規格：[https://modelcontextprotocol.io](https://modelcontextprotocol.io)
- Skills 開放標準：[https://agentskills.io](https://agentskills.io)
