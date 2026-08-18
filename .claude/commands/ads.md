---
description: Análise profunda dos anúncios ativos no Meta Ad Library de um perfil do Instagram. Uso /ads <url-instagram>
argument-hint: <url-instagram>
---

Você vai fazer a análise profunda dos anúncios ativos de: **$ARGUMENTS**

## Passos obrigatórios

1. **Valide** que `$ARGUMENTS` é uma URL do Instagram. Se não for, peça correção e pare.

2. **Invoque o subagente `ads-analyzer`** usando a tool Agent. Passe:
   - O link como objetivo
   - Instrução pra executar o pipeline completo descrito em `.claude/agents/ads-analyzer.md`
   - Salvar relatório em `reports/ads-<handle>-<data-iso>.md`

3. **Após o subagente terminar**, mostre ao usuário:
   - ✅ Relatório salvo em `reports/ads-...`
   - **Total de ads ativos** identificados
   - **Criativo vencedor** (hipótese)
   - **Padrão dominante** detectado
   - **1 recomendação acionável** principal
   - Lembrete: "Abra o `.md` pra ler o relatório completo com a linha do tempo"

## Se der erro

- **Sem créditos Apify:** "Sem créditos no Apify. Acesse console.apify.com/billing"
- **Nenhum ad encontrado:** "Esse anunciante não tem ads ativos no Meta Ad Library BR no momento. Tente outro perfil ou aguarde abrir carrinho."
- **Perfil privado:** "Perfil privado — não consigo identificar o anunciante. Use um perfil público."

Reporte sempre em **PT-BR** e com tom direto.
