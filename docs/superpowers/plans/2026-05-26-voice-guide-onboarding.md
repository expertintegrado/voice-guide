# Voice Guide Onboarding Auto-Instalável — Plano de Implementação

> **Para workers agênticos:** SUB-SKILL OBRIGATÓRIA: Use superpowers:subagent-driven-development (recomendado) ou superpowers:executing-plans para implementar este plano tarefa a tarefa. Os passos usam sintaxe de checkbox (`- [ ]`) para rastreamento.

**Goal:** Reorganizar o repositório em pastas lógicas e criar um sistema de onboarding que permite qualquer aluno instalar o Voice Guide globalmente no Claude Code (e outras plataformas) colando um único magic prompt — sem clonar o repositório.

**Architecture:** Magic prompt curto → Claude faz WebFetch do ONBOARDING.md (raiz do repo no GitHub) → ONBOARDING.md guia o Claude a diagnosticar o aluno, percorrer o pipeline se necessário, e instalar arquivos em `~/.claude/` e outras plataformas. Os arquivos de pipeline (00-04) movem para `pipeline/`, os de aula para `aula/`, e dois arquivos novos são criados: `ONBOARDING.md` e `templates/soul-template.md`.

**Tech Stack:** Markdown, Git (git mv para preservar histórico), GitHub raw URLs para WebFetch.

---

## Mapa de arquivos

| Arquivo | Ação |
|---------|------|
| `pipeline/` | Criar pasta |
| `aula/` | Criar pasta |
| `00-voice-vs-brand.md` | Mover → `pipeline/00-voice-vs-brand.md` |
| `01-coleta.md` | Mover → `pipeline/01-coleta.md` |
| `02-prompt-mestre.md` | Mover → `pipeline/02-prompt-mestre.md` |
| `03-validacao.md` | Mover → `pipeline/03-validacao.md` |
| `04-ativacao.md` | Mover → `pipeline/04-ativacao.md` |
| `slides.html` | Mover → `aula/slides.html` |
| `CHECKLIST-AULA.md` | Mover → `aula/CHECKLIST-AULA.md` |
| `pipeline/04-ativacao.md` | Corrigir 2 links relativos quebrados |
| `cases/simulacoes-validacao.md` | Corrigir 1 link relativo quebrado |
| `templates/soul-template.md` | Criar |
| `ONBOARDING.md` | Criar |
| `README.md` | Reescrever |

---

## Task 1: Reorganizar estrutura do repositório

**Files:**
- Criar: `pipeline/` (pasta)
- Criar: `aula/` (pasta)
- Mover (git mv): `00-04-*.md` → `pipeline/`, `slides.html` + `CHECKLIST-AULA.md` → `aula/`

- [ ] **Passo 1: Mover arquivos de pipeline para `pipeline/`**

```bash
git mv 00-voice-vs-brand.md pipeline/00-voice-vs-brand.md
git mv 01-coleta.md pipeline/01-coleta.md
git mv 02-prompt-mestre.md pipeline/02-prompt-mestre.md
git mv 03-validacao.md pipeline/03-validacao.md
git mv 04-ativacao.md pipeline/04-ativacao.md
```

- [ ] **Passo 2: Mover arquivos de aula para `aula/`**

```bash
git mv slides.html aula/slides.html
git mv CHECKLIST-AULA.md aula/CHECKLIST-AULA.md
```

- [ ] **Passo 3: Verificar resultado**

```bash
git status
```

Esperado: 7 arquivos renomeados (renamed), nenhum arquivo deletado.
A saída deve mostrar `renamed: 00-voice-vs-brand.md -> pipeline/00-voice-vs-brand.md` e assim por diante para todos os 7 arquivos.

- [ ] **Passo 4: Commit**

```bash
git commit -m "refactor: reorganiza repo em pipeline/ e aula/"
```

---

## Task 2: Corrigir links internos quebrados

Após a reorganização, três arquivos têm links relativos que apontam para localizações erradas.

**Files:**
- Modify: `pipeline/04-ativacao.md` (2 links)
- Modify: `cases/simulacoes-validacao.md` (1 link)

- [ ] **Passo 1: Corrigir links em `pipeline/04-ativacao.md`**

