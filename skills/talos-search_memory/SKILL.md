---
name: talos-search_memory
description: Symbiont knowledge_writer fork — 純 Python MEMORY 搜尋。/tmp index + grep CLI。

When to use: 秒挖事實（'MCP' / 'babysit'）。

Precheck:
- command -v python

Steps:
1. mkdir -p /tmp/talos-index
2. python -c "
from pathlib import Path
import re

mem_path = Path('/home/user/.hermes/memories/MEMORY.md')
content = mem_path.read_text(errors='ignore')
facts = re.findall(r'§([^§]+)', content)
tags = [(f.strip()[:50], 'MEMORY', f.strip()[:100]) for f in facts[:50]]

with open('/tmp/talos-index/TAGS.md', 'w') as t:
    t.write('| tag | source | snippet |\\n|--|--|--|\\n')
    for tag, src, snip in tags:
        t.write(f'| {tag} | {src} | {snip} |\\n')

print('Talos memory indexed:', len(tags), 'facts')
"
3. grep -i 'babysit' /tmp/talos-index/TAGS.md | head -3

Pitfalls:
- /tmp 揮發（cron 重建）
- MCP /tmp only

Test:
grep -i 'MCP' /tmp/talos-index/TAGS.md

GH: mcp_github_push_files Hangsau/talos-self-evolve skills/talos-search_memory.md