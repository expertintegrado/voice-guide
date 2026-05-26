# 02 — Prompt mestre de extração

Esse é o coração do material. Você cola o corpus (do passo 01) + esse prompt em qualquer IA de fronteira (Claude 4.x, GPT-5, Gemini 2.5) e ela gera o seu Voice Guide estruturado.

## Como rodar

1. Abre Claude.ai (recomendado), ChatGPT ou Gemini
2. Cria uma conversa nova
3. Cola TODO o conteúdo do prompt abaixo
4. Anexa os arquivos do corpus (`.txt`) OU cola o conteúdo direto na conversa
5. Aguarda a IA gerar o guide
6. Salva o resultado num arquivo `voice-guide.md`

> **Dica**: rode em modelo com janela de contexto grande (Claude 4.x Sonnet/Opus, Gemini 1.5/2.5 Pro). GPT funciona, mas pode precisar fatiar o corpus em pedaços.

---

## Prompt mestre — versão Voice Guide individual

Copie tudo dentro da caixa abaixo:

```
Você vai me ajudar a criar um VOICE GUIDE empírico — um documento que descreve como EU comunico, baseado em mensagens reais que vou te fornecer.

# Contexto

Quem sou eu (preencha):
- Nome:
- Profissão / papel:
- Empresa (se aplicável):
- Público com quem mais converso:
- O que vou usar esse Voice Guide pra fazer: (ex: agente de IA responder WhatsApp, redigir e-mails comerciais, gerar posts no LinkedIn no meu nome, alimentar automação no n8n, etc)

# O corpus

Estou te fornecendo mensagens minhas em [N] contextos diferentes:
- [Contexto 1, ex: WhatsApp com clientes]
- [Contexto 2, ex: WhatsApp com equipe]
- [Contexto 3, ex: E-mails comerciais]
- [Contexto 4, ex: Transcrição de reunião Zoom]

# Sua tarefa

Analise empiricamente o corpus e produza um VOICE GUIDE em markdown com a estrutura abaixo. Use APENAS o que aparece no material — NÃO invente padrões nem importe clichês genéricos. Quando contar frequência, conte de verdade. Quando der exemplo, use trecho real (pode anonimizar nomes).

## Estrutura obrigatória

### TL;DR (8-12 linhas)
Resumo das regras MAIS críticas. Cada linha é uma regra única, acionável, baseada em evidência. Inclua qualquer fingerprint forte (palavra/padrão que aparece muito ou muito pouco e é diagnóstico).

### 1. Vocabulário núcleo

#### Palavras-assinatura (USE)
Liste 15-25 termos/expressões com:
- Frequência aproximada no corpus
- O que significam pra mim / função retórica
- Em que contextos aparecem

#### Vocabulário evitado (NÃO USE)
Liste 10-15 termos/expressões que NUNCA aparecem no meu corpus mas seriam o default genérico de uma IA. Use isso como fingerprint reverso.

#### Jargões pessoais e termos técnicos
Termos próprios, nomes de produtos meus, comunidades que frequento, autores que cito.

### 2. Sintaxe e ritmo

Cubra:
- Tamanho médio de mensagem (chars, palavras, frases)
- Porcentagem de mensagens single-line vs multi-line
- Uso de abreviações (você → vc, para → pra, que → q, etc)
- Uso de pontuação (reticências, vírgula, ponto, em-dash, exclamação)
- Caixa alta (frequência e função)
- Emojis (quais, frequência, em que contexto)
- Conectores frequentes
- Erros de digitação típicos (se houver — pode ser fingerprint autêntico)

### 3. Modulação por contexto

Matriz com TODOS os contextos do corpus. Pra cada um:
- Tom dominante
- Vocativo típico
- Densidade afetiva (alta/média/baixa)
- Marcadores característicos
- Exemplo curto real

### 4. Padrões retóricos nomeados

Cubra como eu:
- ABRO mensagem (openers canônicos)
- FECHO mensagem (closers)
- DISCORDO
- ENSINO / EXPLICO
- DECIDO em público
- PEÇO AÇÃO
- RECONHEÇO ERRO
- VENDO (se aplicável)
- REDIRECIONO conversa

Pra cada padrão, dê 1-2 frases-modelo + 1 exemplo real.

### 5. Identidade e valores (postura)

5-10 princípios que aparecem repetidos no corpus. Não é missão de empresa — é como EU me posiciono. Ex: "frontalidade > polidez", "ROI provado > promessa", "auto-ironia > seriedade postural".

### 6. Anti-padrões absolutos

15-25 coisas que eu NUNCA faria, com base no que NÃO aparece no corpus. Cada item é um fingerprint claro de "isso não foi escrito por mim".

### 7. Como usar este guide (instrução pro modelo)

Checklist de 5-8 passos pra IA aplicar antes de gerar mensagem em meu nome.

---

# Regras pra você (modelo) durante a extração

1. Conte de verdade — não chute números. Se citar "X aparece 200x", precisa ter aparecido perto disso.
2. Use trechos reais como exemplo (anonimizando nomes próprios).
3. Se um padrão é forte só em UM contexto, marque "específico de [contexto]".
4. Se houver contradição no corpus (eu falo X num lugar e o oposto noutro), aponte — é provável que seja modulação por contexto, não inconsistência.
5. NÃO importe padrões genéricos de "boa comunicação" — se não tá no meu corpus, não entra.
6. Se algum dado ficou ralo (poucos exemplos), avise no fim na seção "Limitações conhecidas".

Pronto. Aguarde o corpus.
```