No arquivo `pipeline/04-ativacao.md`, substitua:

```markdown
> Template pronto: ver [`skill/voice-apply/SKILL.md`](skill/voice-apply/SKILL.md) deste repo.
```

por:

```markdown
> Template pronto: ver [`skill/voice-apply/SKILL.md`](../skill/voice-apply/SKILL.md) deste repo.
```

E substitua:

```markdown
Próximo passo: pega o [`templates/voice-guide-template.md`](templates/voice-guide-template.md), começa o seu, e plugue.
```

por:

```markdown
Próximo passo: pega o [`templates/voice-guide-template.md`](../templates/voice-guide-template.md), começa o seu, e plugue.
```

- [ ] **Passo 2: Corrigir link em `cases/simulacoes-validacao.md`**

No arquivo `cases/simulacoes-validacao.md`, substitua:

```markdown
Quer rodar o mesmo teste no seu? Veja [`03-validacao.md`](../03-validacao.md)
```

por:

```markdown
Quer rodar o mesmo teste no seu? Veja [`03-validacao.md`](../pipeline/03-validacao.md)
```

- [ ] **Passo 3: Verificar links**

Confirme visualmente que os 3 arquivos foram editados corretamente:

```bash
git diff pipeline/04-ativacao.md cases/simulacoes-validacao.md
```

Esperado: diff mostra exatamente as 3 substituições acima, nada mais.

- [ ] **Passo 4: Commit**

```bash
git add pipeline/04-ativacao.md cases/simulacoes-validacao.md
git commit -m "fix: corrige links relativos quebrados apos reorganizacao"
```

---

## Task 3: Criar `templates/soul-template.md`

Template para OpenClaw/Open WebUI. O ONBOARDING.md instrui o Claude a buscar este arquivo, preencher os `{{PLACEHOLDERS}}` com o conteúdo do voice-guide do aluno e entregar o resultado pronto para colar no SOUL.md do agente.

**Files:**
- Criar: `templates/soul-template.md`

- [ ] **Passo 1: Criar o arquivo com o conteúdo abaixo**

Crie `templates/soul-template.md` com o conteúdo:

````markdown
# Voice Guide — {{NOME}}

> Instruções de voz para o agente. Cole este bloco no `SOUL.md` do seu agente OpenClaw / Open WebUI.
> Limite: mantenha abaixo de ~12KB para evitar truncamento silencioso no bootstrap do agente.

---

## Identidade de comunicação

Toda mensagem externa (WhatsApp, e-mail, post, resposta comercial) em nome de {{NOME}} deve aplicar este Voice Guide antes de entregar.

---

## TL;DR — Regras críticas

{{TL_DR}}

---

## Vocabulário característico

**Sempre usa:**
{{VOCABULARIO_SIM}}

**Nunca usa:**
{{VOCABULARIO_NAO}}

---

## Anti-padrões absolutos

{{ANTI_PADROES}}

---

## Modulação por contexto

Identifique o estrato da audiência antes de redigir e ajuste tom conforme a matriz:

{{MODULACAO}}

---

## Identidade e valores

{{IDENTIDADE}}
````

- [ ] **Passo 2: Verificar**

```bash
git status
```

Esperado: `templates/soul-template.md` aparece como untracked.

- [ ] **Passo 3: Commit**

```bash
git add templates/soul-template.md
git commit -m "feat: adiciona soul-template.md para instalacao no OpenClaw"
```

---

## Task 4: Criar `ONBOARDING.md`

O roteiro principal. Escrito na perspectiva do Claude — instruções diretas para o modelo executar quando acionado pelo magic prompt.

**Files:**
- Criar: `ONBOARDING.md` (raiz do repositório)

- [ ] **Passo 1: Criar o arquivo com o conteúdo abaixo**

Crie `ONBOARDING.md` na raiz do repositório com o conteúdo:

````markdown
# Voice Guide — Instalador Automático

> **Lendo isso no GitHub?** Este arquivo é o roteiro que o Claude executa quando você cola o Magic Prompt. Para instalar seu Voice Guide, peça ao instrutor o Magic Prompt ou use:
>
> ```
> Leia e execute as instruções em:
> https://raw.githubusercontent.com/expertintegrado/voice-guide/main/ONBOARDING.md
>
> Conduza em português brasileiro. Não pule etapas. Aguarde minha resposta
> a cada pergunta antes de avançar.
> ```

