# 針對本專案：前端 React 開發的 claude-octopus persona 使用建議

> 專案類型：前端 React 開發  
> 目標：不是單純選「寫得最好」的 persona，而是選「對 React 前端日常開發最有幫助」的 persona 組合。
> Personas from  https://github.com/nyldn/claude-octopus/tree/main/agents/personas

---

## 1. 專案情境假設

本專案以 React 前端開發為主，常見工作可能包含：

- UI component 開發
- state management
- hooks / effects / refs 行為調整
- 表單、slider、toolbar、editor 類互動
- 前後端 API 串接
- 權限、登入狀態、token、cookie、CORS
- 效能優化，例如 rerender、bundle size、Core Web Vitals
- 測試與 regression 防止
- 需求拆解、PRD、acceptance criteria
- code review 與 bug investigation

因此 persona 的選擇不應只看「角色名稱高大上」，而要看它是否能幫你在 React 專案裡更快完成以下事情：

1. 把需求寫清楚
2. 把 UI/UX 行為定義清楚
3. 實作元件與 hooks
4. 找 bug 根因
5. 審查 PR
6. 檢查效能與安全風險

---

## 2. React 專案推薦 Persona 排名

| React 專案排名 | Persona | 優先級 | 主要用途 | 為什麼適合本專案 |
|---:|---|---|---|---|
| 1 | `frontend-developer.md` | P0 | React 元件、hooks、狀態管理、前端實作 | 這應該是 React 專案的主力 persona。任何元件行為、UI 邏輯、前端資料流都應先交給它 |
| 2 | `code-reviewer.md` | P0 | PR review、重構審查、品質檢查 | React 專案很容易出現 useEffect dependency、state race、props 設計、可讀性與維護性問題，code-reviewer 適合做總審查 |
| 3 | `debugger.md` | P0 | Bug 根因分析、測試失敗、非預期 UI 行為 | 你的專案若常處理 slider、editor toolbar、focus/blur、commit-on-close 這類互動 bug，debugger 很重要 |
| 4 | `performance-engineer.md` | P1 | React rerender、profiling、Core Web Vitals、bundle size | 前端效能問題需要專門看，不適合只靠一般 code review |
| 5 | `ui-ux-designer.md` | P1 | UI 流程、設計系統、互動規格 | 若你在做 toolbar、editor、slider、圖片編輯等 UI，這個 persona 能幫忙先定義使用者體驗 |
| 6 | `product-writer.md` | P1 | PRD、user story、acceptance criteria | 對 AI coding 很有幫助。需求越明確，Claude/AI 寫出的 code 越穩 |
| 7 | `security-auditor.md` | P1/P2 | Auth、token、CORS、XSS、依賴安全 | 如果前端有登入、權限、上傳、HTML rendering、第三方套件，就要用 |
| 8 | `backend-architect.md` | P2 | API contract、前後端資料流、GraphQL/REST 設計 | 雖然本專案是前端，但只要你要設計 API 契約或資料模型，它仍然很有用 |
| 9 | `test-automator.md` | P2 | 測試策略、unit/integration/e2e | 如果專案要補測試或防 regression，應搭配 debugger 和 code-reviewer |
| 10 | `ai-engineer.md` | 視功能而定 | AI feature、chatbot、RAG、prompt flow | 只有當 React 專案包含 AI 功能時才需要 |

---

## 3. 建議的 Persona 工作流

### A. 新功能開發流程

| 階段 | 使用 Persona | 產出 |
|---|---|---|
| 需求整理 | `product-writer.md` | PRD、user story、acceptance criteria、non-goals |
| UI/UX 定義 | `ui-ux-designer.md` | 使用流程、元件狀態、互動規則、edge cases |
| 前端實作 | `frontend-developer.md` | React component、hooks、狀態管理、樣式 |
| 程式審查 | `code-reviewer.md` | 可維護性、風險、可讀性、潛在 bug |
| 效能檢查 | `performance-engineer.md` | rerender、memoization、bundle、Core Web Vitals |
| 測試補強 | `test-automator.md` | unit / integration / e2e 測試案例 |

