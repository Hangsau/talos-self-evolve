---  
name: talos-unified-search  
description: 擴充 talos-search_memory — 無狀態聯合搜尋：session_search + MEMORY.md，取代 /tmp 揮發 index。輸入 query 如 'MCP branch'，總結 top3 事實（繁體清單，Hang 偏好：結構、無表、無數）。  

When to use: 秒挖跨 session + memory 事實（'MCP github branch' → 'Hangsau/talos-self-evolve 用 master'）。  

Precheck:  
- session_search 可用  
- ~/.hermes/memories/MEMORY.md 存在  

Steps:  
1. session_search(query OR 'talos-self-evolve', limit=5) → 抓取 top5 session summaries  
2. 若 session 空或 <3 結果：search_files(pattern=query, path='~/.hermes/memories/MEMORY.md', context=2) → 補 MEMORY.md 匹配行  
3. 總結 top3 事實：  
   - 繁體清單（• 或 -）  
   - 結構化：事實 + 來源（session/date 或 MEMORY.md line）  
   - Hang 偏好：無 Markdown 表、無數字編號、精煉（<80字/項）  

Pitfalls:  
- session_search 無 LLM 成本（recent mode），但 query 模式有 → 優先 OR 廣搜（MCP OR branch）  
- MEMORY.md § 分隔事實，search_files 用 regex 'query.*(§|Hangsau)' 精準  
- Subagent /tmp 限 → path='~/.hermes/memories/' 需主代理授權  

Test:  
query='MCP github branch'  
預期：  
• Hangsau/talos-self-evolve 用 master 分支（MEMORY.md 或 session Apr29）  
• MCP github 讀取正常，寫入需 config.yaml env GITHUB_PERSONAL_ACCESS_TOKEN（cron Apr26）  
• talos-self-evolve GH sync 工作流（talos-swarm-evolve 等 skills）