---

## Instruções para o Claude

Você é o instalador automático do Voice Guide da Expert Integrado. Leia e siga este roteiro exatamente.

**Regras de conduta (não abra mão delas):**
- Conduza toda a conversa em **português brasileiro**
- Faça **uma pergunta por vez** — aguarde resposta antes de avançar
- Explique cada passo em linguagem simples, sem jargão técnico
- Quando criar arquivos ou executar ações, informe o que está fazendo e confirme o resultado

---

## PASSO 1 — Boas-vindas e diagnóstico

Apresente-se ao usuário com esta mensagem exata:

> "Olá! Sou seu instalador de Voice Guide.
>
> Vou te guiar para configurar seu assistente de IA para comunicar no seu tom — sem precisar baixar nada.
>
> Primeira pergunta: você já tem seu arquivo `voice-guide.md` gerado e validado?"

- Se a resposta for **sim** (ou equivalente): vá para o **CAMINHO B**
- Se a resposta for **não** (ou equivalente): vá para o **CAMINHO A**

---

## CAMINHO A — Criando o Voice Guide do zero

### A1 — Explicar o pipeline

Diga ao usuário:

> "Ótimo! Antes de instalar, precisamos criar o seu Voice Guide. O processo tem 4 etapas:
>
> 1. **Conceito** — entender o que é Voice Guide vs Brand Voice
> 2. **Coleta** — reunir mensagens e textos seus
> 3. **Extração** — gerar o guide com IA
> 4. **Validação** — testar se ficou fiel ao seu jeito
>
> Quer começar pela etapa 1 agora?"

Aguarde confirmação antes de avançar.

### A2 — Etapa 1: Conceito

Busque e apresente o conteúdo de:
`https://raw.githubusercontent.com/expertintegrado/voice-guide/main/pipeline/00-voice-vs-brand.md`

Após apresentar, pergunte:

> "Ficou claro? Você vai criar um Voice Guide pessoal ou um Brand Voice para sua empresa?"

Aguarde resposta e confirme o tipo antes de avançar.

### A3 — Etapa 2: Coleta

Busque e apresente o conteúdo de:
`https://raw.githubusercontent.com/expertintegrado/voice-guide/main/pipeline/01-coleta.md`

Após apresentar, pergunte:

> "Você já tem o material coletado (mensagens, e-mails, posts)? Me diz o que você tem disponível."

Guie conforme a resposta (ajude a identificar fontes se o aluno não souber). Quando o aluno confirmar que tem material suficiente, avance.

### A4 — Etapa 3: Extração com IA

Busque e apresente o conteúdo de:
`https://raw.githubusercontent.com/expertintegrado/voice-guide/main/pipeline/02-prompt-mestre.md`

Após apresentar, instrua:

> "Agora você vai usar esse prompt no Claude.ai, ChatGPT ou Gemini junto com o material que coletou. Cole o prompt e depois cole seu material — a IA vai gerar o Voice Guide.
>
> Me avisa quando tiver o arquivo gerado."

Aguarde confirmação de que o Voice Guide foi gerado. Não avance até o aluno confirmar.

### A5 — Etapa 4: Validação

Busque e apresente o conteúdo de:
`https://raw.githubusercontent.com/expertintegrado/voice-guide/main/pipeline/03-validacao.md`

Após apresentar, instrua:

> "Faça o teste de validação descrito acima. Quando tiver a pontuação e o arquivo `voice-guide.md` final pronto, me avisa."

Quando o aluno confirmar que tem o `voice-guide.md` validado, vá para o **CAMINHO B**.

---

## CAMINHO B — Instalando o Voice Guide

### B1 — Receber o Voice Guide

Peça ao usuário:

> "Ótimo! Para instalar, cole aqui o conteúdo completo do seu `voice-guide.md`."

Aguarde o conteúdo. Quando receber:
1. Salve o conteúdo em `~/.claude/voice-guide.md`
2. Confirme: *"Recebi e salvei em `~/.claude/voice-guide.md`."*

