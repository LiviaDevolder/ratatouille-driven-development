# 🐀 RDD Agents — Google Antigravity

> Skills para [Google Antigravity](https://antigravity.google/docs/home) que transformam requisitos vagos em histórias de usuário e planos de desenvolvimento.
>
> Inspirado na palestra **"Ratatouille Driven Development: Cozinhando com requisitos vagos e falta de tempo"** — porque requisito vago + projeto apressado = código spaghetti.

---

## O que é isso?

Dois agentes especializados para o Google Antigravity que automatizam as etapas que a maioria dos devs pula por falta de tempo:

| Agente               | Papel na Cozinha           | O que faz                                                               |
| -------------------- | -------------------------- | ----------------------------------------------------------------------- |
| 🧑‍🍳 **po-agent**      | Sous Chef (PO)             | Recebe requisitos vagos → user stories com critérios de aceite (INVEST) |
| 📋 **planner-agent** | Chef de Partie (Tech Lead) | Recebe user stories → plano de dev com tasks, estimativas e ordem       |

**Você é o Chef Executivo** — revisa, aprova e implementa.

---

## Estrutura do Projeto

```
antigravity/
├── .agents/
│   └── skills/                    # Skills (Antigravity carrega automaticamente)
│       ├── po-agent/
│       │   ├── SKILL.md           # Definição do skill
│       │   └── references/
│       │       ├── story-template.md   # Template de user story
│       │       └── invest-checklist.md # Checklist INVEST
│       └── planner-agent/
│           ├── SKILL.md
│           └── references/
│               └── plan-template.md    # Template de plano de dev
├── docs/
│   ├── stories/                   # 📝 Saída do po-agent
│   └── plans/                     # 📋 Saída do planner-agent
├── AGENTS.md                      # Instruções de orquestração
└── README.md
```

Os arquivos em `.agents/skills/` seguem o formato nativo de Skills do Google Antigravity. O `AGENTS.md` na raiz funciona como arquivo de instruções de orquestração, equivalente ao `CLAUDE.md` do Claude Code.

---

## Pré-requisitos

- [Google Antigravity](https://antigravity.google/docs/home) instalado (disponível em preview gratuito para macOS, Windows e Linux)

---

## Instalação

### Opção 1: Copiar para o seu projeto (recomendado)

```bash
git clone https://github.com/LiviaDevolder/ratatouille-driven-development.git

# Copiar skills
cp -r ratatouille-driven-development/antigravity/.agents SEU-PROJETO/

# Copiar diretórios de saída
cp -r ratatouille-driven-development/antigravity/docs SEU-PROJETO/

# Adicionar conteúdo do AGENTS.md ao seu projeto
cat ratatouille-driven-development/antigravity/AGENTS.md >> SEU-PROJETO/AGENTS.md
```

### Opção 2: Skills globais

No Antigravity, você pode instalar skills globalmente pelo Manager View ou copiando os diretórios de skill para `~/.agents/skills/`.

> **Nota:** Na instalação global, os agentes não terão acesso aos `references/` relativos ao projeto. Copie também a pasta `.agents/skills/` para o projeto onde for usar.

---

## Como Usar

### 🔄 Modo Orquestrado (dois agentes em sequência)

No **Manager View** do Antigravity, inicie uma conversa com:

```
Recebi esse requisito do cliente: "preciso de um filtro na tela de veículos".
Refine em stories e depois crie o plano de desenvolvimento.
```

O Antigravity vai:

1. Acionar o **po-agent** → gerar stories em `docs/stories/`
2. Acionar o **planner-agent** → gerar o plano em `docs/plans/`
3. Apresentar um resumo consolidado

### 🎯 Modo Independente

#### Só o PO Agent:

```
Use o po-agent para escrever user stories: "o cliente quer exportar relatórios em PDF"
```

#### Só o Planner Agent:

```
Use o planner-agent para planejar o desenvolvimento das stories em docs/stories/
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

### Tarefas

#### 1. Criar componente SearchBar — 2
- **O quê:** Input com ícone de busca e botão de limpar
- **Onde:** `src/components/SearchBar/`
- **Pronto quando:** Componente renderiza e aceita input
```

---

## Como Funciona (Arquitetura)

```
Requisito vago do cliente
  │
  ▼
🧑‍🍳 po-agent (skill)
  │  ├── Lê: .agents/skills/po-agent/references/
  │  ├── Faz perguntas de discovery
  │  ├── Classifica (epic/story/task)
  │  ├── Escreve user stories (INVEST)
  │  └── Salva: docs/stories/*.md
  │
  ▼
📋 planner-agent (skill)
  │  ├── Lê: docs/stories/*.md
  │  ├── Lê: .agents/skills/planner-agent/references/
  │  ├── Explora codebase
  │  ├── Decompõe em tasks técnicas
  │  ├── Estima complexidade (Fibonacci: 1-21)
  │  └── Salva: docs/plans/*.md
  │
  ▼
👩‍💻 Você (Chef Executivo)
   └── Revisa, ajusta e implementa
```

---

## Personalização

### Templates

Edite os arquivos em `.agents/skills/*/references/` para adaptar os templates ao padrão da sua empresa.

### Contexto do Projeto

Adicione informações do seu projeto no `AGENTS.md` (stack, convenções, padrões). Os agentes usam esse contexto automaticamente.

---

## Sobre

Criado por **Lívia Devolder** como material de apoio da palestra **"Ratatouille Driven Development: Cozinhando com requisitos vagos e falta de tempo"** — TDC 2026.

🎤 [Slides](https://drive.google.com/file/d/1rYeNAscJD3wj__3nbQSp3f0n20d57Qao/view?usp=share_link) · 💼 [LinkedIn](https://www.linkedin.com/in/liviadevolder/) · 🐙 [GitHub](https://github.com/LiviaDevolder)

---

## Licença

MIT — use, modifique e compartilhe à vontade.
