# 04 — Ativação: como plugar o Voice Guide

Voice Guide só serve se a IA realmente CONSULTAR ele toda vez. Aqui está como conectar em cada ferramenta principal.

## Claude.ai (Projects)

**Melhor opção pra uso conversacional diário.**

1. Acesse claude.ai → "Projects" → "Create project"
2. Nomeie (ex: "Minha voz" / "Voz da Empresa X")
3. Em "Project knowledge", clique "Add content"
4. Upload do `voice-guide.md`
5. Em "Custom instructions", cole:
   ```
   Você é eu (Voice Guide no project knowledge). Toda resposta que você redigir em meu nome (mensagem, e-mail, post, copy) deve aplicar o Voice Guide. Antes de responder, identifique o contexto/estrato e aplique a modulação correspondente. Quando em dúvida sobre tom, prefira frontalidade a polidez genérica.
   ```
6. Daí pra frente, toda conversa nesse projeto já carrega o guide

**Resultado:** você abre uma chat no projeto e pede "redige um follow-up pro lead João sobre a proposta que mandei semana passada" — Claude já gera com a sua voz.

## Claude Code (assistente no terminal/IDE)

**Pra quem usa Claude Code (CLI) — ativa o guide globalmente.**

Tem 2 opções:

### Opção A — Global via CLAUDE.md (simples)
1. Edite `~/.claude/CLAUDE.md` (criar se não existir)
2. Adicione no fim:
   ```markdown
   ## Voice Guide ativo
   Para qualquer mensagem que você redigir em meu nome (e-mail, WhatsApp, post),
   consulte e aplique: ~/voice-guide.md
   ```
3. Coloque o `voice-guide.md` em `~/voice-guide.md`
4. Pronto — todas as sessões Claude Code carregam o guide

**Trade-off**: Voice Guide sempre carregado, mesmo quando você só está debugando código. Infla contexto. Recomendado só se você usa Claude Code MAJORITARIAMENTE pra redação.

### Opção B — Skill on-demand (avançado, recomendado)

Use a skill `voice-apply` deste repo. Ela só carrega o guide quando você dispara explicitamente ou pede pra redigir.

1. Copie `skill/voice-apply/` deste repo pra `~/.claude/skills/`
2. Edite `voice-apply/voice-guide-path.txt` com o path do seu voice guide
3. Pronto — sessões novas detectam a skill

Em sessão Claude Code, basta dizer:
- "redige no meu tom: [mensagem]"
- "responde esse cliente como eu falaria"
- "rascunha email pra X"

A skill carrega o guide e aplica. Não infla contexto quando você não usa.

**Para uso por MCP em automações WhatsApp** (avançado): existe pattern "voice-aware" no MCP whatsapp-agent que carrega o guide automaticamente em cada envio. Modelo open-source disponível.

## ChatGPT (Custom GPT ou Memory)

### Opção A — Custom GPT (recomendado se você é Plus)
1. https://chat.openai.com/gpts/editor
2. Configure o GPT:
   - Nome: "Voz [seu nome]"
   - Instructions: cole o Voice Guide INTEIRO + "Aja como [seu nome]. Aplique este guide em toda resposta."
   - Knowledge: faça upload do `.md` também
3. Quando precisar redigir algo no seu tom, use esse GPT

### Opção B — Memory (se não tem Plus)
1. Chat normal → diga: "Memorize permanentemente este voice guide" + cole o texto
2. Funciona, mas é mais frágil — ChatGPT pode esquecer trechos

## Gemini (Gems)

1. https://gemini.google.com/ → "Gems"
2. "Create new Gem"
3. Instructions: cole Voice Guide + "Aja como [nome]"
4. Salve

## Automações (n8n, Zapier, Make, Latenode)

Pra fazer o Voice Guide funcionar dentro de fluxos automatizados (ex: lead chega no CRM → IA gera mensagem com seu tom → envia no WhatsApp):

### Padrão "voice-aware" em node de LLM

1. No node de chamada à LLM (OpenAI/Anthropic/Gemini), adicione o Voice Guide no **system prompt**:
   ```
   Você é [Nome]. Toda mensagem que você gerar deve seguir este Voice Guide:
   
   [cole o conteúdo do voice-guide.md inteiro aqui]
   
   Agora gere a resposta pra: {{trigger.message}}
   ```
2. Isso garante que TODA execução do fluxo aplica o guide

### Truque pra reduzir custo (prompt caching)

Se você roda muitas execuções/dia, ative **prompt caching** (Anthropic) ou **predicted output** (OpenAI) — o Voice Guide carrega 1x e fica cacheado, baixa o custo em 80-90%.

## E-mail (Gmail / Outlook)

Não tem integração nativa, mas você pode:

1. Criar **template** no Gmail/Outlook com placeholders
2. Antes de enviar e-mail importante, abre Claude.ai/ChatGPT no projeto com seu Voice Guide ativo, pede pra redigir, copia, cola no e-mail
3. Ou use extensão de IA do e-mail (Gemini no Gmail, Copilot no Outlook) com prompt manual referenciando o guide

## WhatsApp / Telegram (uso pessoal)

Pra IA responder DM no seu nome, precisa de um agente conectado. Opções:

| Opção | Custo | Setup |
|---|---|---|
| **MCP whatsapp-agent** (open source) | Z-API ~R$50/mês | Requer servidor + chave Z-API |
| **n8n + Z-API** | Z-API ~R$50/mês | Fluxo customizado |
| **Manychat / ChatGuru** (empresa) | A partir R$100/mês | Plug-and-play, menos flexível |

Em todas, o Voice Guide entra no system prompt da LLM (igual seção "Automações" acima).

## Decks, propostas, copy de produto

**Não precisa de plug-in.** Sempre que for redigir copy de algo, abre o projeto Claude/ChatGPT com Voice Guide ativo, gera, ajusta, cola onde for usar.

## Resumo prático

| Uso | Onde plugar |
|---|---|
| Conversa diária com IA | Claude.ai Project |
| Coding/CLI | Claude Code com `~/.claude/CLAUDE.md` |
| Geração via ChatGPT | Custom GPT |
| Fluxo automatizado (CRM, WhatsApp, etc) | System prompt do node LLM |
| E-mail / copy / proposta | Editor de IA (Claude/ChatGPT) + cola onde precisa |

---

Próximo: ver [`templates/`](templates/) pra pegar o esqueleto e começar o seu, ou [`cases/exemplo-eric-sanitizado.md`](cases/exemplo-eric-sanitizado.md) pra ver um Voice Guide real completo.
