# Voice Guide — Material da aula

Como criar um Voice Guide próprio (ou da sua empresa) pra fazer IA falar como você (ou como a sua marca) em qualquer canal: Claude, ChatGPT, Gemini, automações no n8n/Zapier, e-mail, WhatsApp, LinkedIn.

> Material de aula da mentoria. Clone este repo, leia na ordem, monte o seu.

## Por que isso importa

CEO, especialista, dono de empresa, produtor de conteúdo: você não escala 1:1. A sua **voz** precisa escalar. Hoje, com IA, dá pra documentar o seu jeito de comunicar (léxico, ritmo, anti-padrões) e fazer o modelo simular isso de forma consistente — em vez de cada agente, automação ou copywriter inventar do zero e desalinhar.

Voice Guide é o documento que faz esse trabalho.

## Ordem de leitura

| # | Arquivo | Pra que serve |
|---|---|---|
| 0 | [`00-voice-vs-brand.md`](00-voice-vs-brand.md) | Entender a diferença Voice Guide × Brand Voice |
| 1 | [`01-coleta.md`](01-coleta.md) | Como coletar o material bruto (WhatsApp, Zoom, e-mail, posts) |
| 2 | [`02-prompt-mestre.md`](02-prompt-mestre.md) | **O coração**: prompt pronto que gera o seu Voice Guide |
| 3 | [`03-validacao.md`](03-validacao.md) | Como saber se ficou bom (protocolo A/B simplificado) |
| 4 | [`04-ativacao.md`](04-ativacao.md) | Como plugar o guide em Claude, ChatGPT, Gemini, automações |

## Templates prontos

- [`templates/voice-guide-template.md`](templates/voice-guide-template.md) — esqueleto pessoal
- [`templates/brand-voice-template.md`](templates/brand-voice-template.md) — esqueleto institucional

## Skill opcional (Claude Code)

- [`skill/voice-apply/`](skill/voice-apply/) — skill que dispara o Voice Guide on-demand em Claude Code. **Opcional** — pra uso em Claude.ai/ChatGPT basta Project/Custom GPT.

## Exemplo real

- [`cases/exemplo-eric-sanitizado.md`](cases/exemplo-eric-sanitizado.md) — Voice Guide do Eric Luciano (extraído de 13.526 mensagens reais), versão pública
- [`cases/simulacoes-validacao.md`](cases/simulacoes-validacao.md) — 5 simulações reais aplicando o Voice Guide (evidência de que funciona)

## Quick start (lição de casa)

1. Colete 200-500 mensagens suas em qualquer canal (WhatsApp exportado, e-mails enviados, posts, transcrições) → veja `01-coleta.md`
2. Cole o material + o prompt mestre no Claude/ChatGPT/Gemini → veja `02-prompt-mestre.md`
3. Valide com 3 pares pergunta→resposta → veja `03-validacao.md`
4. Plugue o guide na ferramenta que você usa → veja `04-ativacao.md`

Resultado esperado: assistente de IA que escreve mensagens, e-mails, posts e respostas comerciais com o seu fingerprint linguístico, não com o tom genérico do modelo.

## Glossário rápido

- **Voice Guide**: documento que descreve como UMA PESSOA comunica (fingerprint individual)
- **Brand Voice**: documento que descreve como UMA MARCA/EMPRESA comunica (identidade institucional)
- **Estrato**: contexto de audiência (lead frio, cliente, equipe, parceiro técnico, pessoal) — o tom muda em cada um
- **Anti-padrão**: coisa que você NUNCA fala, fingerprint claro de "isso não foi eu/minha marca"
- **Corpus**: o conjunto de mensagens/textos coletados que vai virar matéria-prima do guide
