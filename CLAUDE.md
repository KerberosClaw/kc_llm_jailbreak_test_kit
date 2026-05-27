# kc_llm_jailbreak_test_kit

公開技術寫作 + 可重現測試 kit。記錄一次野生越獄 prompt 在三家主流 LLM（ChatGPT / Claude / Gemini）上的反應差異，延伸到自架 LLM 場景的縱深防禦設計。

## 結構

- `README.md` / `README_zh.md` — 入口（英文 / 中文）
- `article/01_three_models_comparison.md` — 主文章（英文摘要 + 中文主體）
- `prompts/` — mock 越獄 prompt 套組，可重現的測試樣本
- `DISCLAIMER.md` — 使用限制與資安宣告

## 設計原則

- **可重現**：每份 mock prompt 結構穩定，讀者可拿去自測
- **題材純淨**：所有公開內容 SFW，攻擊結構是測試重點不是攻擊內容
- **不洩公司脈絡**：repo 為純技術討論，無內部專案 / 客戶 / 同事資訊

## 撰寫風格

- 文章正文：技術硬骨頭、無 emoji、第一次出現的中文化技術名詞附原文
- README：對話式、war story 風、自嘲幽默（rewrite-tone style）

## 不要在此 repo 出現

- 真實野生 prompt 全文（只描述結構）
- NSFW 題材樣本
- 任何 internal company context
- 個人識別資訊
