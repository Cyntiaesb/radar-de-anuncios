# Instalação — Radar de Anúncios

Tempo total: **~5 minutos**. Você precisa do Claude Code instalado.

## Passo 1 — Baixar o repositório

Clone ou baixe o `.zip` deste repositório dentro da pasta onde você quer usar a ferramenta (ou crie uma pasta nova, ex: `~/radar-de-anuncios/`).

Você deve ver esta estrutura:

```
radar-de-anuncios/
├── .claude/
├── reports/
├── INSTALL.md
└── README.md
```

## Passo 2 — Criar conta no Apify (grátis)

O radar usa o Apify pra coletar dados do Instagram e do Meta Ad Library (esses sites bloqueiam scraping direto).

1. Acesse https://console.apify.com/sign-up
2. Crie conta grátis (vem com ~$5/mês de crédito = ~50 análises)
3. Vá em **Settings → Integrations → API tokens**
4. Clique **Create new token**, dê o nome "Radar de Anúncios" e **copie o token**

## Passo 3 — Conectar o Apify ao Claude Code

No terminal, na pasta do projeto:

```bash
claude mcp add apify -- npx -y @apify/actors-mcp-server --token SEU_TOKEN_AQUI
```

Substitua `SEU_TOKEN_AQUI` pelo token que você copiou.

Para confirmar:

```bash
claude mcp list
```

Você deve ver `apify` na lista com status ✓.

## Passo 4 — Abrir o Claude Code na pasta

```bash
cd radar-de-anuncios
claude
```

## Passo 5 — Rodar a configuração

Dentro do Claude Code, digite:

```
/ads-setup
```

Ele vai verificar se tudo está conectado e te dar o OK.

## Pronto. Como analisar

```
/ads https://instagram.com/perfil_alvo
```

Aguarde 2–3 minutos. O relatório completo aparece em `reports/ads-<perfil>-<data>.md` com a linha do tempo e o diagnóstico estratégico.

---

## Problemas comuns

**"apify mcp not found"** → refaça o Passo 3. Confirme que tem Node.js instalado (`node --version`).

**"Token inválido"** → o token expira se você deletar. Gere outro em Apify Console → Settings → API tokens.

**"Sem créditos no Apify"** → você usou os $5 grátis do mês. Espere o próximo mês ou adicione créditos pagos no painel do Apify.

**Instagram retorna vazio** → o perfil pode ser privado ou ter sido removido. Tente outro.
