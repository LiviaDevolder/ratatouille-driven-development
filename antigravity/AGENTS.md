# RDD Agents — Instruções de Orquestração

## Sobre

Este projeto usa dois agentes especializados para transformar requisitos vagos em planos de desenvolvimento:

- **po-agent** → Refina requisitos em user stories (modelo INVEST)
- **planner-agent** → Transforma stories em tasks com estimativas e ordem de execução

## Fluxo Orquestrado (modo automático)

Quando o usuário pedir para "planejar uma feature" ou "preparar requisitos para desenvolvimento":

1. Acionar o `po-agent` → salva stories em `docs/stories/`
2. Acionar o `planner-agent` → lê stories e salva plano em `docs/plans/`
3. Apresentar resumo consolidado

## Fluxo Independente (modo manual)

- "Escreva stories para [feature]" → aciona `po-agent`
- "Planeje o desenvolvimento de [stories]" → aciona `planner-agent`

## Convenções

- **Idioma de saída:** PT-BR sempre
- **Um arquivo por story** em `docs/stories/`
- **Um arquivo por plano** em `docs/plans/`
- **Nomes de arquivo:** lowercase, kebab-case, descritivo (ex: `filtro-status-veiculos.md`)

## Skills

Os agentes carregam referências de `.agents/skills/po-agent/references/` e `.agents/skills/planner-agent/references/` para templates e checklists.