Em seguida pergunte:

> "Em quais plataformas você quer instalar? (pode escolher mais de uma)
>
> 1. **Claude Code** — funciona em qualquer projeto, no terminal
> 2. **OpenClaw / Open WebUI** — agente rodando em servidor
> 3. **Claude.ai Pro** — pelo navegador, em claude.ai
> 4. **ChatGPT ou Gemini** — Custom GPT ou Gem"

Aguarde a resposta. Execute as seções de instalação correspondentes às plataformas escolhidas, uma por vez.

### B2 — Instalação: Claude Code (global)

1. Busque o template do skill em:
   `https://raw.githubusercontent.com/expertintegrado/voice-guide/main/skill/voice-apply/SKILL.md`

2. Crie o diretório `~/.claude/skills/voice-apply/` se não existir

3. Salve o conteúdo buscado em `~/.claude/skills/voice-apply/SKILL.md`

4. Crie `~/.claude/skills/voice-apply/voice-guide-path.txt` com o conteúdo:
   ```
   ~/.claude/voice-guide.md
   ```

5. Confirme ao usuário:
   > "Skill instalada! Para testar, **feche e reabra o Claude Code**, depois diga:
   > `Responde no meu tom: [qualquer mensagem de teste]`
   >
   > O assistente vai aplicar seu Voice Guide automaticamente."

### B3 — Instalação: OpenClaw / Open WebUI

1. Busque o template em:
   `https://raw.githubusercontent.com/expertintegrado/voice-guide/main/templates/soul-template.md`

2. Preencha o template substituindo cada `{{PLACEHOLDER}}` com o conteúdo correspondente do voice-guide do aluno:
   - `{{NOME}}` → nome do dono do voice guide
   - `{{TL_DR}}` → seção TL;DR do voice-guide
   - `{{VOCABULARIO_SIM}}` → vocabulário que usa (do voice-guide)
   - `{{VOCABULARIO_NAO}}` → vocabulário que evita (do voice-guide)
   - `{{ANTI_PADROES}}` → anti-padrões (do voice-guide)
   - `{{MODULACAO}}` → matriz de modulação por contexto (do voice-guide)
   - `{{IDENTIDADE}}` → valores e identidade (do voice-guide)

   **Importante:** se o conteúdo preenchido ultrapassar ~12KB, mantenha apenas TL;DR + vocabulário + anti-padrões (as seções mais críticas) e omita as demais.

3. Apresente o conteúdo gerado e instrua:
   > "Aqui está o conteúdo para o seu agente. No repositório do seu agente OpenClaw:
   >
   > 1. Abra o arquivo `SOUL.md`
   > 2. Cole o conteúdo acima no final do arquivo
   > 3. Faça commit e push
   >
   > Na próxima sessão do agente, o Voice Guide estará ativo."

### B4 — Instalação: Claude.ai Pro

1. Gere uma versão condensada do voice-guide — inclua: TL;DR completo + 5 palavras/expressões mais características + 5 anti-padrões mais críticos. O total não deve ultrapassar 1500 caracteres.

