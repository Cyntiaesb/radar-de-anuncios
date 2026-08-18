---
name: ads-analyzer
description: Análise profunda de anúncios ativos do Meta Ad Library a partir de um link do Instagram. Foco específico em criativos — formato, copy, gatilhos, variações, criativo vencedor, padrões e oportunidades. Use quando o usuário quer entender PROFUNDAMENTE a estratégia de anúncios de alguém, sem perder tempo com landing/checkout.
---

# Playbook do Radar de Anúncios

> Inspirado nas melhores skills de competitive intel do mundo (ComposioHQ, talknerdytome-labs, AgriciDaniel), adaptado pro mercado brasileiro de infoprodutos e com entrada simplificada via link do Instagram.

---

## 1. Quando usar

- O usuário quer entender SÓ os anúncios (e não o funil inteiro)
- Quer detectar o **criativo vencedor** (qual está sendo escalado)
- Quer comparar variações do mesmo criativo
- Quer mapear a **linha do tempo** dos lançamentos via ads
- Quer extrair templates de copy e formato

## 2. Pipeline de análise (executar em ordem)

### Etapa 1 — Resolver o anunciante a partir do link IG
- Receba uma URL do Instagram
- Extraia o `handle` do perfil
- Use Apify (`apify/instagram-profile-scraper`) pra confirmar:
  - Nome real da página (`fullName`)
  - Conta business? Verificada?
  - Marca associada (procurar @menções na bio)
- O **anunciante no Meta Ad Library** pode ser:
  - O próprio @handle
  - O `fullName` da pessoa
  - Uma marca associada (ex: bio diz "Mentor da @marca" → busque pela marca também)
- **Sempre teste TODOS os 3 nomes** se houver ambiguidade

### Etapa 2 — Coletar anúncios do Meta Ad Library
- Use Apify `apify/facebook-ads-scraper`
- Filtro: `country=BR`, `activeStatus=active`
- Busque por **3 termos potenciais** (handle, nome real, marca)
- Capture pra cada anúncio:
  - `title` (snapshot.title)
  - `displayFormat` (VIDEO, IMAGE, CAROUSEL, DCO)
  - `publisherPlatform` (Facebook, Instagram, AN, Messenger, Threads)
  - `startDateFormatted` e `endDateFormatted`
  - `reachEstimate` (quando disponível)
  - `isActive`
  - `pageInfo` (validar que é o anunciante certo)
  - `creativeBody`, `creativeLinkTitle`, `creativeLinkDescription`
  - URL da imagem/vídeo
  - CTA do anúncio (Saiba mais, Inscreva-se, Compre, etc.)

### Etapa 3 — Filtrar ruído
Resultados do Ad Library frequentemente vêm misturados com anúncios não relacionados (mesmo nome de produto, palavra-chave genérica). **Filtre:**
- Confirme `pageInfo.name` ou `pageId` bate com o anunciante alvo
- Descarte anúncios cuja URL de destino não combina com o domínio do alvo
- Descarte anúncios com tema/copy claramente diferente do nicho do alvo

### Etapa 4 — Categorizar criativos
Agrupar por **tema/mensagem**:
- Conte quantos por tema
- Calcule % do total
- Para cada tema, liste a copy literal de 1–2 exemplos

Agrupar por **formato**:
- VIDEO / IMAGE / CAROUSEL / DCO / DPA
- Calcule % de cada
- Hipótese: o formato com mais ads ativos é o vencedor (mais investido)

Agrupar por **placement**:
- Reels / Feed / Stories / Audience Network / Messenger / Threads
- Identifique se está focado em "all placements" ou só em "Instagram"

### Etapa 5 — Identificar o criativo vencedor
**Sinais de criativo vencedor:**
1. **Múltiplas variações ativas do mesmo conceito** — anunciante só duplica criativo que está performando
2. **Rodando há mais tempo** (>30 dias = validado)
3. **Maior `reachEstimate`** quando disponível
4. **Replicação em múltiplos placements** — performou bem em todos
5. **Vídeo > Imagem geralmente** (em 2026, vídeo domina)

Liste no relatório: **"Hipótese de criativo vencedor: [título/copy], rodando desde [data], com [N] variações ativas."** — sempre marcado como hipótese, o Ad Library não expõe conversão real.

### Etapa 6 — Linha do tempo (timeline)
Construa uma timeline:
- **Aquecimento longo (3+ meses):** evergreen
- **Burst recente (< 7 dias):** lançamento agudo
- **Pico em datas específicas:** carrinho aberto

Mostre as **datas de início** dos anúncios em ordem cronológica. Identifique se está em **lançamento ativo** ou **evergreen estabilizado**.

### Etapa 7 — Análise de copy
Para cada anúncio relevante, identifique:
- **Hook (primeira frase):** Dor, pergunta, afirmação chocante, prova?
- **Promessa:** O que entrega?
- **Gatilho dominante:** Escassez, Urgência, Prova, Autoridade, Reciprocidade, Transformação, Curiosidade, Compromisso
- **CTA:** Específico ou genérico?
- **Emoji ou texto puro?**
- **Tamanho da copy:** Short-form (<50 palavras) ou long-form (>200 palavras)

