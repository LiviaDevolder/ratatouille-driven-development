# Checklist INVEST

Valide TODA história contra estes critérios antes de entregar.

## I — Independente
- [ ] A história entrega valor sozinha, sem depender de outra história estar pronta?
- [ ] Se há dependência, ela está documentada nas notas?

## N — Negociável
- [ ] A história descreve O QUÊ e POR QUÊ, sem ditar o COMO?
- [ ] A implementação técnica está ausente dos critérios de aceitação?

## V — Valiosa
- [ ] O benefício é um resultado real de negócio (não técnico)?
- [ ] Um stakeholder não-técnico entenderia o valor?

## E — Estimável
- [ ] Um dev consegue estimar o esforço sem precisar de mais informações?
- [ ] O escopo está claro o suficiente?

## S — Small (Pequena)
- [ ] A história cabe em um sprint (≤ 2 semanas)?
- [ ] Se é maior, foi sugerida uma quebra?

## T — Testável
- [ ] Todo critério de aceitação é verificável com sim/não?
- [ ] Não há critérios subjetivos ("deve ser rápido", "deve ser intuitivo")?
- [ ] Cenários de erro e limites estão cobertos?

## Sinais de Problema

| Sinal | Ação |
|-------|------|
| Papel é "usuário" genérico | Pergunte quem especificamente |
| Ação contém "e" | Separe em duas histórias |
| Benefício repete a ação | Busque o "por quê" real |
| Critério é subjetivo | Reescreva com métrica observável |
| > 8 critérios | A história provavelmente é grande demais |
