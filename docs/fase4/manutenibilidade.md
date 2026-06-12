# Manutenibilidade

Esta página registra a execução da avaliação de **Manutenibilidade** no commit `ba6db878b9dfa36fb034916612c4cf58ddf43475`, mantendo rastreabilidade com as métricas avaliadas nesta fase e com os procedimentos da Fase 3.

> **Resultado:** M1 atingiu 28,43% e M5 atingiu 37,28%, ambas na faixa inaceitável. M2, M3 e M4 não foram calculadas devido à ausência dos denominadores ou registros experimentais previstos nos respectivos métodos.

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

O mapa de dependências internas foi obtido por análise estática dos módulos de produção. A unidade de contagem foi o arquivo de código-fonte:

- frontend SvelteKit: arquivos `.ts` e `.svelte` de `no_fluxo_frontend_svelte/src/`;
- backend: arquivos `.ts` de `no_fluxo_backend/src/`;
- serviços Python: módulos de `DBA/`, `mcp_agent/` e serviços de processamento do backend.

Testes, código gerado, dependências externas, documentação e scripts de implantação foram excluídos. Um componente foi classificado como **não dependente** quando não importa, reexporta ou carrega dinamicamente outro componente interno. Assim, mudanças em outros módulos não chegam diretamente a ele por uma relação de dependência.

Foram utilizados **Madge 8.0.0** no código TypeScript, **svelte2tsx 0.7.56** para expor estaticamente os imports dos componentes Svelte e **Pydeps 3.0.6** nos módulos Python.

$$
M5 = \frac{\text{componentes não dependentes}}{\text{total de componentes}} \times 100
$$

$$
M5 = \frac{107}{287} \times 100 = 37{,}28\%
$$

| Subsistema | Componentes | Não dependentes | Dependentes | Relações internas |
| :--------- | ----------: | --------------: | ----------: | ----------------: |
| Frontend SvelteKit | 242 | 79 | 163 | 496 |
| Backend TypeScript | 20 | 6 | 14 | 51 |
| Serviços Python | 25 | 22 | 3 | 4 |
| **Total** | **287** | **107** | **180** | **551** |

<p align="center">Tabela 2 - Dados brutos da M5 por subsistema. Fonte: Equipe Carol Shaw, 2026.</p>

O resultado de 37,28% indica que 180 dos 287 componentes possuem ao menos uma dependência interna direta. A análise também identificou três ciclos no frontend, envolvendo os tipos de curso, matéria e equivalência e duas famílias de componentes de interface.

O mapa, as ferramentas, as relações de maior concentração e os componentes não dependentes estão em [Evidência da M5](evidencias/m5.md).

---

## 2. Comparação com os Critérios

| Métrica | Desejável | Aceitável | Inaceitável | Resultado | Classificação |
| :------ | :-------- | :-------- | :----------- | :-------- | :------------ |
| M1 | >= 80% | 50% a 79% | < 50% | 28,43% | Inaceitável |
| M2 | <= 4 h/modificação | > 4 e <= 8 h/modificação | > 8 h/modificação | Não calculado | Inconclusiva |
| M3 | 100% | 80% a 99% | < 80% | Não calculado | Inconclusiva |
| M4 | 100% | 80% a 99% | < 80% | Não calculado | Inconclusiva |
| M5 | >= 80% | 50% a 79% | < 50% | 37,28% | Inaceitável |

<p align="center">Tabela 3 - Comparação das métricas de Manutenibilidade com os critérios da Fase 2. Fonte: Equipe Carol Shaw, 2026.</p>

---

## 3. Respostas às Questões GQM

| Questão | Métrica | Resposta | Hipótese |
| :------ | :------ | :------- | :------- |
| Q1. Quão elevado é o reaproveitamento de componentes e ativos do frontend? | M1 | 28,43%, classificação inaceitável | H1 refutada |
| Q2. Qual é o esforço médio necessário para realizar modificações? | M2 | Inconclusiva | H2 não confirmada nem refutada |
| Q3. Quão completa está a implementação dos testes previstos? | M3 | Inconclusiva | H3 não confirmada nem refutada |
| Q4. Quão completa está a implementação de monitoramento e diagnóstico? | M4 | Inconclusiva | H4 não confirmada nem refutada |
| Q5. Quão independentes são os componentes do sistema? | M5 | 37,28%, classificação inaceitável | H5 refutada |

<p align="center">Tabela 4 - Respostas às questões GQM de Manutenibilidade. Fonte: Equipe Carol Shaw, 2026.</p>

---

## 4. Julgamento e Ações de Melhoria

O resultado de M1 indica baixo reaproveitamento segundo o critério estabelecido. Dos 102 ativos, 73 aparecem em menos de dois contextos. Parte deles pode ser corretamente específica de uma tela, mas o critério da métrica não distingue especialização legítima de duplicação.

A M5 indica baixa independência entre os componentes. As rotas do fluxograma concentram até 23 dependências internas diretas, enquanto módulos agregadores de interface concentram entre 10 e 17 relações. Os três ciclos encontrados aumentam o risco de propagação de mudanças e dificultam a substituição isolada dos tipos e componentes envolvidos.

As ações fundamentadas pelas evidências são:

1. revisar os 73 ativos não reutilizados e remover os que não possuem import;
2. consolidar padrões repetidos de formulários, modais e layouts em componentes compartilhados;
3. manter famílias de UI expostas por módulos públicos e documentar seu uso;
4. criar a matriz de cenários requeridos para permitir o cálculo de M3;
5. adicionar testes de frontend e corrigir os 10 erros identificados pelo `svelte-check`;
6. definir a lista mínima de diagnóstico exigida para M4;
7. registrar tempo útil em tarefas futuras para viabilizar M2;
8. dividir as rotas de fluxograma em módulos de apresentação e coordenação com interfaces menores;
9. remover os ciclos entre `curso.ts`, `materia.ts` e `equivalencia.ts` por meio de tipos compartilhados sem dependência reversa;
10. revisar os ciclos das famílias `dialog` e `scroll-area`, evitando que componentes internos importem seus próprios módulos agregadores.

---

## 5. Rastreabilidade

- [Propósito e Escopo - Fase 1](../fase1/proposito_escopo.md)
- [Especificação da Manutenibilidade - Fase 2](../fase2/manutenibilidade.md)
- [Plano da Manutenibilidade - Fase 3](../fase3/manutenibilidade.md)
- [Evidência da M1](evidencias/m1.md)
- [Evidência da M5](evidencias/m5.md)
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
| 1.3 | 12/06/2026 | Cálculo da M5 por análise estática de dependências | Equipe Carol Shaw |  |  |  |
