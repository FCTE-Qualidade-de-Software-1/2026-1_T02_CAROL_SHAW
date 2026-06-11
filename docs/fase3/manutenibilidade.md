# Manutenibilidade

Esta página apresenta o Plano de Avaliação da característica **Manutenibilidade**, detalhando o método de avaliação, as instruções para o avaliador, os recursos e o ambiente necessários e o cronograma das ações. O plano operacionaliza as métricas definidas na Fase 2 (M1, M2, M3, M4 e M5), garantindo que a coleta de dados na Fase 4 seja **repetível e reprodutível**.

> **Objeto de avaliação:** código-fonte do NoFluxoUNB hospedado no GitHub, considerando o ambiente multi-linguagem (TypeScript no frontend, Python e SQL no backend), no estado do repositório fixado para esta avaliação.

---

## 1. Método de Avaliação

A avaliação da Manutenibilidade combina **análise estática de código** e **inspeção documental/manual**, conforme a natureza de cada métrica. Cada método abaixo descreve o procedimento, a fonte de dados e a forma de cálculo.

### 1.1 Visão geral por métrica

A **Tabela 1** resume, para cada métrica, o tipo de método de avaliação e a fonte de dados utilizada.

| Métrica | Nome                                                | Tipo de método                                | Fonte de dados                                |
| :------ | :-------------------------------------------------- | :-------------------------------------------- | :-------------------------------------------- |
| M1      | Execução de reusabilidade                           | Análise estática + inspeção manual            | Código do frontend                            |
| M2      | Complexidade de modificação                         | Análise de histórico / experimento controlado | Issues, commits e registro de tempo           |
| M3      | Completude funcional das funções de teste embutidas | Inspeção documental + execução de ferramenta  | Especificação de requisitos e suíte de testes |
| M4      | Suficiência das funções de diagnóstico              | Inspeção manual                               | Especificação e código de monitoramento/logs  |
| M5      | Condensabilidade                                    | Análise estática de dependências              | Estrutura de módulos/componentes              |

<p align="center">Tabela 1 - "Visão geral do método de avaliação por métrica de Manutenibilidade" Autor: Matheus de Alcântara</p>

---

## 2. Instruções para o Avaliador

As instruções a seguir descrevem, passo a passo, como obter cada medida. Todos os dados brutos coletados devem ser registrados nos formulários da seção 3 e armazenados no repositório para auditoria.

### 2.1 M1 — Execução de reusabilidade

$$
M1 = \frac{\text{Ativos Reutilizados}}{\text{Total de Ativos}} \times 100
$$

1. Definir "ativo" como componente de frontend reutilizável (componentes de UI, hooks, funções utilitárias, estilos compartilhados).
2. Mapear o diretório de componentes do frontend e listar o **total de ativos** existentes.
3. Para cada ativo, verificar via busca no código (ex.: referências/imports) se ele é utilizado em **dois ou mais** contextos distintos; em caso afirmativo, marcá-lo como **ativo reutilizado**.
4. Registrar a contagem de ativos reutilizados e o total no formulário.
5. Calcular M1 aplicando a fórmula.

### 2.2 M2 — Complexidade de modificação

$$
M2 = \frac{\text{Tempo Total de Trabalho}}{\text{Número de Modificações}}
$$

1. Selecionar uma amostra de modificações representativas (ex.: correções de bug e pequenas evoluções) a partir das issues/commits do repositório, ou definir um conjunto de tarefas-padrão a serem executadas em experimento controlado.
2. Para cada modificação, registrar o **tempo útil de trabalho** gasto (em horas), do início da análise até a conclusão e validação.
3. Somar o tempo de todas as modificações (**Tempo Total de Trabalho**) e contar o **Número de Modificações**.
4. Calcular M2 aplicando a fórmula.

### 2.3 M3 — Completude funcional das funções de teste embutidas

$$
M3 = \frac{\text{Testes Implementados}}{\text{Testes Requeridos na Especificação}} \times 100
$$

1. Levantar, na especificação de requisitos/documentação do produto, o conjunto de **cenários de teste requeridos**.
2. Inspecionar a suíte de testes do repositório e identificar os **testes implementados** que cobrem esses cenários.
3. Quando disponível, executar a ferramenta de cobertura do projeto para apoiar a contagem.
4. Registrar o número de testes implementados e o número de testes requeridos.
5. Calcular M3 aplicando a fórmula.

