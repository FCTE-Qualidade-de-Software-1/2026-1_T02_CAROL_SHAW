# Manutenibilidade

Esta página registra a execução da avaliação de **Manutenibilidade** no commit `ba6db878b9dfa36fb034916612c4cf58ddf43475`, mantendo rastreabilidade com as métricas M1, M2, M3, M4 e M5 especificadas na Fase 2 e com os procedimentos da Fase 3.

> **Resultado:** M1 atingiu 28,43%. M2, M3, M4 e M5 não foram calculadas devido à ausência dos denominadores ou registros experimentais previstos nos respectivos métodos.

---

## 1. Obtenção das Medidas

### 1.1 M1 - Execução de reusabilidade

O inventário considerou como ativo:

- cada componente Svelte fora das famílias de UI;
- cada família de UI com arquivo público `index.ts`, contada como um ativo;
- cada módulo de hook, utilitário ou action;
- cada folha de estilo compartilhada.

Arquivos internos de uma mesma família de UI não foram contados separadamente. Um ativo foi marcado como reutilizado quando possuía imports em dois ou mais arquivos de contexto distintos.

$$
M1 = \frac{\text{ativos reutilizados}}{\text{total de ativos}} \times 100
$$

$$
M1 = \frac{29}{102} \times 100 = 28{,}43\%
$$

| Tipo de ativo | Total | Reutilizados |
| :------------ | ----: | ------------: |
| Componentes Svelte independentes | 68 | 20 |
| Famílias de componentes de UI | 14 | 1 |
| Hooks | 3 | 0 |
| Utilitários | 12 | 6 |
| Actions | 4 | 2 |
| Estilos compartilhados | 1 | 0 |
| **Total** | **102** | **29** |

<p align="center">Tabela 1 - Dados brutos da M1 por tipo de ativo. Fonte: Equipe Carol Shaw, 2026.</p>

A relação dos 29 ativos reutilizados e suas contagens de contextos está em [Evidência da M1](evidencias/m1.md).

### 1.2 M2 - Complexidade de modificação

$$
M2 = \frac{\text{tempo total de trabalho}}{\text{número de modificações}}
$$

- Registros de início, fim e tempo útil: **não disponíveis**;
- Amostra controlada de modificações: **não disponível**;
- Resultado: **não calculado**.

Datas de commits não representam tempo útil de trabalho e, por isso, não foram usadas como aproximação.

### 1.3 M3 - Completude funcional das funções de teste embutidas

$$
M3 = \frac{\text{testes implementados}}{\text{testes requeridos na especificação}} \times 100
$$

- Testes implementados e executados: **disponíveis**;
- Cenários de teste requeridos na especificação: **não enumerados**;
- Resultado: **não calculado**.

Como evidência auxiliar, foram obtidos 45 testes Jest aprovados no backend e 36 testes Pytest aprovados, além de 10 resultados `xfail` e 1 teste ignorado. O frontend não contém arquivos reconhecidos pelo Vitest. Esses valores não permitem calcular M3 sem o total de cenários requeridos.

### 1.4 M4 - Suficiência das funções de diagnóstico

$$
M4 = \frac{\text{funções de diagnóstico implementadas}}{\text{funções exigidas na especificação}} \times 100
$$

- Mecanismos implementados: **logging Winston, logger por controlador, logs em arquivo, tratamento de exceções globais e endpoints de health check**;
- Funções exigidas na especificação: **não enumeradas**;
- Resultado: **não calculado**.

A presença dos mecanismos confirma capacidade de diagnóstico, mas não permite medir completude sem uma lista normativa de funções requeridas.

### 1.5 M5 - Condensabilidade

$$
M5 = \frac{\text{componentes não impactados por mudanças em outros}}{\text{total de componentes}} \times 100
$$

- Estrutura de módulos e imports: **disponível**;
- Regra objetiva para determinar impacto: **não definida**;
- Resultado: **não calculado**.

O critério da Fase 3 menciona dependências de entrada "relevantes", mas não estabelece limiar, direção de impacto, granularidade dos componentes nem tratamento de dependências indiretas. Qualquer percentual dependeria de uma convenção criada durante a execução.

---

## 2. Comparação com os Critérios

