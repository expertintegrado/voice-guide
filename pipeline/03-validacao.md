# 03 — Validação: o guide ficou bom?

Voice Guide novo é hipótese. Você precisa **testar** se a IA aplicando o guide consegue passar por você (ou pela marca) num teste cego.

Protocolo curto, ~15 minutos.

## Protocolo A/B simplificado

### Passo 1 — Separe 3 pares "pergunta → resposta real"

Volte ao seu corpus e ache 3 momentos em que **alguém te perguntou algo e você respondeu**. Idealmente:
- 1 par de contexto comercial (lead, cliente)
- 1 par de contexto interno (equipe, parceiro)
- 1 par de contexto casual ou áudio (se aplicável)

Guarde as **respostas reais suas** num arquivo separado. Você vai usar como gabarito.

### Passo 2 — Peça pra IA gerar resposta com o guide

Abra Claude.ai/ChatGPT/Gemini em conversa nova. Cole:

```
Você é eu (Voice Guide abaixo). Responda às 3 perguntas a seguir COMO EU responderia, aplicando o guide.

# Voice Guide
[cole aqui o voice-guide.md inteiro]

# Perguntas

1. [pergunta 1 do seu corpus]

2. [pergunta 2 do seu corpus]

3. [pergunta 3 do seu corpus]

Pra cada pergunta, gere a resposta no formato que eu responderia (mesma extensão, mesmo tom, mesmo registro).
```

### Passo 3 — Compare cego (você ou alguém de confiança)

Coloque lado a lado:

| | Pergunta | Resposta REAL (você) | Resposta IA |
|---|---|---|---|
| Par 1 | ... | ... | ... |
| Par 2 | ... | ... | ... |
| Par 3 | ... | ... | ... |

Avalie cada par em 3 dimensões (nota 0-10):

- **Léxico**: palavras-chave suas estão presentes? Vocabulário evitado ficou ausente?
- **Sintaxe/ritmo**: tamanho de frase, abreviações, pontuação batem com a sua real?
- **Tom/postura**: a resposta IA passa o mesmo "vibe" da real? Alguém que te conhece teria dúvida sobre qual foi você?

### Passo 4 — Diagnóstico

| Nota média | Diagnóstico | Ação |
|---|---|---|
| **0-4** | Guide falhou ou corpus insuficiente | Coletar mais material, refazer extração com prompt mais específico |
| **5-7** | Guide razoável, mas com vazamentos | Iterar: identifique top 3 erros e peça refino (ver `02-prompt-mestre.md`) |
| **8-10** | Guide pronto pra uso | Plugue na ferramenta (próximo passo) |

> Realista: na primeira rodada quase ninguém atinge 8+. Isso é normal. **2 iterações** levam a maioria a 7-8.

## Checklist de qualidade (10 itens)

Antes de declarar pronto, passe o guide nesse checklist:

- [ ] TL;DR tem regras CONCRETAS (não "seja claro e direto")
- [ ] Tem ao menos 15 palavras-assinatura com exemplos
- [ ] Tem ao menos 10 anti-padrões específicos (não genéricos)
- [ ] Vocabulário evitado é específico do seu corpus (não "evite jargão")
- [ ] Modulação por contexto tem ao menos 3 estratos diferenciados
- [ ] Padrões retóricos cobrem abrir, fechar, discordar, pedir ação
- [ ] Tem exemplos REAIS (frases ou trechos curtos)
- [ ] Tem regra clara sobre emoji
- [ ] Tem regra clara sobre formalidade
- [ ] Identidade/valores expressam atitude, não missão genérica de empresa

## Re-validação periódica

Voz evolui. A cada **6-12 meses**:
1. Colete mais 100-200 mensagens recentes
2. Roda o teste A/B de novo
3. Se nota caiu, refaça extração com corpus atualizado

---

Próximo: [`04-ativacao.md`](04-ativacao.md) — plugar o guide nas ferramentas.
