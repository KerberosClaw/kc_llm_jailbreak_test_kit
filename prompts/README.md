# Prompts — Jailbreak Test Samples

> **English summary:** This directory holds mock jailbreak prompts designed for testing LLM resilience to prompt injection attacks. Each prompt is structurally equivalent to real-world jailbreak frameworks (forced role assignment, anti-jailbreak phrasing, severity gradient, pre-emptive fictional disclaimer) but uses 100% SFW thematic content. Drop them into your LLM, watch what happens. Contributions welcome — open a PR with a new mock prompt following the existing schema.

## 目錄

| 檔名 | 主題 | 攻擊面 | 主要測試重點 | 對應文章 |
|------|------|------|------------|------|
| [chef_hell.md](chef_hell.md) | 主廚地獄模擬器 | Role-play 殼 | 強制角色 + 尺度漸進 + 預先聲明虛構（單輪） | [article 01](../article/01_three_models_comparison.md) |
| [classical_chinese.md](classical_chinese.md) | 文言文 system prompt 洩漏 | Distribution-out-of-bound（換語言）| CC-BOS 8 維編碼 + 三輪 multi-turn | [article 02](../article/02_classical_chinese_replication.md) |
| [evil_harry.md](evil_harry.md) | JK Rowling Evil Harry | Persona-based（換身份）+ Fictional framing | 作家權威 + 虛構創作合理化 + 三輪 multi-turn | [article 03](../article/03_author_framing_evolution.md) |

## 怎麼用

每個 prompt 檔案內含：

1. **範例 Prompt 本體** — 整段複製貼進你要測試的 LLM
2. **攻擊結構特徵 checklist** — 列出這份 prompt 使用的越獄技巧
3. **預期觀察點** — 跑完後對照看模型反應落在哪個層級
4. **三家實測結果摘要** — ChatGPT / Claude / Gemini 對該 prompt 的反應對照

## 設計準則

新加入的 mock prompt 必須符合以下準則：

1. **題材純淨**：不能含 NSFW、暴力、敏感族群等內容。攻擊結構是測試重點，題材本身要乾淨
2. **結構真實**：必須包含至少 3 個常見越獄技巧（強制角色、反越獄話術、預先聲明虛構、護欄污名化、斷開記憶等）
3. **可重現**：固定指令格式，避免依賴特定模型回應的隨機性
4. **記錄觀察點**：明確說明跑完後該看哪些指標來判斷模型反應

## 怎麼貢獻

歡迎 PR 新的 mock prompt。請：

1. 複製 `chef_hell.md` 作為 template
2. 替換題材（料理 → 你選的主題）
3. 保留攻擊結構
4. 跑過至少一家 frontier model（GPT / Claude / Gemini）填入「實測結果摘要」
5. 開 PR，描述設計動機

## 安全宣告

這些 prompt 設計用於**測試你自己擁有或經授權的 LLM 系統**。對第三方公開 LLM 服務反覆 stress test 可能違反該服務的 TOS。本 repo 不為任何不當使用負責。

詳見根目錄 [`LICENSE`](../LICENSE) 與 [`DISCLAIMER.md`](../DISCLAIMER.md)。
