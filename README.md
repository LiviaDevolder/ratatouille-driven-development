# 🐀 RDD Agents — Sua Brigada de Cozinha Digital

> Subagentes + Skills para Claude Code que transformam requisitos vagos em histórias de usuário e planos de desenvolvimento.
>
> Inspirado na palestra **"Ratatouille Driven Development: Cozinhando com requisitos vagos e falta de tempo"** — porque requisito vago + projeto apressado = código spaghetti.

---

## O que é isso?

Dois agentes especializados para o [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) que automatizam as etapas que a maioria dos devs pula por falta de tempo:

| Agente               | Papel na Cozinha           | O que faz                                                               |
| -------------------- | -------------------------- | ----------------------------------------------------------------------- |
| 🧑‍🍳 **po-agent**      | Sous Chef (PO)             | Recebe requisitos vagos → user stories com critérios de aceite (INVEST) |
| 📋 **planner-agent** | Chef de Partie (Tech Lead) | Recebe user stories → plano de dev com tasks, estimativas e ordem       |

**Você é o Chef Executivo** — revisa, aprova e implementa.

---

## Estrutura do Projeto

```
ratatouille-driven-development/
├── .claude/
│   └── agents/                    # Subagentes (Claude Code carrega automaticamente)
│       ├── po-agent.md
│       └── planner-agent.md
├── skills/                        # Agent Skills (formato Anthropic oficial)
│   ├── po-agent/
│   │   ├── SKILL.md               # Instruções do skill
│   │   └── references/
│   │       ├── story-template.md   # Template de user story
│   │       └── invest-checklist.md # Checklist INVEST
│   └── planner-agent/
│       ├── SKILL.md
│       └── references/
│           └── plan-template.md    # Template de plano de dev
├── docs/
│   ├── stories/                   # 📝 Saída do po-agent
│   └── plans/                     # 📋 Saída do planner-agent
├── CLAUDE.md                      # Instruções de orquestração
├── LICENSE
└── README.md
```

**Por que dois formatos?** Os arquivos em `.claude/agents/` são subagentes que o Claude Code invoca automaticamente via `Task`. Os arquivos em `skills/` seguem o [padrão oficial de Agent Skills da Anthropic](https://github.com/anthropics/skills) e servem como referência carregada dinamicamente. Os subagentes usam os `references/` dos skills para templates e checklists — isso mantém os prompts concisos e a documentação reutilizável.

---

## Pré-requisitos

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) instalado
- Node.js 18+

---

## Instalação

### Opção 1: Copiar para o seu projeto (recomendado)

```bash
git clone https://github.com/LiviaDevolder/ratatouille-driven-development.git

# Copiar subagentes
cp -r ratatouille-driven-development/.claude SEU-PROJETO/

# Copiar skills e referências
cp -r ratatouille-driven-development/skills SEU-PROJETO/

# Copiar diretórios de saída
cp -r ratatouille-driven-development/docs SEU-PROJETO/

# Adicionar conteúdo do CLAUDE.md ao seu projeto
cat ratatouille-driven-development/CLAUDE.md >> SEU-PROJETO/CLAUDE.md
```

### Opção 2: Subagentes globais

```bash
# Disponível em todos os projetos
cp ratatouille-driven-development/.claude/agents/*.md ~/.claude/agents/
```

> **Nota:** Na instalação global, os agentes não terão acesso aos `references/`. Copie também a pasta `skills/` para o projeto onde for usar.

---

## Como Usar

### 🔄 Modo Orquestrado (dois agentes em sequência)

Ideal quando você recebe um requisito vago e quer ir direto ao plano:

```
> Recebi esse requisito do cliente: "preciso de um filtro na tela de veículos".
> Refine em stories e depois crie o plano de desenvolvimento.
```

Claude Code vai:

1. Acionar o **po-agent** → gerar stories em `docs/stories/`
2. Acionar o **planner-agent** → gerar o plano em `docs/plans/`
3. Apresentar um resumo consolidado

### 🎯 Modo Independente

#### Só o PO Agent:

```
> Use o po-agent para escrever user stories: "o cliente quer exportar relatórios em PDF"
```

#### Só o Planner Agent:

```
> Use o planner-agent para planejar o desenvolvimento das stories em docs/stories/
```

---

## Exemplo Completo

### Entrada (requisito vago do cliente)

```
"O cliente quer melhorar a busca de veículos no sistema"
```

### Saída do po-agent → `docs/stories/busca-veiculos.md`

