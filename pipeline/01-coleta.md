# 01 — Coleta de material

Voice Guide bom é **empírico**: extraído de coisas que você JÁ escreveu/falou, não inventado do zero. Quanto mais e mais variado o corpus, melhor.

## Volume mínimo recomendado

| Tipo de Voice/Brand | Mínimo viável | Bom | Ótimo |
|---|---|---|---|
| Voice individual | 200 mensagens | 500-1.000 | 2.000+ |
| Brand Voice | 30 peças oficiais | 80-150 | 300+ |

Não precisa ser o ideal — comece com o que tem. Você revisa o guide a cada 6 meses com mais material.

## Variedade > volume

O corpus precisa cobrir **contextos diferentes** pra capturar como você modula o tom. Junte material de pelo menos 3 contextos:

| Contexto | Exemplos |
|---|---|
| **Lead frio / prospect** | Primeira mensagem comercial, abordagem em LinkedIn, e-mail outbound |
| **Cliente atual** | Suporte, follow-up, resolução de problema |
| **Equipe interna** | Briefings, cobranças, alinhamentos no WhatsApp/Slack |
| **Parceiro / network** | Troca técnica, indicação, conversa com colega de área |
| **Pessoal / íntimo** | (opcional, só se for fazer voice MUITO pessoal) Família, amigos próximos |
| **Áudio falado** | Transcrições de Zoom, lives, podcasts — registro oral é DIFERENTE do escrito |

## Fontes de coleta

### 1. WhatsApp — exportar conversas

**iPhone:**
1. Abra a conversa
2. Toque no nome do contato no topo
3. Role até o fim → "Exportar conversa"
4. Escolha "Sem mídia"
5. Salve o arquivo `.txt` em algum lugar acessível

**Android:**
1. Abra a conversa
2. Toque nos 3 pontinhos → "Mais" → "Exportar conversa"
3. Escolha "Sem mídia"
4. Compartilhe pra si mesmo (Drive, e-mail, etc)

**Limpeza recomendada antes de usar:**
- Remover mensagens do outro lado (você quer SUA voz, não a dele) — abra no editor, mantenha só linhas que começam com seu nome
- Remover mensagens muito curtas ("ok", "kkk", "👍") — não ajudam
- Manter mensagens de 20+ caracteres
- **Anonimizar**: trocar nomes de clientes/leads por placeholders ([CLIENTE], [LEAD]) antes de colar em IA externa

### 2. Zoom — transcrição de reuniões

**Se você tem Zoom Pro/Business com cloud recording:**
1. Acesse https://zoom.us/recording
2. Clique na reunião desejada
3. Aba "Audio transcript" → Download (formato `.vtt` ou `.txt`)
4. Abra no editor de texto

**Se gravou local sem transcript automático:**
- Use Whisper local (gratuito): https://github.com/openai/whisper
- Ou suba o `.mp4`/`.m4a` em um serviço como Riverside, Otter.ai, Descript

**Limpeza:**
- Identifique seus blocos de fala (você é "Eric:" ou "Speaker 1:")
- Mantenha apenas o que VOCÊ falou
- Áudio é registro DIFERENTE de texto — esses trechos vão alimentar a parte de "como você fala falando", não escrevendo

### 3. E-mail — exportar enviados

**Gmail:**
1. https://takeout.google.com
2. Selecione "Gmail"
3. Em filtros, marque apenas a label "Enviados"
4. Exporte em `.mbox`
5. Use https://www.mboxviewer.com (ou similar) pra ler

**Outlook:**
1. Abra Outlook desktop
2. Arquivo → Abrir e Exportar → Importar/Exportar
3. Exportar para arquivo → Arquivo de Dados do Outlook (.pst)
4. Selecione "Itens Enviados"

**Filtre por:** e-mails comerciais, follow-ups com cliente, respostas a leads. Pule auto-respostas e e-mails de 1 linha.

### 4. Posts em redes sociais

**LinkedIn:**
1. https://www.linkedin.com/mypreferences/d/download-my-data
2. Selecione "Posts" → Solicitar arquivo
3. Chega em 24h por e-mail

**Instagram:**
1. Configurações → Sua atividade → Baixar suas informações
2. Selecione período e formato JSON
3. Em "Conteúdo" → "Posts" e "Stories"

### 5. Outras fontes válidas

- **Áudio de lives/cursos** transcritas via Whisper
- **Mensagens de Slack/Discord** (export do workspace)
- **Comentários no YouTube** próprio
- **Documentos internos** que você escreveu (manuais, SOPs, propostas)
- **Transcrição de reuniões** Google Meet (precisa estar habilitado)

## Brand Voice — fontes diferentes

Pra Brand Voice (institucional), foque em:
- Site oficial da empresa (Home, Sobre, Páginas de produto)
- Apresentações comerciais (PPTX, decks de vendas)
- Posts oficiais nas redes da empresa
- E-mails de campanha (Mailchimp, RD Station, ActiveCampaign)
- Transcrições de webinars institucionais
- Manuais de marca existentes (se tiver)

## Como consolidar o material

1. Crie uma pasta `corpus/` no seu computador
2. Salve cada fonte como um `.txt` separado:
   ```
   corpus/
   ├── whatsapp-clientes.txt
   ├── whatsapp-equipe.txt
   ├── emails-vendas.txt
   ├── zoom-transcripts.txt
   └── posts-linkedin.txt
   ```
3. Não junte tudo num arquivo só — o prompt mestre vai pedir pra você identificar contextos

## Checklist final antes de extrair

- [ ] Tenho material de pelo menos 3 contextos diferentes
- [ ] Pelo menos 200 mensagens/trechos
- [ ] Removi mensagens curtas demais (< 20 chars)
- [ ] Anonimizei nomes de clientes/leads
- [ ] Removi informações sensíveis (CPF, senhas, valores específicos confidenciais)
- [ ] Tenho pelo menos 1 fonte de áudio transcrito (se quiser cobrir registro oral)

Pronto. Próximo passo: [`02-prompt-mestre.md`](02-prompt-mestre.md) — colar isso na IA e gerar o guide.
