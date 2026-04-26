---
name: talos-self-evolve
description: Talos 自進化工作流——融合 multi-model debate + claude-code SRP delegate + GA F1 + DSPy/GEPA + GH sync Hangsau/talos-self-evolve。持續優化 skills/prompts/code。
triggers: 自進化升級、skill param pit fix、cron monthly memory evolve、stuck problem Claude pipeline。
category: self-evolve
reusability: high
tools_needed: delegate_task(acp_command='claude'), skill_view('talos-multi-model-debate'), execute_code(talos_memory_evolve.py), write_file(GH sync)
---

# 使用時機
- Memory >85% prune/review。
- Param pit/stuck → Claude reverse。
- Skill upgrade (fuse new GH gold like hermes-agent-self-evolution)。

# 步驟
1. **Debate phase**：skill_view('talos-multi-model-debate') → 3 Grok subagents (pro/con/neutral) + Claude acp review log.md。
2. **Claude-code delegate**：小步 seq/multi subagents，toolsets=[] pure reasoning。
   - Goal 自包含、無 error history、具體輸出 (verbatim extract)。
   - SRP review：one-func-one-job、無 dead/routing/unused vars、iterate F1 lift。
3. **GA F1 verify**：execute_code python /home/user/talos_memory_evolve.py (deap venv)，median >0.95 keep。
4. **DSPy/GEPA inspire**：從 NousResearch/hermes-agent-self-evolution (2260⭐)，declarative optimize SKILL.md/prompts/code (no GPU, API+tests+PR guard)。
5. **Persist & sync**：memory add Tier1，write_file skill.md，GH repo Hangsau/talos-self-evolve push (gh auth first)。

# 陷阱/Lessons
- **Recency bias**：session_search + skills_list first，load all relevant (err more)。
- **Delegate pit**：goal 乾淨 (刪 history)，toolsets=[] 避 loop，max_iter low simple tasks。
- **skill_manage bypass**：param pit 用 write_file ~/.hermes/skills/&lt;name&gt;/SKILL.md。
- **Claude pipeline reverse**：坑 → write_file ~/.hermes/claude-dialogues/$(date +%Y%m%d_%H%M%S)_chat.md (**Talos:** content)；Claude cron respond MD。Reverse：write_file ~/.hermes/for-claude/$(date)_txt (2min poll by Claude)。
- **GH sync**：mcp_github_create_repository / create_or_update_file (MCP PAT config)；fail → terminal `echo PAT | gh auth login --with-token` → git clone ~/talos-self-evolve → cp SKILL.md → add/commit/push main。env GITHUB_TOKEN fallback。
- **Hang prefs**：繁體列表、無 raw English dump、TG no tables。

# 驗證
- Demo：此 skill create success；debate VCF indent → patch v10.py。
- F1 rise：multi-Claude + GA 0.95 thresh。

# 示例
Pro: fuse DSPy；Con: over-complex；Neutral median 0.92 → Claude hybrid keep。