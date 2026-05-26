# Skill voice-apply

Skill opcional pra ativar o Voice Guide on-demand em ferramentas que suportam skills (Claude Code, Claude Desktop com plugin).

## Quando vale instalar a skill

| Situacao | Vale skill? |
|---|---|
| Voce so usa Claude.ai conversacional | **Nao** — usa Project Knowledge (mais simples) |
| Voce usa ChatGPT/Gemini | **Nao** — usa Custom GPT / Gems |
| Voce usa Claude Code com varios projetos | **Sim** — skill carrega so quando precisa, nao infla CLAUDE.md |
| Voce quer disparo declarativo ("redige no meu tom") | **Sim** — skill responde a triggers |
| Voce quer automacao via MCP | **Nao precisa de skill** — coloca guide no system prompt do node LLM |

## Como instalar

Veja `voice-apply/SKILL.md` pra instrucoes detalhadas.

Resumo:
1. Copie `voice-apply/` pra `~/.claude/skills/`
2. Edite `voice-apply/voice-guide-path.txt` com o path do seu voice guide
3. Pronto — sessoes novas do Claude Code carregam a skill

## Estrutura

```
skill/
├── README.md                    # este arquivo
└── voice-apply/
    ├── SKILL.md                 # definicao da skill (frontmatter + instrucoes)
    └── voice-guide-path.txt     # path configuravel pro voice guide
```