### 2.4 M4 — Suficiência das funções de diagnóstico

$$
M4 = \frac{\text{Funções de Diagnóstico Implementadas}}{\text{Funções Exigidas na Especificação}} \times 100
$$

1. Listar as **funções de diagnóstico, rastreamento de erros e monitoramento** previstas no projeto/especificação (ex.: logging, tratamento de exceções, telemetria, mensagens de erro).
2. Inspecionar o código e a configuração para identificar quais dessas funções estão **efetivamente implementadas**.
3. Registrar o número de funções implementadas e o número de funções exigidas.
4. Calcular M4 aplicando a fórmula.

### 2.5 M5 — Condensabilidade

$$
M5 = \frac{\text{Componentes não impactados por mudanças em outros}}{\text{Total de Componentes}} \times 100
$$

1. Identificar os **componentes/módulos** principais do sistema e elaborar o mapa de dependências entre eles (via ferramenta de análise estática ou inspeção dos imports).
2. Para cada componente, avaliar se uma alteração em outro componente o afetaria diretamente (acoplamento). Componentes sem dependências de entrada relevantes são considerados **não impactados**.
3. Registrar o número de componentes não impactados e o total de componentes.
4. Calcular M5 aplicando a fórmula.

---

## 3. Recursos e Ambiente de Avaliação

### 3.1 Recursos humanos

A avaliação será conduzida pelos membros da equipe atuando como avaliadores. Conhecimento exigido:

- **Informática:** intermediário/avançado — uso de Git, terminal e ferramentas de análise de código.
- **Domínio da aplicação:** conhecimento da arquitetura multi-linguagem do NoFluxoUNB — frontend em **SvelteKit/TypeScript** (com app legado em **Flutter/Dart**), backend em **Express/TypeScript**, serviços de apoio em **Python** (parsing de PDF, scraping e agente de IA) e banco **Supabase/PostgreSQL (SQL)** — e do seu fluxo de funcionalidades.

### 3.2 Hardware

- Computador com acesso à internet capaz de clonar o repositório e executar as ferramentas de análise (mínimo recomendado: 8 GB de RAM).

### 3.3 Software e ferramentas

As ferramentas abaixo foram selecionadas a partir da **inspeção das dependências e configurações reais do repositório do NoFluxoUNB** (`package.json`, `requirements.txt`, `.pylintrc`, `jest.config.js`, `pytest.ini`, `codecov.yml` e os workflows em `.github/workflows/`). Priorizou-se reutilizar o ferramental que o próprio projeto já adota, garantindo reprodutibilidade. Elas estão agrupadas por finalidade nas **Tabelas 2 a 6**.

#### a) Ambiente e gestão de código

A **Tabela 2** lista as ferramentas de ambiente e gestão de código.

| Ferramenta                      | Versão/origem no repositório | Finalidade na avaliação                                          | Métricas  |
| :------------------------------ | :--------------------------- | :--------------------------------------------------------------- | :-------- |
| **Git + GitHub**                | repositório oficial          | Fixar o commit de referência e obter histórico de commits/issues | M2, todas |
| **pnpm** (monorepo, workspaces) | `pnpm@10.12.1`               | Instalar dependências e executar scripts de lint/teste/cobertura | todas     |

<p align="center">Tabela 2 - "Ferramentas de ambiente e gestão de código" Autor: Matheus de Alcântara</p>

#### b) Análise estática e linters

A **Tabela 3** apresenta as ferramentas de análise estática e linters.

| Ferramenta                                                  | Origem no repositório                           | Finalidade na avaliação                                                     | Métricas |
| :---------------------------------------------------------- | :---------------------------------------------- | :-------------------------------------------------------------------------- | :------- |
| **ESLint** (+ `@typescript-eslint`, `eslint-plugin-svelte`) | frontend e backend (`lint`)                     | Identificar code smells e apoiar a contagem de ativos/componentes TS/Svelte | M1, M5   |
| **svelte-check** e **tsc --noEmit** (`type-check`)          | frontend / backend                              | Verificar consistência de tipos e imports entre módulos                     | M5       |
| **pylint**                                                  | `.pylintrc` na raiz                             | Análise estática dos serviços Python                                        | M1, M5   |
| **flake8**, **black**, **isort**, **mypy**                  | `security-and-quality.yml` / `python-tests.yml` | Padronização e checagem estática do código Python                           | M1, M5   |
| **madge** (TS/JS) e **pydeps** (Python) — _a adotar_        | — (não presente; sugerido)                      | Gerar o grafo de dependências entre módulos para medir acoplamento          | M5       |

