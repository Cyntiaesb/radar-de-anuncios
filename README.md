# Radar de Anúncios

Análise profunda dos anúncios ativos de qualquer perfil no Meta Ad Library — só com um link do Instagram, dentro do Claude Code.

## O que ele faz

Você cola um link do Instagram. Em ~2-3 minutos você recebe:

1. **Inventário completo de criativos ativos** — por tema, formato (vídeo/imagem/carrossel) e placement (Feed, Reels, Stories, Audience Network)
2. **Hipótese de criativo vencedor** — qual está sendo escalado, com justificativa (variações ativas, tempo rodando, replicação em placements)
3. **Linha do tempo** — quando cada onda de criativos entrou no ar, se é lançamento agudo ou evergreen estabilizado
4. **Análise de copy dos top 5 anúncios** — hook, promessa, gatilho psicológico dominante, CTA
5. **Diagnóstico estratégico** — por que a estratégia funciona, pontos fortes, brechas exploráveis, templates prontos pra adaptar
6. **Comparação com análise anterior** (se você já rodou nesse perfil antes) — o que mudou desde a última vez

## Como usar

1. Leia [INSTALL.md](INSTALL.md) — instalação de ~5 minutos
2. Configure a API key do Apify: `/ads-setup`
3. Analise: `/ads https://instagram.com/perfil_alvo`
4. Abra o relatório em [reports/](reports/)

## Por que só ads, e não o funil inteiro

Existe uma ferramenta irmã, [Espião de Funil](https://github.com/Cyntiaesb/espiao-de-funil), que mapeia o funil completo (Instagram + landing + checkout + ads + estratégia). O Radar de Anúncios é o recorte pra quem já sabe que quer entender SÓ a estratégia de tráfego pago — sem gastar tempo/créditos processando landing e checkout.

## Custo de operação

- **Claude Code**: sua assinatura
- **Apify**: free tier dá ~50 análises/mês. Depois custa ~$0.05–0.20 por análise completa.

## Parte da família Radar

- [Radar de Demanda](https://github.com/Cyntiaesb/radar-de-demanda) — descobre o que o mercado já busca e já compra
- [Radar de Posicionamento](https://github.com/Cyntiaesb/radar-de-posicionamento) — estudo de mercado + posicionamento + Value Proposition Canvas
- **Radar de Anúncios** — o que o concorrente está anunciando agora, e por quê funciona

## Suporte

- Bugs e sugestões: abra uma Issue neste repositório, ou me chama no Instagram [@cyntiaesberard](https://instagram.com/cyntiaesberard)
- Versão: 1.0.0
