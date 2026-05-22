# RDD Agents — Instruções de Orquestração

## Sobre

Este projeto usa dois subagentes especializados para transformar requisitos vagos em planos de desenvolvimento:

- **po-agent** → Refina requisitos em user stories (modelo INVEST)
- **planner-agent** → Transforma stories em tasks com estimativas e ordem de execução

## Fluxo Orquestrado (modo automático)

Quando o usuário pedir para "planejar uma feature" ou "preparar requisitos para desenvolvimento":

1. Delegar ao `po-agent` → salva stories em `docs/stories/`
2. Delegar ao `planner-agent` → lê stories e salva plano em `docs/plans/`
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

Os agentes podem carregar referências adicionais de `skills/po-agent/references/` e `skills/planner-agent/references/` para templates e checklists.
