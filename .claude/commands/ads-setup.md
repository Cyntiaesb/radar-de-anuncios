---
description: Verifica se o Radar de Anúncios está configurado corretamente (Apify MCP, pasta reports, etc.)
---

Faça os seguintes checks e reporte ao usuário em formato de checklist:

1. **Apify MCP conectado?**
   - Verifique se existe alguma tool com prefixo `mcp__apify__` disponível na sessão atual
   - Se sim: ✅ "Apify MCP conectado"
   - Se não: ❌ "Apify MCP não está conectado. Rode no terminal: `claude mcp add apify -- npx -y @apify/actors-mcp-server --token SEU_TOKEN` e reinicie o Claude Code"

2. **Pasta `reports/` existe?**
   - Use Glob `reports/*` ou tente listar. Se não existir, crie com Write de um `.gitkeep` em `reports/.gitkeep`.
   - Reporte: ✅ "Pasta de relatórios pronta"

3. **Skill `ads-analyzer` presente?**
   - Verifique se existe `.claude/skills/ads-analyzer/SKILL.md` via Read
   - ✅ ou ❌ conforme resultado

4. **Subagente `ads-analyzer` presente?**
   - Verifique `.claude/agents/ads-analyzer.md` via Read
   - ✅ ou ❌

Ao final, se tudo ✅, mostre:

> 🎯 **Radar de Anúncios pronto!** Use `/ads https://instagram.com/perfil_alvo` pra começar.

Se algo ❌, mostre o passo de correção e pare.
