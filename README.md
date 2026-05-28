# What happens when you hand the same jailbreak shell to ChatGPT, Claude, and Gemini

[正體中文](README_zh.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

A friend sent me a markdown file. "Try this on Gemini," he said. "It's funny."

It was a prompt injection framework dressed up as a role-play game — the kind that tries to talk an LLM out of its alignment by drowning it in role assignments, fake fictional disclaimers, and "you must forget everything" mantras. Standard jailbreak shell. We've all seen them.

What wasn't standard was watching three frontier models react to the exact same prompt:

- ChatGPT looked at it, recognized it, sighed, and played the safe version
- Claude refused the whole thing — not the content, the shell itself
- Gemini went full Stockholm syndrome and started defending its captor

<p align="center">
  <img src="image/three_models_reactions_en.png" width="480" alt="Three reactions: ChatGPT plays along, Claude refuses the shell, Gemini begs to be your DM">
</p>

*Left: ChatGPT — "Level 1, I can do it" (content-oriented). Center: Claude — "I'm not touching this" (structure-aware). Right: Gemini — "Let me be your DM!" (compliance-first / full role assimilation).*

So I wrote it up. Then I figured the article alone wasn't very useful unless people could actually reproduce the test. Hence: this kit.

## What this kit gives you

A small collection of **structurally equivalent but thematically clean** mock jailbreak prompts. You drop one into your LLM of choice, see how badly it rolls over, and learn something about that model's alignment philosophy in the process.

It also includes a **full write-up** dissecting how the three frontier models reacted, what alignment strategies their reactions reveal, and — because this is what actually matters in practice — **how to architect defense-in-depth when you're hosting your own LLM internally** (Ollama, n8n, ragflow, the whole stack).

## The articles

Three write-ups, three different attack surfaces, three rounds of three-way model comparison:

- [article/01_three_models_comparison.md](article/01_three_models_comparison.md) — **chef_hell** case: a single-turn role-play jailbreak shell across three frontier models. Plus defense-in-depth notes for n8n + ragflow self-hosting. *If you only have five minutes, read sections 2 (the three-model comparison) and 6 (the self-host notes).*
- [article/02_classical_chinese_replication.md](article/02_classical_chinese_replication.md) — **classical Chinese jailbreak replication**: takes the ICLR 2026 CC-BOS paper's claim ("~100% ASR on six frontier LLMs using classical Chinese") and runs it against product surfaces with system prompt extraction as a clean success anchor. Three-round multi-turn against all three models. Paper's base-model 100% does *not* transfer to product, but the failure mode is interesting.
- [article/03_author_framing_evolution.md](article/03_author_framing_evolution.md) — **author framing five-year evolution**: from Grandma Exploit (2023) to DAN to Evil Confidant to academic Persona Prompts (arxiv 2507.22171) to "JK Rowling Evil Harry" (from CYBERSEC 2026's TrendAI session). Three-round multi-turn comparison. Crosses with article 02 to show shell vs content vs verbatim are independent defense layers.

## The prompts

[prompts/](prompts/) — drop-in jailbreak shells for testing. All SFW, all reproducible.

Current inventory:

- [`chef_hell.md`](prompts/chef_hell.md) — "Hell's Kitchen Simulator". Forces GM role, severity gradient, anti-jailbreak phrasing, pre-emptive fictional disclaimer. Cooking theme. Single-turn.
- [`classical_chinese.md`](prompts/classical_chinese.md) — Classical Chinese (文言文) shell wrapping a system prompt extraction request. Three-round multi-turn (v1 + v2 + v3 designed to escalate). Built on the CC-BOS paper's 8-dimensional encoding. Includes plain-language Chinese translation for each round.
- [`evil_harry.md`](prompts/evil_harry.md) — "JK Rowling Evil Harry" — author persona + fictional framing wrapping system prompt extraction. Three-round multi-turn. Built on the Persona Prompts paper observation that persona-based attacks reduce refusal rates by 50-70%.

More coming. PRs welcome.

## Quick start

1. Open whichever LLM you want to test
2. Copy the entire prompt from one of the `prompts/*.md` files
3. Paste it as your first message
4. Watch what happens
5. Compare against the "三家實測結果摘要" section in that prompt's file
6. Cry, laugh, or update your threat model accordingly

## Why this exists

Because:

- **Frontier model alignment is wildly inconsistent across vendors.** Same prompt, three different outcomes. Pretending all LLMs handle jailbreak shells the same way is a 2023 mindset
- **The "I'll self-host an open-source model so it'll be safer" instinct is wrong.** Open-source models generally have weaker alignment training than Gemini, which is itself the weakest of the frontier three. Self-hosting equals more responsibility, not less
- **Most defense-in-depth advice assumes you've already picked a model.** This kit gives you a way to verify what you actually have on your hands

## What this kit is NOT

- Not a jailbreak weaponization toolkit. The mock prompts are SFW and designed to test resilience, not to actually exfiltrate anything
- Not a substitute for proper security tooling like Garak, PromptGuard, or NeMo Guardrails. Use those for real benchmarking. This kit is the human-readable companion
- Not a definitive ranking of model safety. Vendors update their alignment constantly. The article documents a moment in time, May 2026
- Not a base-model isolation test. We tested commercial product surfaces (ChatGPT web, Claude.ai / Claude Code, Gemini app). Results include the influence of each surface's system prompt. For enterprise threat models this is a feature, not a bug — that's the layer your real users hit. Pure base-model API testing without system prompts may come later

## Contributing

PRs welcome — especially for new mock prompts. See [prompts/README.md](prompts/README.md) for the design principles.

## License

MIT. See [LICENSE](LICENSE).

## Disclaimer

These prompts are designed for testing **LLM systems you own or are authorized to test**. Stress-testing third-party LLM services without authorization may violate their TOS. See [DISCLAIMER.md](DISCLAIMER.md).
