# Template de Plano de Desenvolvimento

Use este formato para todos os planos produzidos.

```markdown
# Plano: [Nome da Feature/Epic]

## Resumo
[2-3 frases descrevendo o que será construído e por quê]

## Histórias Referenciadas
- `docs/stories/[slug].md` — [título da história]

## Visão Geral

| História | Complexidade | Tarefas |
|----------|-------------|---------|
| [Título] | [1/2/3/5/8/13/21] | [N] |

---

## [Título da User Story]

**Complexidade:** [story points — Fibonacci]
**Abordagem:** [2-3 frases sobre a abordagem técnica — sem prescrever implementação]

### Tarefas

#### 1. [Título da tarefa] — [story points]
- **O quê:** [descrição clara do que precisa ser feito]
- **Onde:** [arquivos/módulos prováveis]
- **Pronto quando:** [critério objetivo de conclusão]

#### 2. [Título da tarefa] — [story points]
- **O quê:** [descrição]
- **Onde:** [arquivos/módulos]
- **Pronto quando:** [critério]

### Riscos e Dependências
- ⚠️ [Risco ou dependência com descrição e mitigação sugerida]

### Ordem de Execução
1. Tarefa X (pré-requisito)
2. Tarefas Y e Z (paralelas)
3. Tarefa W (depende de Y)

---

## Riscos Gerais
- [Riscos que afetam múltiplas histórias]

## Sugestão de Sprint
- **Sprint 1:** [Tarefas A, B, C — foco em fundação]
- **Sprint 2:** [Tarefas D, E, F — foco em features]
```

## Escala de Estimativa (Fibonacci Story Points)

| Pontos | Esforço | Quando usar |
|--------|---------|-------------|
| **1** | ~1-2h | Trivial, sem incerteza |
| **2** | ~meio dia | Simples, bem entendido |
| **3** | ~1 dia | Pouca complexidade, approach claro |
| **5** | ~2-3 dias | Complexidade moderada |
| **8** | ~3-5 dias | Complexo, pode precisar de pesquisa |
| **13** | ~1-2 semanas | Muito complexo, múltiplas incógnitas |
| **21** | ~2+ semanas | Nível de épico → DEVE ser quebrado |

> Pontos válidos: 1, 2, 3, 5, 8, 13, 21. Nunca use valores fora da sequência.
> Se uma tarefa é 13 ou mais, considere seriamente dividi-la.
> Se uma história soma 21+, ela provavelmente é um épico disfarçado.

## Regras

1. Cada tarefa deve ser completável em 1-2 dias por um dev.
2. "Pronto quando" deve ser verificável objetivamente.
3. Tarefas devem respeitar a ordem de dependências.
4. Sem suposições sobre implementação de outras tarefas.
5. Inclua tarefas de spike/pesquisa quando a incerteza for alta.
