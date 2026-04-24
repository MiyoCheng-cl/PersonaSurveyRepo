[English](./README.md) | [中文](./README.zh-TW.md)

# PersonaSurveyRepo

這個 repo 用來整理與研究 AI coding agent / persona 的設計方式，聚焦在不同 persona 適合處理哪些任務、如何為特定開發場景挑選 persona，以及不同平台在 persona 結構與可用性上的差異。

目前內容主要圍繞 React 專案情境與跨平台 persona 比較。

Personas from  https://github.com/nyldn/claude-octopus/tree/main/agents/personas

## Repo 主旨

這個 repo 的主旨，是把分散的 persona 研究、角色建議與平台觀察，整理成一個容易閱讀、比較與延伸的小型知識庫。

這個 repo 希望協助回答幾個實際問題：

- 在 React 專案中，哪些 persona 應該優先建立？
- 每種 persona 最適合負責什麼工作？
- ChatGPT、Claude、Gemini 在 persona 設計上有什麼差異？
- 這些 persona 研究未來如何應用到 routing、orchestration 與 review workflow？

## 檔案說明

### `react_project_persona_recommendations.md`

這份文件聚焦在 React 專案，整理出前端導向開發工作的 persona 建議，內容包含：

- React 專案常見任務，例如 UI component、state management、hooks、API 串接、效能、測試與 code review
- 推薦 persona 與其優先順序
- 各 persona 的強項與可能負責的工作
- 為什麼這些 persona 特別適合 React 專案流程
- 哪些 persona 值得優先建立

簡單來說，這份文件是在說明：如果要支援 React 專案，哪些 AI persona 最有幫助，以及它們各自能提供什麼價值。

### `claude_octopus_personas_combined_review.md`

這份文件是較廣泛的 persona 設計綜合比較與 review，內容包含：

- ChatGPT、Claude、Gemini 在 persona 或 agent 設計上的差異
- persona 結構、描述方式與可擴充性的觀察
- 在多平台之間都相對有價值的 persona 類型
- 可作為核心 persona 集合的候選名單
- 未來在 orchestration、routing 與 workflow 設計上的延伸方向

簡單來說，這份文件是在說明：不同 AI 平台如何設計 persona，以及哪些概念值得整理後採用。

## Repository Contents

- [README.md](./README.md)
- [README.zh-TW.md](./README.zh-TW.md)
- [react_project_persona_recommendations.md.html](./react_project_persona_recommendations.md.html)
- [claude_octopus_personas_combined_review.md.html](./claude_octopus_personas_combined_review.md.html)

## 適合的使用情境

- 為團隊建立 AI coding persona / agent library
- 定義前端或 React 專案的 AI 協作角色
- 比較不同 AI 平台的 persona 設計方式
- 為後續 orchestration 或 workflow 設計準備研究輸入
