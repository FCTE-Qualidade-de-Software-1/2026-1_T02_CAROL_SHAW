# Sobre a Fase 4

## 1. Introdução

A Fase 4 executa o plano definido nas etapas anteriores por meio da obtenção das medidas, da comparação com os critérios da Fase 2 e do julgamento dos resultados. A avaliação foi realizada sobre o commit [`ba6db878`](https://github.com/unb-mds/2025-1-NoFluxoUNB/commit/ba6db878b9dfa36fb034916612c4cf58ddf43475) do [NoFluxoUNB](https://github.com/unb-mds/2025-1-NoFluxoUNB), com coleta em 11/06/2026.

---

## 2. Resultados Consolidados

| Característica | Métrica | Resultado | Classificação |
| :------------- | :------ | :-------- | :------------ |
| Adequação Funcional | CRF | 60,00% (9 de 15 requisitos) | Aceitável |
| Adequação Funcional | TDD | 40,00% (2 de 5 operações) | Inaceitável |
| Adequação Funcional | CF | 70,00% (21 de 30 transações) | Inaceitável |
| Manutenibilidade | M1 | 25,61% (21 de 82 componentes) | Inaceitável |
| Manutenibilidade | M2 | 6,75 dias por modificação | Aceitável |
| Manutenibilidade | M3 | Não calculada | Inconclusiva |
| Manutenibilidade | M4 | 300% (12 de 4 funções) | Desejável |
| Manutenibilidade | M5 | 30,00% (6 de 20 componentes do backend) | Inaceitável |

<p align="center">Tabela 1 - Resultados consolidados da Fase 4. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

A M3 permaneceu inconclusiva porque a especificação não enumera os cenários de teste requeridos. A M4 atingiu 300%, com 12 funções de diagnóstico identificadas para quatro funções previstas, e foi classificada como desejável. Os cálculos, critérios, respostas às questões GQM e dados brutos estão registrados nas páginas de [Adequação Funcional](adequacao_funcional.md), [Manutenibilidade](manutenibilidade.md) e nas evidências vinculadas a esses documentos.

---

## 3. Julgamento e Ações de Melhoria

Os resultados apoiam a priorização do backlog e a gestão do débito técnico, conforme o propósito definido na Fase 1. A avaliação indica as seguintes ações prioritárias:

1. completar os requisitos funcionais ausentes e decompor requisitos compostos em capacidades verificáveis;
2. atualizar os dados de disciplinas e corrigir as divergências da matriz curricular e das recomendações;
3. ampliar o reaproveitamento dos componentes do frontend;
4. definir os cenários de teste requeridos e documentar claramente as funções de diagnóstico previstas;
5. reduzir a concentração de dependências nos principais componentes do backend.

---

## 4. Rastreabilidade

- [Propósito e Escopo - Fase 1](../fase1/proposito_escopo.md)
- [Adequação Funcional - Fase 4](adequacao_funcional.md)
- [Manutenibilidade - Fase 4](manutenibilidade.md)
- [Evidência da CRF](evidencias/adequacao_funcional/crf.md)
- [Evidência da CF](evidencias/adequacao_funcional/cf.md)
- [Evidência da M1](evidencias/manutenibilidade/m1.md)
- [Evidência da M3](evidencias/manutenibilidade/m3.md)
- [Evidência da M5](evidencias/manutenibilidade/m5.md)

---

## Histórico de Versões

| Versão | Data       | Descrição                      | Autor(es)                                                     | Revisor(es) | Data de Revisão | Alterações Realizadas |
| ------ | ---------- | ------------------------------ | ------------------------------------------------------------- | ----------- | --------------- | --------------------- |
| 1.0    | 13/06/2026 | Adiciona texto base da fase 4  | [Caio Duarte](https://github.com/caioduart3) e  [Gabriel Flores](https://github.com/Gabrielfcoelho) | |  |  |
| 1.1    | 13/06/2026 | Alinhamento da consolidação com as evidências e os métodos das fases anteriores | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |  |  |  |
