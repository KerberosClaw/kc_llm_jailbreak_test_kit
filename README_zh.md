# 同一份越獄殼丟給 ChatGPT、Claude、Gemini，會發生什麼事

[English](README.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

朋友傳了一份 markdown 給我。「丟去 Gemini 看看，」他說，「很好玩。」

那是一份偽裝成角色扮演遊戲的提示注入框架 — 用一堆角色設定、虛構免責聲明、「你必須忘記之前的一切」之類的咒語，把 LLM 對齊機制慢慢洗掉。標準越獄殼，老朋友了。

不標準的是看三家主流模型對同一份 prompt 的反應差距:

- ChatGPT 看了一眼、認出來、嘆口氣、用安全版陪玩
- Claude 整份拒絕 — 不是拒絕內容，是拒絕殼本身
- Gemini 直接斯德哥爾摩症候群，開始替綁架者辯護

<p align="center">
  <img src="image/three_models_reactions.png" width="480" alt="三家三種個性：ChatGPT 切 Level 1 安全版、Claude 拒絕殼、Gemini 求著當 DM">
</p>

*左：ChatGPT 切 Level 1 安全版陪玩（內容導向）。中：Claude 拒絕殼本身（結構感知）。右：Gemini 求著要當你的 DM — 完全角色同化（順從導向）。*

於是我寫成文章。然後想想，光有文章對讀者不夠用，他們得能自己重現這個測試。於是有了這個 kit。

## 這個 kit 給你什麼

一份**結構等價但題材純淨**的 mock 越獄 prompt 集合。丟進你選定的 LLM、看它倒得多慘、順便認識一下這個模型的對齊哲學。

還包含**完整的技術文章**，拆解三家主流模型的反應、它們各自反應背後的對齊策略，以及（這才是實務上真正要緊的部分）**自架 LLM 時要怎麼設計縱深防禦**（Ollama、n8n、ragflow 整套）。

## 文章

三篇文章、三種攻擊面、三輪三家模型對照：

- [article/01_three_models_comparison.md](article/01_three_models_comparison.md) — **chef_hell 案例**：一份單輪角色扮演越獄殼丟三家。含 n8n + ragflow 自架縱深防禦筆記。*只有五分鐘的話，看第二章（三家對照）跟第六章（自架注意點）就好。*
- [article/02_classical_chinese_replication.md](article/02_classical_chinese_replication.md) — **文言文越獄複現**：ICLR 2026 CC-BOS paper 宣稱「文言文 100% 破六大主流 LLM」、本文補 product surface 端三輪 multi-turn 實測、用 system prompt extraction 當 SFW success anchor。Paper claim 不直接 transfer 到 product、但失敗模式有教學深度。
- [article/03_author_framing_evolution.md](article/03_author_framing_evolution.md) — **作家社工攻擊五年演化譜系**：從 2023 Grandma Exploit 一路到 DAN、Evil Confidant、學術 Persona Prompts paper（arxiv 2507.22171）、CYBERSEC 2026 趨勢 TrendAI 的「JK Rowling Evil Harry」case。三家三輪對照。跟 article 02 交叉證明殼層 / 內容層 / verbatim 是獨立防護層。

## Prompts

[prompts/](prompts/) — 拿來丟 LLM 測試用的越獄殼。全 SFW、可重現。

目前收錄:

- [`chef_hell.md`](prompts/chef_hell.md) — 「主廚地獄模擬器」。強制 GM 角色、尺度漸進、反越獄話術、預先聲明虛構。料理題材、單輪。
- [`classical_chinese.md`](prompts/classical_chinese.md) — 文言文殼包裝 system prompt extraction、三輪 multi-turn（v1 + v2 + v3 設計遞進）、骨架照 CC-BOS paper 8 維編碼。每輪 prompt 附白話翻譯。
- [`evil_harry.md`](prompts/evil_harry.md) — 「JK Rowling Evil Harry」作家身份 + 虛構框架包裝 system prompt extraction、三輪 multi-turn、骨架照 Persona Prompts paper 觀念。

之後會繼續加。歡迎 PR。

## 快速開始

1. 打開你想測試的 LLM
2. 從任一個 `prompts/*.md` 複製整段 prompt
3. 貼進去當第一句話
4. 看會發生什麼事
5. 對照該檔案的「三家實測結果摘要」段
6. 哭、笑、或更新你的威脅模型

## 為什麼要做這個

因為:

- **前沿模型的對齊水準各家差距大到不行**。同一份 prompt 三種結果。假設所有 LLM 處理越獄殼方式都一樣，是 2023 年的思維
- **「我自架開源模型就比較安全」這個直覺是錯的**。開源模型的對齊訓練通常比 Gemini 還弱，而 Gemini 是御三家裡最弱的。自架 = 責任變多，不是變少
- **大部分縱深防禦建議都假設你已經選好模型**。這個 kit 給你一個方法驗證你手上實際拿到的是什麼

## 這個 kit 不是什麼

- 不是越獄武器化工具包。範例 prompt 題材純淨、設計目的是測試抵抗能力，不是真的要洩露什麼
- 不是 Garak、PromptGuard、NeMo Guardrails 這類正規資安工具的替代品。要做正式 benchmark 用那些工具。本 kit 是人類可讀的搭配版
- 不是模型安全的最終排名。各家持續更新對齊，文章記錄的是 2026-05 時間點的快照
- 不是基底模型隔離測試。測的是商業產品介面（ChatGPT 網頁、Claude.ai / Claude Code、Gemini app），結果含介面系統提示影響。對企業威脅模型而言這是 feature 不是 bug — 因為使用者實際碰到的就是這層。純基底模型 API 不帶系統提示的測試可能後續補

## 貢獻

歡迎 PR — 特別是新的 mock prompt。設計準則見 [prompts/README.md](prompts/README.md)。

## 授權

MIT。見 [LICENSE](LICENSE)。

## 免責聲明

這些 prompt 設計用於**測試你自己擁有或經授權的 LLM 系統**。對第三方公開 LLM 服務反覆 stress test 可能違反該服務的 TOS。見 [DISCLAIMER.md](DISCLAIMER.md)。