| Métrica | Desejável | Aceitável | Inaceitável | Resultado | Classificação |
| :------ | :-------- | :-------- | :----------- | :-------- | :------------ |
| M1 | >= 80% | 50% a 79% | < 50% | 28,43% | Inaceitável |
| M2 | <= 4 h/modificação | > 4 e <= 8 h/modificação | > 8 h/modificação | Não calculado | Inconclusiva |
| M3 | 100% | 80% a 99% | < 80% | Não calculado | Inconclusiva |
| M4 | 100% | 80% a 99% | < 80% | Não calculado | Inconclusiva |
| M5 | >= 80% | 50% a 79% | < 50% | Não calculado | Inconclusiva |

<p align="center">Tabela 2 - Comparação das métricas de Manutenibilidade com os critérios da Fase 2. Fonte: Equipe Carol Shaw, 2026.</p>

---

## 3. Respostas às Questões GQM

| Questão | Métrica | Resposta | Hipótese |
| :------ | :------ | :------- | :------- |
| Q1. Quão elevado é o reaproveitamento de componentes e ativos do frontend? | M1 | 28,43%, classificação inaceitável | H1 refutada |
| Q2. Qual é o esforço médio necessário para realizar modificações? | M2 | Inconclusiva | H2 não confirmada nem refutada |
| Q3. Quão completa está a implementação dos testes previstos? | M3 | Inconclusiva | H3 não confirmada nem refutada |
| Q4. Quão completa está a implementação de monitoramento e diagnóstico? | M4 | Inconclusiva | H4 não confirmada nem refutada |
| Q5. Quão independente é a estrutura modular diante de modificações? | M5 | Inconclusiva | H5 não confirmada nem refutada |

<p align="center">Tabela 3 - Respostas às questões GQM de Manutenibilidade. Fonte: Equipe Carol Shaw, 2026.</p>

---

## 4. Julgamento e Ações de Melhoria

O resultado de M1 indica baixo reaproveitamento segundo o critério estabelecido. Dos 102 ativos, 73 aparecem em menos de dois contextos. Parte deles pode ser corretamente específica de uma tela, mas o critério da métrica não distingue especialização legítima de duplicação.

As ações fundamentadas pelas evidências são:

1. revisar os 73 ativos não reutilizados e remover os que não possuem import;
2. consolidar padrões repetidos de formulários, modais e layouts em componentes compartilhados;
3. manter famílias de UI expostas por módulos públicos e documentar seu uso;
4. criar a matriz de cenários requeridos para permitir o cálculo de M3;
5. adicionar testes de frontend e corrigir os 10 erros identificados pelo `svelte-check`;
6. definir a lista mínima de diagnóstico exigida para M4;
7. formalizar a granularidade e o limiar de impacto antes de calcular M5;
8. registrar tempo útil em tarefas futuras para viabilizar M2.

---

## 5. Rastreabilidade

- [Propósito e Escopo - Fase 1](../fase1/proposito_escopo.md)
- [Especificação da Manutenibilidade - Fase 2](../fase2/manutenibilidade.md)
- [Plano da Manutenibilidade - Fase 3](../fase3/manutenibilidade.md)
- [Evidência da M1](evidencias/m1.md)
- [Evidências de Testes](evidencias/testes.md)
- [Visão Geral da Fase 4](introducao.md)

---

## 6. Referências

> 1. SOARES RAMOS, Cristiane. Processo de Avaliação de Produto de Software. Brasília: UnB, 2025. Material de aula (slides). Acesso em: 11/06/2026.
>
> 2. SOARES RAMOS, Cristiane. Projeto Final da Disciplina: Avaliação da Qualidade de Produto de Software. Brasília: UnB, 2026. Enunciado do trabalho final. Acesso em: 11/06/2026.
>
> 3. UNB-MDS. 2025-1-NoFluxoUNB. Disponível em: https://github.com/unb-mds/2025-1-NoFluxoUNB. Acesso em: 11/06/2026.

---

## Histórico de Versões

| Versão | Data | Descrição | Autor(es) | Revisor(es) | Data de Revisão | Alterações Realizadas |
| :----- | :--- | :-------- | :-------- | :----------- | :--------------- | :-------------------- |
| 1.0 | 11/06/2026 | Registro inicial da execução da avaliação de Manutenibilidade | Equipe Carol Shaw |  |  |  |
| 1.1 | 11/06/2026 | Cálculo da M1, evidências auxiliares e registro das métricas inviáveis | Equipe Carol Shaw |  |  |  |
| 1.2 | 11/06/2026 | Revisão da redação acadêmica da página | Equipe Carol Shaw |  |  |  |