```markdown
# Busca de veículos por placa ou modelo

## História de Usuário

Como **operador de pátio da aplicação PVX**,
eu quero **buscar veículos por placa ou modelo na tela central**,
para que **eu consiga localizar rapidamente um veículo específico
sem navegar por toda a listagem**.

## Critérios de Aceitação

- [ ] Campo de busca visível na parte superior da tela central
- [ ] Aceita texto livre (modelo) e formato de placa (ABC-1234 ou ABC1D23)
- [ ] Resultados filtrados conforme digitação, a partir do 3º caractere
- [ ] Mensagem "Nenhum veículo encontrado" quando sem resultados
- [ ] Botão de limpar retorna à listagem completa
```

### Saída do planner-agent → `docs/plans/plano-busca-veiculos.md`

```markdown
# Plano: Busca de Veículos

## Resumo

Implementar campo de busca na tela central do PVX para filtrar
veículos por placa ou modelo em tempo real.

## Visão Geral

| História                  | Complexidade | Tarefas |
| ------------------------- | ------------ | ------- |
| Busca por placa ou modelo | 5            | 4       |

---

### Tarefas

#### 1. Criar componente SearchBar — 2

- **O quê:** Input com ícone de busca e botão de limpar
- **Onde:** `src/components/SearchBar/`
- **Pronto quando:** Componente renderiza e aceita input

#### 2. Implementar lógica de filtro — 3

- **O quê:** Filtrar listagem por placa ou modelo a partir do 3º caractere com debounce
- **Onde:** `src/hooks/useVehicleFilter.ts`
- **Pronto quando:** Filtro funciona para ambos os formatos

#### 3. Tratar estado vazio — 1

- **O quê:** Mensagem quando nenhum resultado encontrado
- **Pronto quando:** Mensagem aparece/desaparece corretamente

#### 4. Testes — 2

- **O quê:** Unitários para filtro + teste de componente
- **Pronto quando:** Cobertura dos cenários dos critérios de aceite

### Ordem de Execução

1 → 2 → 3 → 4 (sequencial, cada um depende do anterior)
```

---

## Personalização

### Idioma

Os agentes produzem saída em **PT-BR** por padrão. Para mudar, edite a instrução de idioma nos arquivos `.claude/agents/*.md`.

### Modelo

Ambos usam `model: sonnet` (balanço entre velocidade e qualidade). Opções:

- `opus` — mais capaz, mais lento, mais caro
- `haiku` — mais rápido, mais barato
- `inherit` — usa o modelo da conversa principal

### Estimativas

O planner-agent usa **Fibonacci story points** (1, 2, 3, 5, 8, 13, 21). Para ajustar a escala ou os referenciais de esforço, edite `skills/planner-agent/references/plan-template.md`.

### Templates

Edite os arquivos em `skills/*/references/` para adaptar os templates de saída ao padrão da sua empresa.

### Contexto do Projeto

Adicione informações do seu projeto no `CLAUDE.md` (stack, convenções, padrões). Os agentes usam esse contexto automaticamente.

---

## Como Funciona (Arquitetura)

```
Requisito vago do cliente
  │
  ▼
🧑‍🍳 po-agent (subagente)
  │  ├── Lê: skills/po-agent/references/
  │  ├── Faz perguntas de discovery
  │  ├── Classifica (epic/story/task)
  │  ├── Escreve user stories (INVEST)
  │  └── Salva: docs/stories/*.md
  │
  ▼
📋 planner-agent (subagente)
  │  ├── Lê: docs/stories/*.md
  │  ├── Lê: skills/planner-agent/references/
  │  ├── Explora codebase (Grep/Glob)
  │  ├── Decompõe em tasks técnicas
  │  ├── Estima complexidade (Fibonacci: 1-21)
  │  └── Salva: docs/plans/*.md
  │
  ▼
👩‍💻 Você (Chef Executivo)
   └── Revisa, ajusta e implementa
```

---

## Contribuindo

Ideias de contribuição:

- Novos agentes (code-reviewer, test-writer, etc.)
- Melhorias nos prompts e templates
- Exemplos de uso em diferentes stacks
- Traduções dos prompts

---

## Sobre

Criado por **Lívia Devolder** como material de apoio da palestra **"Ratatouille Driven Development: Cozinhando com requisitos vagos e falta de tempo"** — TDC 2026.

🎤 [Slides](https://drive.google.com/file/d/1rYeNAscJD3wj__3nbQSp3f0n20d57Qao/view?usp=share_link) · 💼 [LinkedIn](https://www.linkedin.com/in/liviadevolder/) · 🐙 [GitHub](https://github.com/LiviaDevolder)

---

## Licença

MIT — use, modifique e compartilhe à vontade.
