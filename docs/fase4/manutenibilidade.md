# Manutenibilidade

Esta página apresenta a execução da avaliação de **Manutenibilidade** sobre o commit [`ba6db878b9dfa36fb034916612c4cf58ddf43475`](https://github.com/unb-mds/2025-1-NoFluxoUNB/commit/ba6db878b9dfa36fb034916612c4cf58ddf43475) do [NoFluxoUNB](https://github.com/unb-mds/2025-1-NoFluxoUNB), em conformidade com as métricas especificadas na Fase 2 e com os procedimentos definidos na Fase 3.

> **Resultado:** a M1 atingiu 28,43% e a M5 atingiu 30,00% no backend TypeScript; ambas foram classificadas como inaceitáveis. As métricas M2, M3 e M4 permaneceram inconclusivas devido à ausência dos registros experimentais ou dos denominadores exigidos pelos respectivos métodos.

---

## 1. Obtenção das Medidas

### 1.1 M1 - Execução de reusabilidade

Para a M1, o inventário adotou as seguintes unidades de análise:

- cada componente Svelte fora das famílias de UI;
- cada família de UI com arquivo público `index.ts`, contada como um ativo;
- cada módulo de hook, utilitário ou action;
- cada folha de estilo compartilhada.

Os arquivos internos de uma mesma família de interface não foram contabilizados separadamente. Um ativo foi classificado como reutilizado quando era importado por dois ou mais arquivos pertencentes a contextos distintos.

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

<p align="center">Tabela 1 - Dados brutos da M1 por tipo de ativo. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

A relação dos 29 ativos reutilizados e suas contagens de contextos está em [Evidência da M1](evidencias/manutenibilidade/m1.md).

### 1.2 M2 - Complexidade de modificação

$$
M2 = \frac{\text{tempo total de trabalho}}{\text{número de modificações}}
$$

- Registros de início, fim e tempo útil: **não disponíveis**;
- Amostra controlada de modificações: **não disponível**;
- Situação: **não calculada e inconclusiva**.

As datas registradas no [histórico de commits](https://github.com/unb-mds/2025-1-NoFluxoUNB/commits/main/) não representam o tempo efetivo dedicado a cada modificação. Por esse motivo, não foram utilizadas como aproximação do esforço de trabalho.

### 1.3 M3 - Completude funcional das funções de teste embutidas

$$
M3 = \frac{\text{testes implementados}}{\text{testes requeridos na especificação}} \times 100
$$

- Testes implementados e executados: **disponíveis**;
- Cenários de teste requeridos na especificação: **não enumerados**;
- Situação: **não calculada e inconclusiva**.

Como evidência auxiliar, foram obtidos 45 testes aprovados pelo [Jest](https://jestjs.io/docs/getting-started) no backend e 36 testes aprovados pelo [pytest](https://docs.pytest.org/), além de 10 falhas esperadas (`xfail`) e 1 teste ignorado. No frontend, o [Vitest](https://vitest.dev/guide/) não localizou arquivos de teste. Essas quantidades não permitem calcular a M3 sem a definição do total de cenários requeridos.

Os comandos, resultados e motivos que impedem o cálculo estão registrados na [Evidência da M3](evidencias/manutenibilidade/m3.md).

### 1.4 M4 - Suficiência das funções de diagnóstico

$$
M4 = \frac{\text{funções de diagnóstico implementadas}}{\text{funções exigidas na especificação}} \times 100
$$

- Mecanismos implementados: **registro estruturado com [Winston](https://github.com/winstonjs/winston), logger por controlador, registros em arquivo, tratamento global de exceções e endpoints de verificação de integridade**;
- Funções exigidas na especificação: **não enumeradas**;
- Situação: **não calculada e inconclusiva**.

A presença desses mecanismos demonstra capacidade de diagnóstico, mas não permite medir sua completude sem uma relação normativa das funções requeridas.

### 1.5 M5 - Condensabilidade

O mapa de dependências internas foi obtido por análise estática dos arquivos `.ts` de produção localizados em [`no_fluxo_backend/src/`](https://github.com/unb-mds/2025-1-NoFluxoUNB/tree/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_backend/src). Foram excluídos testes, arquivos de declaração, código gerado e dependências externas. Um componente foi classificado como **não dependente** quando não importava outro componente interno do backend.

O escopo foi restringido ao backend porque o [Madge 8.0.0](https://github.com/pahen/madge) processou diretamente todos os módulos TypeScript e produziu resultados reproduzíveis por linha de comando. No frontend, as ferramentas examinadas não resolveram de forma confiável as importações declaradas nos componentes `.svelte`. Nos serviços Python, o [Pydeps](https://pydeps.readthedocs.io/) não construiu o grafo em razão de nomes e caminhos incompatíveis com sua resolução de módulos. A exclusão desses subsistemas evita que a medida dependa de conversões, renomeações ou programas auxiliares não previstos no procedimento.

$$
M5 = \frac{\text{componentes não dependentes}}{\text{total de componentes}} \times 100
$$

$$
M5 = \frac{6}{20} \times 100 = 30{,}00\%
$$

| Subsistema | Componentes | Não dependentes | Dependentes | Relações internas |
| :--------- | ----------: | --------------: | ----------: | ----------------: |
| Backend TypeScript | 20 | 6 | 14 | 51 |

<p align="center">Tabela 2 - Dados brutos da M5 no backend. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

O resultado de 30,00% indica que 14 dos 20 componentes do backend possuem ao menos uma dependência interna direta. Não foram identificadas dependências circulares no escopo avaliado.

O mapa, as ferramentas, as relações de maior concentração e os componentes não dependentes estão em [Evidência da M5](evidencias/manutenibilidade/m5.md).

---

## 2. Comparação com os Critérios

| Métrica | Desejável | Aceitável | Inaceitável | Resultado | Classificação |
| :------ | :-------- | :-------- | :----------- | :-------- | :------------ |
| M1 | >= 80% | 50% a 79% | < 50% | 28,43% | Inaceitável |
| M2 | <= 4 h/modificação | > 4 e <= 8 h/modificação | > 8 h/modificação | Não calculado | Inconclusiva |
| M3 | 100% | 80% a 99% | < 80% | Não calculado | Inconclusiva |
| M4 | 100% | 80% a 99% | < 80% | Não calculado | Inconclusiva |
| M5 | >= 80% | 50% a 79% | < 50% | 30,00% (backend) | Inaceitável |

<p align="center">Tabela 3 - Comparação das métricas de Manutenibilidade com os critérios da Fase 2. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

---

## 3. Respostas às Questões GQM

| Questão | Métrica | Resposta | Hipótese |
| :------ | :------ | :------- | :------- |
| Q1. Quão elevado é o reaproveitamento de componentes e ativos do frontend? | M1 | 28,43%, classificação inaceitável | H1 refutada |
| Q2. Qual é o esforço médio necessário para realizar modificações? | M2 | Inconclusiva | H2 não confirmada nem refutada |
| Q3. Quão completa está a implementação dos testes previstos? | M3 | Inconclusiva | H3 não confirmada nem refutada |
| Q4. Quão completa está a implementação de monitoramento e diagnóstico? | M4 | Inconclusiva | H4 não confirmada nem refutada |
| Q5. Quão independentes são os componentes do sistema? | M5 | No backend, 30,00%, classificação inaceitável | H5 refutada no escopo avaliado |

<p align="center">Tabela 4 - Respostas às questões GQM de Manutenibilidade. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

---

## 4. Julgamento e Ações de Melhoria

O resultado da M1 indica baixo reaproveitamento segundo o critério estabelecido. Entre os 102 ativos inventariados, 73 aparecem em menos de dois contextos. Parte desses ativos pode ser legitimamente específica de uma única tela; contudo, a métrica adotada não distingue especialização arquitetural de ausência de reutilização.

A M5 indica baixa independência entre os componentes do backend. O arquivo [`index.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_backend/src/index.ts) concentra 9 dependências internas diretas, [`assistente_controller.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_backend/src/controllers/assistente_controller.ts) possui 8 e [`fluxograma_controller.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_backend/src/controllers/fluxograma_controller.ts) possui 7. Embora não tenham sido encontrados ciclos, essa concentração amplia o conjunto de módulos que precisa ser compreendido e verificado durante alterações nesses componentes.

As ações fundamentadas pelas evidências são:

1. revisar os 73 ativos não reutilizados e remover os que não possuem import;
2. consolidar padrões repetidos de formulários, modais e layouts em componentes compartilhados;
3. manter famílias de UI expostas por módulos públicos e documentar seu uso;
4. criar a matriz de cenários requeridos para permitir o cálculo de M3;
5. adicionar testes de frontend e corrigir os 10 erros identificados pelo `svelte-check`;
6. definir a lista mínima de diagnóstico exigida para M4;
7. registrar tempo útil em tarefas futuras para viabilizar M2;
8. revisar as responsabilidades de `index.ts`, `assistente_controller.ts` e `fluxograma_controller.ts`;
9. reduzir dependências diretas dos controladores por meio das camadas e interfaces já existentes no backend;
10. manter a verificação de ciclos no processo de integração para preservar o resultado atual de ausência de dependências circulares.

---

## 5. Rastreabilidade

- [Propósito e Escopo - Fase 1](../fase1/proposito_escopo.md)
- [Especificação da Manutenibilidade - Fase 2](../fase2/manutenibilidade.md)
- [Plano da Manutenibilidade - Fase 3](../fase3/manutenibilidade.md)
- [Evidência da M1](evidencias/manutenibilidade/m1.md)
- [Evidência da M5](evidencias/manutenibilidade/m5.md)
- [Evidência da M3](evidencias/manutenibilidade/m3.md)
- [Visão Geral da Fase 4](introducao.md)

---

## 6. Referências

> 1. SOARES RAMOS, Cristiane. Processo de Avaliação de Produto de Software. Brasília: UnB, 2025. Material de aula (slides). Acesso em: 11/06/2026.
>
> 2. SOARES RAMOS, Cristiane. Projeto Final da Disciplina: Avaliação da Qualidade de Produto de Software. Brasília: UnB, 2026. Enunciado do trabalho final. Acesso em: 11/06/2026.
>
> 3. UNB-MDS. [2025-1-NoFluxoUNB](https://github.com/unb-mds/2025-1-NoFluxoUNB). Acesso em: 11/06/2026.

---

## Histórico de Versões

| Versão | Data | Descrição | Autor(es) |
| :----- | :--- | :-------- | :-------- |
| 1.0 | 11/06/2026 | Registro inicial da execução da avaliação de Manutenibilidade | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.1 | 11/06/2026 | Cálculo da M1, evidências auxiliares e registro das métricas inviáveis | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.2 | 12/06/2026 | Cálculo da M5 por análise estática de dependências | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.3 | 12/06/2026 | Restrição da M5 ao backend TypeScript para garantir reprodutibilidade | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.4 | 12/06/2026 | Consolidação da execução e da inviabilidade de cálculo da M3 | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