<p align="center">Tabela 3 - "Ferramentas de análise estática e linters" Autor: Matheus de Alcântara</p>

> Observação: o projeto ainda não possui uma ferramenta dedicada de **grafo de dependências**. Recomenda-se incluir o `madge` (para o código TypeScript/Svelte) e o `pydeps` (para o código Python) para tornar o cálculo de M5 objetivo e auditável; na ausência delas, o mapa de dependências é obtido pela inspeção dos `import`/`require` apoiada pelo ESLint e pelo `tsc`.

#### c) Testes e cobertura

A **Tabela 4** apresenta as ferramentas de testes e cobertura.

| Ferramenta                            | Origem no repositório                             | Finalidade na avaliação                                          | Métricas |
| :------------------------------------ | :------------------------------------------------ | :--------------------------------------------------------------- | :------- |
| **Jest + ts-jest**                    | backend (`test:coverage`, `jest.config.js`)       | Executar e medir cobertura dos testes do backend TS              | M3       |
| **Vitest** (+ coverage)               | frontend Svelte (`test:coverage`)                 | Executar e medir cobertura dos testes unitários do frontend      | M3       |
| **Playwright**                        | frontend (`test:integration`)                     | Testes de integração/E2E como evidência de cobertura de cenários | M3       |
| **pytest + pytest-cov + pytest-mock** | `tests-python/pytest.ini` (`--cov-fail-under=70`) | Executar e medir cobertura dos serviços Python                   | M3       |
| **Codecov**                           | `codecov.yml` (alvo 80%)                          | Consolidar e auditar os relatórios de cobertura                  | M3       |

<p align="center">Tabela 4 - "Ferramentas de testes e cobertura" Autor: Matheus de Alcântara</p>

#### d) Diagnóstico, logging e monitoramento

A **Tabela 5** apresenta as ferramentas de diagnóstico, logging e monitoramento.

| Ferramenta                    | Origem no repositório        | Finalidade na avaliação                                  | Métricas |
| :---------------------------- | :--------------------------- | :------------------------------------------------------- | :------- |
| **Winston**                   | backend (`winston`)          | Verificar implementação de logging estruturado           | M4       |
| **Morgan**                    | backend (`morgan`)           | Verificar registro de requisições HTTP                   | M4       |
| **Helmet**                    | backend (`helmet`)           | Verificar cabeçalhos de segurança/robustez               | M4       |
| **psutil**                    | `requirements_monitor.txt`   | Verificar monitoramento de recursos do sistema           | M4       |
| **logging** / **stack_trace** | app Flutter (`pubspec.yaml`) | Verificar diagnóstico e rastreamento de erros no cliente | M4       |

<p align="center">Tabela 5 - "Ferramentas de diagnóstico, logging e monitoramento" Autor: Matheus de Alcântara</p>

#### e) Apoio à coleta

A **Tabela 6** apresenta os recursos de apoio à coleta.

| Ferramenta                                                       | Finalidade na avaliação                                                | Métricas |
| :--------------------------------------------------------------- | :--------------------------------------------------------------------- | :------- |
| **Documentação do produto** (StoryMap, requisitos, backlog, PBB) | Referência dos cenários de teste e das funções de diagnóstico exigidas | M3, M4   |
| **GitHub Actions** (workflows de CI)                             | Evidência reprodutível da execução de lint/testes/cobertura            | M3, M5   |
| **Planilha de coleta / formulários**                             | Registro auditável dos dados brutos                                    | todas    |

<p align="center">Tabela 6 - "Recursos de apoio à coleta" Autor: Matheus de Alcântara</p>

### 3.4 Massa de dados

