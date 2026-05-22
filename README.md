# 🐀 Ratatouille Driven Development

> Agentes de IA que transformam requisitos vagos em histórias de usuário e planos de desenvolvimento.
>
> Inspirado na palestra **"Ratatouille Driven Development: Cozinhando com requisitos vagos e falta de tempo"** — porque requisito vago + projeto apressado = código spaghetti.

---

## O que é isso?

Dois agentes especializados que automatizam as etapas que a maioria dos devs pula por falta de tempo:

| Agente               | Papel na Cozinha           | O que faz                                                               |
| -------------------- | -------------------------- | ----------------------------------------------------------------------- |
| 🧑‍🍳 **po-agent**      | Sous Chef (PO)             | Recebe requisitos vagos → user stories com critérios de aceite (INVEST) |
| 📋 **planner-agent** | Chef de Partie (Tech Lead) | Recebe user stories → plano de dev com tasks, estimativas e ordem       |

**Você é o Chef Executivo** — revisa, aprova e implementa.

---

## Escolha sua ferramenta

Este repositório oferece implementações para duas IDEs agênticas:

| | [Claude Code](claude-code/) | [Google Antigravity](antigravity/) |
|---|---|---|
| **Formato de agente** | `.claude/agents/*.md` | `.agents/skills/**/SKILL.md` |
| **Orquestração** | `CLAUDE.md` | `AGENTS.md` |
| **Modelos** | Claude (Anthropic) | Gemini + Claude + GPT-OSS |
| **README** | [claude-code/README.md](claude-code/README.md) | [antigravity/README.md](antigravity/README.md) |

---

## Estrutura do Repositório

```
ratatouille-driven-development/
├── claude-code/          # Implementação para Claude Code (Anthropic)
│   ├── .claude/agents/   # Subagentes
│   ├── skills/           # Agent Skills (formato Anthropic)
│   ├── docs/             # Saída dos agentes
│   └── CLAUDE.md         # Instruções de orquestração
│
├── antigravity/          # Implementação para Google Antigravity
│   ├── .agents/skills/   # Skills
│   ├── docs/             # Saída dos agentes
│   └── AGENTS.md         # Instruções de orquestração
│
├── LICENSE
└── README.md
```

---

## Fluxo (igual nos dois)

```
Requisito vago do cliente
  │
  ▼
🧑‍🍳 po-agent   →  docs/stories/*.md
  │
  ▼
📋 planner-agent  →  docs/plans/*.md
  │
  ▼
👩‍💻 Você (Chef Executivo)
```

---

## Sobre

Criado por **Lívia Devolder** como material de apoio da palestra **"Ratatouille Driven Development: Cozinhando com requisitos vagos e falta de tempo"**.

🎤 [Slides](https://drive.google.com/file/d/1rYeNAscJD3wj__3nbQSp3f0n20d57Qao/view?usp=share_link) · 💼 [LinkedIn](https://www.linkedin.com/in/liviadevolder/) · 🐙 [GitHub](https://github.com/LiviaDevolder)

---

## Licença

MIT — use, modifique e compartilhe à vontade.
