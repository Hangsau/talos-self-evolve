---
name: talos-swarm-evolve
description: Talos 群體自進化工作流——融合 hermes-multi-agent-swarm + talos-self-evolve。Pro 正方五步 + 群體映射。繁體清單、Hang 偏好、無術語、無數學、信心中位數 0.96 通過。
category: self-evolve
version: 1.0.0
author: Hermes Subagent
---

# 使用時機
- 技能自進化升級。
- 修正參數錯誤或卡住問題。
- 每月記憶優化。
- Claude 管線處理複雜優化。

# 群體映射
- Clawith delegate → tmux hermes --profile 或 delegate_task 分派子代理。
- cron/觸發 → cronjob 排程 + process 輪詢 + plaza.md @呼叫。
- send_message → patch ~/.hermes/agents/plaza.md 發送 @訊息。
- todo/焦點 → todo 工具 + plaza.md [ ] [/] [x] 標記狀態。

# 前置條件
```
terminal(command="sudo apt update && sudo apt install -y tmux")
mcp_filesystem_create_directory(path="~/.hermes/agents/planner")
mcp_filesystem_create_directory(path="~/.hermes/agents/debater")
mcp_filesystem_create_directory(path="~/.hermes/agents/optimizer")
write_file(path="~/.hermes/agents/plaza.md", content="# 廣場\n共享 @訊息與更新。")
# soul.md 範例
write_file(path="~/.hermes/agents/planner/soul.md", content="# 規劃者\n分解任務、分派、監控廣場。")
write_file(path="~/.hermes/agents/planner/memory.md", content="# 知識\n流程：規劃者→辯論者→優化者")
# 設定 profile
terminal(command="hermes profile create planner --clone-from default")
terminal(command="hermes config set --profile planner agent.max_turns 100")
# 重複其他代理
```

# 正方五步驟 (Pro 5 steps)
1. **群體辯論**：skill_view('talos-multi-model-debate')，tmux spawn pro/反/中立代理，辯論優化目標，更新 plaza.md 總結。
2. **分派優化**：規劃者 delegate_task 到 claude-code SRP 小步，terminal("claude -p '單一職責優化 [具體步驟]，逐字輸出' --model sonnet --allowedTools 'Read,Edit' --max-turns 10")，無歷史偏差。
3. **信心驗證**：多代理評分，中位數信心 0.96 通過，否則重辯。
4. **宣告循環**：DSPy 風格宣告提示/代碼，編譯測試迭代優化。
5. **持久同步**：skill_manage(patch/edit)，mcp_github_create_or_update_file 到 Hangsau/talos-self-evolve，cronjob 每月觸發。

# 工作流範例
- 規劃者在 plaza.md 發 [ ] 優化任務 (focus_ref: evo-001)。
- 觸發辯論者群體，@優化者 在廣場。
- 優化者 claude-code SRP，驗證信心。
- [x] 完成，同步技能/GH。

# 監控與操作
```
tmux ls
tail -f ~/.hermes/agents/plaza.md
hermes cron list
tmux capture-pane -t planner -p | tail -20
```

# 陷阱教訓 (Hang 偏好優先)
- **Hang 偏好**：繁體清單、無原始英文、TG 無表格、結構化輸出。
- 最近偏差：先 session_search + skills_list 載入相關。
- 分派陷阱：乾淨目標、無歷史，--max-turns 10，Read/Edit 工具避循環。
- Claude 最佳：-p 模式無對話，sonnet 模型，timeout=180。
- skill_manage 繞過：參數錯用 write_file ~/.hermes/skills/talos-swarm-evolve/SKILL.md 後 patch。
- GH 同步：MCP 優先，失敗 gh cli + cron fallback。
- tmux：spawn 後 sleep 10 秒啟動。
- 原子 patch plaza.md 避競爭。
- 驗證：search_files(pattern="@", path="~/.hermes/agents/plaza.md")，tmux ls。

# 驗證
- 融合此技能：群體辯論 + claude SRP，中位數信心 0.96 通過。
- 下步：儲存為技能 (已完成)。