Para esta característica, a "massa de dados" corresponde ao próprio **código-fonte e à documentação** do NoFluxoUNB no commit de referência, além do histórico de issues/commits utilizado na amostragem da métrica M2. Não há necessidade de dados-exemplo de execução, uma vez que a avaliação é majoritariamente estática.

### 3.5 Formulários de coleta

Para cada métrica, registrar no repositório uma tabela com: identificador da métrica, valores brutos coletados (numerador e denominador), data da coleta, avaliador responsável e evidências (links/prints).

---

## 4. Cronograma de Avaliação

O cronograma da **Tabela 7** é parte do planejamento da Fase 3 e define **quando** as atividades de coleta e análise da Manutenibilidade serão **executadas na Fase 4**. Ou seja, nesta fase apenas se planeja a agenda; a obtenção das medidas, a comparação com os critérios e o julgamento ocorrerão na Fase 4, conforme este cronograma. Toda a execução está prevista para o período de **07/06/2026 a 10/06/2026**.

| Etapa | Atividade (a executar na Fase 4)                                                          | Métricas | Responsável | Data de execução |
| :---- | :---------------------------------------------------------------------------------------- | :------- | :---------- | :--------------- |
| 1     | Preparação do ambiente: clonar repositório no commit de referência e instalar ferramentas | —        |             | 07/06/2026       |
| 2     | Coleta estática: mapear ativos e componentes; calcular M1 e M5                            | M1, M5   |             | 07/06/2026       |
| 3     | Coleta de testes e diagnóstico: inspeção documental e de código; calcular M3 e M4         | M3, M4   |             | 08/06/2026       |
| 4     | Coleta de esforço: amostragem de modificações e registro de tempo; calcular M2            | M2       |             | 09/06/2026       |
| 5     | Consolidação dos dados brutos e formulários no repositório                                | todas    |             | 09/06/2026       |
| 6     | Verificação cruzada dos resultados e preparação para a Fase 4                             | todas    |             | 10/06/2026       |

<p align="center">Tabela 7 - "Cronograma de execução da avaliação de Manutenibilidade (Fase 4)" Autor: Matheus de Alcântara</p>

---

## 5. Consistência com a Fase 2

Cada elemento deste plano deriva diretamente da especificação da Fase 2: os métodos e ferramentas foram escolhidos para coletar exatamente as métricas M1, M2, M3, M4 e M5 e permitir a comparação com seus respectivos níveis de pontuação e critérios de julgamento. O ambiente (acesso ao código, histórico de commits e documentação) garante a disponibilidade dos dados necessários para todas as medições, assegurando rastreabilidade entre o que foi especificado e o que será executado na Fase 4.

---

## 6. Referências

> 1. SOARES RAMOS, Cristiane. Processo de Avaliação de Produto de Software. Brasília: UnB, 2025/2026. Material de aula (slides). Acesso em: 05/06/2026.

> 2. ISO/IEC 25010:2023. Características e subcaracterísticas de qualidade de software. Disponível em: https://www.iso.org/standard/82998.html. Acesso em: 05/06/2026.

> 3. ISO/IEC 25040:2011. Systems and software engineering — SQuaRE — Evaluation process. Geneva: ISO/IEC, 2011. Acesso em: 05/06/2026.

---

## Histórico de Versões

O histórico de alterações desta página é apresentado na **Tabela 8**.

| Versão | Data       | Descrição                                                                             | Autor(es)                                                     | Revisor(es) | Data de Revisão | Alterações Realizadas |
| ------ | ---------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------- | ----------- | --------------- | --------------------- |
| 1.0    | 05/06/2026 | Criação do Plano de Avaliação da Fase 3 para Manutenibilidade                         | [Matheus de Alcântara](https://github.com/matheusdealcantara) |             |                 |                       |
| 1.1    | 05/06/2026 | Especificação das ferramentas reais a partir da inspeção do repositório do NoFluxoUNB | [Matheus de Alcântara](https://github.com/matheusdealcantara) |             |                 |                       |
| 1.2    | 05/06/2026 | Definição do cronograma de execução (07/06 a 10/06/2026)                              | [Matheus de Alcântara](https://github.com/matheusdealcantara) |             |                 |                       |

<p align="center">Tabela 8 - "Histórico de versões da página Plano de Avaliação" Autor: Matheus de Alcântara</p>