---

## Prompt mestre — variante Brand Voice institucional

Pra Brand Voice, troque a abertura por:

```
Você vai me ajudar a criar um BRAND VOICE GUIDE — documento que descreve como a empresa [NOME] comunica de forma consistente em todos os canais oficiais.

# Contexto

A empresa:
- Nome:
- Setor:
- Tamanho aproximado:
- Público principal:
- Posicionamento (em 1 frase, se já tiver):
- Onde esse Brand Voice vai ser aplicado: (ex: site, posts oficiais, e-mails de campanha, copy de produto, scripts de SAC)

# O corpus

Estou te fornecendo material oficial da empresa:
- [Site / landing pages]
- [Posts em redes sociais oficiais]
- [E-mails de campanha]
- [Apresentação comercial]
- [Outros]

# Sua tarefa

Mesma estrutura do Voice Guide individual, mas adaptada:

[...estrutura idêntica, ajustando seções:]
- Seção 3 (modulação): em vez de "estratos pessoais", organize por CANAIS (site, posts, e-mails, SAC)
- Seção 5 (identidade): substituir por "promessa da marca + valores expressos no copy"
- Adicionar Seção 8: "Termos institucionais oficiais" (nomes de produtos, expressões registradas, taglines)

Resto idêntico.

Aguarde o corpus.
```

---

## Iteração — quando rodar de novo

Você não precisa acertar de primeira. Roda → aplica → testa → ajusta.

**Sinais de que precisa iterar:**
- IA misturou tom de contextos diferentes (vendas + íntimo na mesma msg)
- Palavras-chave suas faltaram no resultado
- Anti-padrões ficaram genéricos ("não use linguagem chula") em vez de específicos
- O guide ficou curto demais (< 150 linhas) — provavelmente faltou material ou prompt foi mal calibrado

**Como pedir iteração:**
Cole o guide gerado de volta no chat, junto com 2-3 exemplos reais que ele errou, e peça: "Refine esses 3 pontos baseado nesses exemplos reais que ficaram fora do padrão."

---

## Custo aproximado

| Modelo | Custo da extração |
|---|---|
| Claude.ai (assinatura mensal) | Já incluso no Pro/Max |
| Claude API direto | ~$2-5 por extração (depende do tamanho do corpus) |
| ChatGPT Plus | Já incluso |
| Gemini Advanced | Já incluso |

---

Próximo: [`03-validacao.md`](03-validacao.md) — como saber se ficou bom.