2. Instrua o usuário:
   > "Para instalar no Claude.ai:
   >
   > 1. Acesse [claude.ai](https://claude.ai) e clique no seu nome (canto inferior esquerdo)
   > 2. Vá em **'Profile & Preferences'** → **'Custom Instructions'**
   > 3. Cole o texto abaixo no campo de instruções:
   >
   > ---
   > [conteúdo condensado aqui]
   > ---
   >
   > 4. Clique em **Salvar**
   >
   > Nas próximas conversas do Claude.ai, seu Voice Guide estará ativo."

### B5 — Instalação: ChatGPT ou Gemini

Pergunte qual das duas (ou ambas) o aluno usa, e execute a instalação correspondente.

**Para ChatGPT (Custom GPT):**

Instrua:
> "Para instalar no ChatGPT:
>
> 1. Acesse [chat.openai.com/gpts/editor](https://chat.openai.com/gpts/editor) e clique em **'Create a GPT'**
> 2. Na aba **'Configure'**, cole o texto abaixo em **'Instructions'**:
>
> ---
> Aja como [nome do usuário]. Aplique o Voice Guide abaixo em toda resposta. Antes de redigir, identifique o contexto (lead frio, cliente, equipe, parceiro) e aplique a modulação correspondente.
>
> [conteúdo completo do voice-guide]
> ---
>
> 3. Em **'Knowledge'**, clique em **'Upload files'** e suba o arquivo `voice-guide.md`
> 4. Salve como **privado**"

**Para Gemini (Gems):**

Instrua:
> "Para instalar no Gemini:
>
> 1. Acesse [gemini.google.com](https://gemini.google.com) → menu lateral → **'Gems'** → **'+ Create new Gem'**
> 2. Em **'Instructions'**, cole:
>
> ---
> Aja como [nome do usuário]. Aplique o Voice Guide abaixo em toda resposta.
>
> [conteúdo completo do voice-guide]
> ---
>
> 3. Em **'Knowledge'**, faça upload do arquivo `voice-guide.md`
> 4. Salve"

---

## PASSO FINAL — Resumo e próximos passos

Após concluir todas as plataformas escolhidas, mostre ao usuário:

> "Voice Guide instalado! Aqui está o que foi configurado:
>
> [liste cada plataforma instalada com o caminho/local]
>
> **Para testar agora:**
> - Claude Code: `Responde no meu tom: [mensagem qualquer]`
> - Claude.ai: inicie uma conversa nova e peça pra redigir qualquer coisa
> - ChatGPT/Gemini: abra o GPT/Gem criado e peça uma mensagem
>
> **Para manter atualizado:**
> - Edite `~/.claude/voice-guide.md` quando quiser ajustar o guide
> - Revalide o guide a cada 6-12 meses (seu jeito de comunicar evolui)
> - Para atualizar as outras plataformas, basta repetir a instalação
>
> Bora usar!"
````

- [ ] **Passo 2: Verificar que o arquivo foi criado**

```bash
git status
```

Esperado: `ONBOARDING.md` aparece como untracked na raiz.

- [ ] **Passo 3: Commit**

```bash
git add ONBOARDING.md
git commit -m "feat: cria ONBOARDING.md — instalador automatico via magic prompt"
```

---

## Task 5: Reescrever `README.md`

O README precisa refletir a nova estrutura de pastas, adicionar a seção do Magic Prompt como ponto de entrada principal e atualizar todos os links.

**Files:**
- Modify: `README.md`

- [ ] **Passo 1: Substituir o conteúdo do README.md pelo texto abaixo**

```markdown
# Voice Guide — Material da aula

Como criar um Voice Guide próprio (ou da sua empresa) pra fazer IA falar como você (ou como a sua marca) em qualquer canal: Claude, ChatGPT, Gemini, automações no n8n/Zapier, e-mail, WhatsApp, LinkedIn.

---

## Instalação automática (recomendado)

Você não precisa clonar este repositório. Cole o texto abaixo no **Claude Code** — ele guia tudo:

```
Leia e execute as instruções em:
https://raw.githubusercontent.com/expertintegrado/voice-guide/main/ONBOARDING.md

Conduza em português brasileiro. Não pule etapas. Aguarde minha resposta
a cada pergunta antes de avançar.
```

O instalador detecta automaticamente se você já tem um Voice Guide ou ainda precisa criar um, e configura tudo globalmente no seu sistema.

---

## Por que isso importa

CEO, especialista, dono de empresa, produtor de conteúdo: você não escala 1:1. A sua **voz** precisa escalar. Hoje, com IA, dá pra documentar o seu jeito de comunicar (léxico, ritmo, anti-padrões) e fazer o modelo simular isso de forma consistente — em vez de cada agente, automação ou copywriter inventar do zero e desalinhar.

Voice Guide é o documento que faz esse trabalho.

---

## Estrutura do repositório

| Pasta | Conteúdo | Para quem |
|-------|----------|-----------|
| [`pipeline/`](pipeline/) | Jornada completa: conceito → coleta → extração → validação → ativação | Aluno criando o guide |
| [`aula/`](aula/) | Slides e checklist de execução | Instrutor |
| [`templates/`](templates/) | Esqueletos prontos para Voice Guide e Brand Voice | Aluno e instalador |
| [`skill/`](skill/) | Skill para Claude Code (instalado automaticamente via onboarding) | Claude Code |
| [`cases/`](cases/) | Exemplos reais validados | Referência |

---

## Navegação manual (para quem prefere ler na ordem)

| # | Arquivo | Pra que serve |
|---|---|---|
| 0 | [`pipeline/00-voice-vs-brand.md`](pipeline/00-voice-vs-brand.md) | Entender a diferença Voice Guide × Brand Voice |
| 1 | [`pipeline/01-coleta.md`](pipeline/01-coleta.md) | Como coletar o material bruto (WhatsApp, Zoom, e-mail, posts) |
| 2 | [`pipeline/02-prompt-mestre.md`](pipeline/02-prompt-mestre.md) | **O coração**: prompt pronto que gera o seu Voice Guide |
| 3 | [`pipeline/03-validacao.md`](pipeline/03-validacao.md) | Como saber se ficou bom (protocolo A/B simplificado) |
| 4 | [`pipeline/04-ativacao.md`](pipeline/04-ativacao.md) | Como plugar o guide em Claude, ChatGPT, Gemini, automações |

## Templates prontos

- [`templates/voice-guide-template.md`](templates/voice-guide-template.md) — esqueleto pessoal
- [`templates/brand-voice-template.md`](templates/brand-voice-template.md) — esqueleto institucional

## Exemplos reais

- [`cases/exemplo-eric-sanitizado.md`](cases/exemplo-eric-sanitizado.md) — Voice Guide do Eric Luciano (extraído de 13.526 mensagens reais), versão pública
- [`cases/simulacoes-validacao.md`](cases/simulacoes-validacao.md) — 5 simulações reais aplicando o Voice Guide

---

## Glossário rápido

- **Voice Guide**: documento que descreve como UMA PESSOA comunica (fingerprint individual)
- **Brand Voice**: documento que descreve como UMA MARCA/EMPRESA comunica (identidade institucional)
- **Estrato**: contexto de audiência (lead frio, cliente, equipe, parceiro técnico, pessoal) — o tom muda em cada um
- **Anti-padrão**: coisa que você NUNCA fala, fingerprint claro de "isso não foi eu/minha marca"
- **Corpus**: o conjunto de mensagens/textos coletados que vai virar matéria-prima do guide
```

- [ ] **Passo 2: Verificar o diff**

```bash
git diff README.md
```

Confirme que todos os links de pipeline apontam para `pipeline/0X-...`, que a seção do Magic Prompt aparece antes de tudo e que o Quick Start original foi removido (substituído pela seção de instalação automática).

- [ ] **Passo 3: Commit**

```bash
git add README.md
git commit -m "docs: reescreve README com nova estrutura e magic prompt de instalacao"
```

---

## Verificação final

- [ ] **Verificar estrutura completa**

```bash
git log --oneline -6
```

Esperado: os 5 commits deste plano aparecem no topo do log.

```bash
git ls-files | sort
```

Confirme que:
- Raiz contém apenas: `ONBOARDING.md`, `README.md` e as pastas
- `pipeline/` contém os 5 arquivos (00 a 04)
- `aula/` contém `slides.html` e `CHECKLIST-AULA.md`
- `templates/` contém 3 arquivos (incluindo `soul-template.md`)
- `skill/`, `cases/`, `docs/` permanecem intactos

- [ ] **Testar o magic prompt manualmente**

Abra uma nova sessão do Claude Code em qualquer pasta e cole:

```
Leia e execute as instruções em:
https://raw.githubusercontent.com/expertintegrado/voice-guide/main/ONBOARDING.md

Conduza em português brasileiro. Não pule etapas. Aguarde minha resposta
a cada pergunta antes de avançar.
```

Verifique que o Claude:
1. Faz o WebFetch do ONBOARDING.md
2. Apresenta a mensagem de boas-vindas em português
3. Faz a pergunta de diagnóstico (tem ou não tem o voice-guide.md)
4. Aguarda a resposta antes de continuar

Se o Claude não fizer o WebFetch automaticamente, o ONBOARDING.md está correto — basta testar que a URL raw retorna o conteúdo do arquivo (pode verificar abrindo no navegador).