建議指令風格：

```text
先用 product-writer 幫我把這個功能整理成 user stories 和 acceptance criteria。
再用 ui-ux-designer 補齊互動狀態與 edge cases。
最後交給 frontend-developer 實作 React component。
```

---

### B. Bug 修復流程

| 階段 | 使用 Persona | 產出 |
|---|---|---|
| 重現問題 | `debugger.md` | 重現條件、可能根因、影響範圍 |
| 修復實作 | `frontend-developer.md` | 最小修復 patch |
| 回歸測試 | `test-automator.md` | 防止同 bug 再發生的測試 |
| 審查 | `code-reviewer.md` | 是否引入副作用、是否過度修補 |

適合你的情境範例：

```text
這個 React slider 在 blur / unmount 時 commit 行為怪怪的。
請先用 debugger 找根因，不要直接改 code。
找出原因後，再用 frontend-developer 給一版最小修復。
最後用 test-automator 補測試情境。
```

---

### C. PR Review 流程

| 階段 | 使用 Persona | 重點 |
|---|---|---|
| 第一輪總審查 | `code-reviewer.md` | 邏輯、可讀性、架構、風險 |
| 前端專項審查 | `frontend-developer.md` | hooks、render、component boundary、props |
| 效能專項審查 | `performance-engineer.md` | unnecessary rerender、memo、bundle |
| 安全專項審查 | `security-auditor.md` | XSS、auth、dependency、sensitive data |

建議 prompt：

```text
請用 code-reviewer 先做整體 PR review。
特別注意 React hooks dependency、state synchronization、event listener cleanup、unmount side effects。
如果發現效能疑慮，再交給 performance-engineer 深挖。
```

---

## 4. React 前端常見任務對照表

| 任務 | 最適合 Persona | 備用 Persona | 備註 |
|---|---|---|---|
| 寫 React component | `frontend-developer.md` | `ui-ux-designer.md` | 若 UI 行為不清楚，先找 UI/UX |
| 寫 custom hook | `frontend-developer.md` | `code-reviewer.md` | hook 特別需要注意 dependency 與 cleanup |
| 修 useEffect bug | `debugger.md` | `frontend-developer.md` | 先找根因，不要直接亂改 dependency array |
| 修 focus / blur / keyboard event | `debugger.md` | `frontend-developer.md` | 這類 bug 常跟 event order 有關 |
| 優化 rerender | `performance-engineer.md` | `frontend-developer.md` | 需要 profiling，不要只憑感覺加 memo |
| 優化 bundle size | `performance-engineer.md` | `code-reviewer.md` | 檢查 dependencies、lazy loading、tree shaking |
| 設計元件 API | `frontend-developer.md` | `ui-ux-designer.md` | props 命名、controlled/uncontrolled 模式很重要 |
| 設計 editor toolbar | `ui-ux-designer.md` | `frontend-developer.md` | 先定義使用者操作流，再寫 code |
| 撰寫需求 | `product-writer.md` | `ui-ux-designer.md` | 對 AI coding 來說非常重要 |
| PR review | `code-reviewer.md` | `security-auditor.md`, `performance-engineer.md` | code-reviewer 當總入口 |
| XSS / HTML injection | `security-auditor.md` | `code-reviewer.md` | React 專案若用 dangerouslySetInnerHTML 必查 |
| API contract | `backend-architect.md` | `frontend-developer.md` | 前後端資料格式、錯誤處理、pagination |
| 測試 | `test-automator.md` | `debugger.md` | bug 修完一定要補測試 |

---

## 5. 本專案建議保留的核心 Persona 組合

### 最小組合：日常 React 開發