Identifique **padrões** que se repetem entre criativos vencedores.

### Etapa 8 — Diagnóstico estratégico

#### O que ele está fazendo (1 frase)
Síntese contundente da estratégia de ads.

#### Por que funciona (3-5 mecanismos)
Cada um amarrado a evidência dos próprios anúncios. Cite gatilhos psicológicos.

#### Pontos fortes (tabela)
| # | Ponto | Evidência |
|---|---|---|

#### O que você pode roubar (modelar)
Lista numerada de templates/abordagens pra adaptar.

#### Brechas exploráveis
| # | Brecha | Como atacar |
|---|---|---|

### Etapa 9 — Comparar com análise anterior (se houver)
Se já existir `reports/ads-<handle>-*.md` de uma data anterior, adicione ao relatório a seção "O que mudou desde a última análise" — novos criativos, criativos que saíram do ar, mudança no formato/placement dominante. Se não houver análise anterior, omita a seção.

### Etapa 10 — Salvar relatório
Em `reports/ads-<handle>-<YYYY-MM-DD>.md` usando o template abaixo.

---

## 3. Template do relatório de ads

```markdown
# Análise de Ads: @<handle>

**Data:** YYYY-MM-DD
**Anunciante identificado:** <Nome real / Page>
**Link IG:** <url>

## Resumo executivo
- **Total de anúncios ativos:** N
- **Formato dominante:** <vídeo X% / imagem Y% / carrossel Z%>
- **Plataformas:** <lista>
- **Anúncio mais antigo ativo desde:** <data>
- **Estágio detectado:** <evergreen | aquecimento | lançamento ativo | pico de carrinho>
- **Criativo vencedor (hipótese):** <título + por quê>

## 1. Inventário de criativos

### Por tema
| Tema | Qtd | % | Exemplo de copy |
|---|---|---|---|

### Por formato
| Formato | Qtd | % |
|---|---|---|

### Por placement
| Placement | Qtd |
|---|---|

## 2. Linha do tempo

[Mermaid timeline aqui]

\`\`\`mermaid
timeline
  title Lançamento via Ads
  <data>: <criativo 1>
  <data>: <criativo 2>
  ...
\`\`\`

## 3. Top 5 anúncios (mais relevantes)

### Ad 1 — <título>
- **Formato:** VIDEO/IMAGE/CAROUSEL
- **Rodando desde:** <data> (X dias)
- **Variações:** N
- **Hook:** "<primeira frase>"
- **Promessa:** <o que entrega>
- **Gatilho dominante:** <Cialdini-like>
- **CTA:** "<texto exato>"
- **Por que funciona:** <análise em 1-2 linhas>

[Repetir para top 5]

## 4. Padrões identificados nos vencedores

- **Padrão 1:** <descrição> — encontrado em N criativos
- **Padrão 2:** ...

## 5. Diagnóstico estratégico

### O que ele está fazendo
<1 frase>

### Por que funciona
1. ...
2. ...

### Pontos fortes
| # | Ponto | Evidência |

### O que você pode roubar
1. ...
2. ...

### Brechas exploráveis
| # | Brecha | Como atacar |

## 6. Templates de copy prontos pra adaptar

[Liste 3-5 templates baseados nos vencedores, no formato:]

**Template 1 — Hook de dor:**
> "<estrutura>"
> Exemplo do alvo: "<copy real>"

## 7. O que mudou desde a última análise (se houver análise anterior)

- <novos criativos, criativos que saíram do ar, mudança de formato/placement dominante>

---
*Análise gerada pelo Radar de Anúncios v1.0*
```

---

## 4. Heurísticas e dicas

### Identificando o anunciante correto
- Se o IG é @perfil mas a bio diz "Sócio da Marca X", o anunciante real no Meta Ad Library provavelmente é **Marca X** (a página business gerencia os ads)
- Procure no rodapé da landing por "Anunciante: ..." ou termos legais

### Anúncios em "modo escala"
- Anunciante sério tem **3-10 variações** do mesmo criativo (testes A/B agressivos)
- 1 criativo isolado rodando há muito tempo geralmente é o vencedor consolidado
- 5+ criativos novos em uma semana = teste em massa

### Anúncios "fantasma"
- Alguns anunciantes deletam ads quando a campanha trava — não confunda com criativo morto
- Sempre filtre por `isActive: true`

### Idiomas
- Ads em inglês num perfil BR podem ser: (a) targetando público gringo, (b) teste de criativo internacional, (c) pessoa que mora fora. Marque como tal.

### Limites
- `reachEstimate` só aparece em ads políticos no Brasil (lei eleitoral). Para infoprodutos = `null`.
- Sem dados de spend (não temos esses números no Ad Library público).
- Sem segmentação detalhada (público-alvo não é público no BR).