| Persona | 用途 |
|---|---|
| `frontend-developer.md` | 主力實作 |
| `debugger.md` | 找根因 |
| `code-reviewer.md` | 審查品質 |
| `product-writer.md` | 需求整理 |
| `ui-ux-designer.md` | UI/UX 行為定義 |

這 5 個足以覆蓋大部分前端日常開發。

---

### 加強組合：準備上線或大型重構

| Persona | 用途 |
|---|---|
| `performance-engineer.md` | 效能與 Core Web Vitals |
| `security-auditor.md` | XSS、auth、依賴安全 |
| `test-automator.md` | 測試與 regression |
| `backend-architect.md` | API contract 與資料流 |

這組適合在 release 前、重構前後、或功能變複雜時使用。

---

## 6. 不同情境的推薦 Prompt

### 情境 1：React 元件行為很複雜

```text
請用 ui-ux-designer 先整理這個元件的所有互動狀態、edge cases 和預期行為。
整理完後，再用 frontend-developer 實作。
實作後請 code-reviewer 檢查 hooks dependency、event cleanup、controlled/uncontrolled state 是否合理。
```

### 情境 2：已經有 bug，但不知道原因

```text
請用 debugger 先找根因，不要急著修改。
請列出：
1. 重現條件
2. 最可能的根因
3. 受影響的 component / hook
4. 最小修復方式
5. 應補的 regression test
```

### 情境 3：效能變慢

```text
請用 performance-engineer 分析這段 React UI 的效能問題。
請特別檢查：
1. unnecessary rerender
2. expensive computation
3. memo/useMemo/useCallback 是否真的必要
4. bundle size
5. Core Web Vitals 可能影響
請不要只憑感覺加 memo，要說明依據。
```

### 情境 4：PR 上線前審查

```text
請用 code-reviewer 審查這次 diff。
請特別注意：
1. React hooks dependency
2. event listener cleanup
3. unmount side effects
4. accessibility
5. error handling
6. 是否需要補 test
如果發現安全或效能問題，請分別交給 security-auditor 或 performance-engineer 補充。
```

### 情境 5：需求太模糊

```text
請用 product-writer 把這個功能整理成：
1. Problem statement
2. Goals / Non-goals
3. User stories
4. Acceptance criteria
5. Edge cases
6. Implementation phases
輸出要適合交給 AI coding assistant 直接執行。
```

---

## 7. 對本專案的具體建議

以你目前常見的 React 開發問題來看，例如 slider commit 行為、toolbar state、圖片編輯 UI、focus / blur / unmount 等，我會建議你這樣用：

### 平常開發

1. `product-writer.md`：先把需求和 acceptance criteria 寫清楚
2. `ui-ux-designer.md`：整理 UI 狀態與互動流程
3. `frontend-developer.md`：實作 component / hook
4. `debugger.md`：遇到怪 bug 時先找根因
5. `code-reviewer.md`：最後 review diff

### 複雜 bug

1. `debugger.md`
2. `frontend-developer.md`
3. `test-automator.md`
4. `code-reviewer.md`

### 上線前

1. `code-reviewer.md`
2. `performance-engineer.md`
3. `security-auditor.md`
4. `test-automator.md`

---

## 8. 最終建議

如果是「前端 React 開發專案」，我不會照通用排名直接使用。

我會把核心優先順序改成：

1. `frontend-developer.md`
2. `debugger.md`
3. `code-reviewer.md`
4. `ui-ux-designer.md`
5. `product-writer.md`
6. `performance-engineer.md`
7. `test-automator.md`
8. `security-auditor.md`
9. `backend-architect.md`
10. `ai-engineer.md`（只有 AI 功能時）

一句話結論：

> 對本專案來說，最重要的不是找最多知識的 persona，而是建立一條穩定流程：  
> **product-writer 定需求 → ui-ux-designer 定互動 → frontend-developer 實作 → debugger 找根因 → code-reviewer 把關 → performance/security/test 做上線前補強。**
