# Adequação Funcional

Esta página apresenta o Plano de Avaliação da característica **Adequação Funcional**, detalhando o método de avaliação, as instruções para o avaliador, os recursos e o ambiente necessários e o cronograma das ações. O plano operacionaliza as métricas definidas na Fase 2 (CRF, TDD e CF), garantindo que a coleta de dados na Fase 4 seja **repetível e reprodutível**.

> **Objeto de avaliação:** sistema NoFluxoUNB em execução, considerando tanto o frontend (SvelteKit/TypeScript) quanto o backend (Express/TypeScript e serviços Python), avaliado a partir do estado do repositório fixado para esta avaliação e de sessões de uso controlado com dados acadêmicos reais.

---


## 1. Método de Avaliação

A avaliação da Adequação Funcional combina **inspeção documental**, **execução de testes funcionais** e **análise de logs/resultados**, conforme a natureza de cada métrica. Cada método descreve o procedimento, a fonte de dados e a forma de cálculo.

### 1.1 Visão geral por métrica

| Métrica | Nome                            | Tipo de método                                      | Fonte de dados                                                      |
| ------- | ------------------------------- | --------------------------------------------------- | ------------------------------------------------------------------- |
| CRF     | Cobertura de Requisitos Funcionais | Inspeção documental + verificação de implementação  | Especificação de requisitos e código-fonte / interface da aplicação |
| TDD     | Taxa de Divergência de Dados    | Execução de casos de teste + análise de resultados  | Sessões de teste com dados acadêmicos conhecidos                    |
| CF      | Conformidade Funcional          | Execução de transações-padrão + verificação de saída | Regras e normas acadêmicas da UnB documentadas                      |

<p align="center">Tabela 1 - "Visão geral do método de avaliação por métrica de Adequação Funcional" Autor: Gustavo Oki</p>

---

## 2. Instruções para o Avaliador

As instruções a seguir descrevem, passo a passo, como obter cada medida. Todos os dados brutos coletados devem ser registrados nos instrumentos de coleta da seção 3 e armazenados no repositório para auditoria.

### 2.1 CRF — Cobertura de Requisitos Funcionais

$$
CRF = \frac{\text{n° funções declaradas na especificação de requisitos} - \text{n° funções ausentes ou incorretas}}{\text{n° funções declaradas na especificação de requisitos}} \times 100
$$

1. Levantar a **lista completa de funções** declaradas na especificação de requisitos do NoFluxoUNB (StoryMap, backlog, PBB ou documento equivalente no repositório).
2. Para cada um dos 15 requisitos funcionais de primeiro nível, verificar no código-fonte e nas evidências visuais se todos os comportamentos descritos possuem implementação. Registrar como "ausente/incorreto" quando não houver implementação ou quando apenas parte do requisito estiver atendida.
3. Somar o número de funções **ausentes ou incorretas**.
4. Registrar o total de funções declaradas e o total de funções ausentes/incorretas no instrumento de coleta.
5. Calcular CRF aplicando a fórmula.

> **Limitação:** a CRF registra presença e aderência estática. A disponibilidade operacional das funcionalidades depende de validação ponta a ponta em ambiente integrado.

---

### 2.2 TDD — Taxa de Divergência de Dados

$$
TDD = \frac{\text{n° operações reportadas com divergência de dados}}{\text{n° total de operações realizadas no período}} \times 100
$$

1. Executar cinco **operações-padrão**: login, importação de histórico acadêmico, verificação do fluxograma gerado, consulta dos pré-requisitos de APC, EDA1 e EDA2 e geração de recomendação para um perfil acadêmico predefinido de Engenharia de Software.
2. Para cada operação, preparar antecipadamente a **saída esperada** (resultado correto) com base nos dados oficiais da UnB (grade curricular, pré-requisitos publicados no SIGAA).
3. Executar cada operação no sistema e registrar a **saída obtida**.
4. Comparar a saída obtida com a saída esperada. Marcar a operação como **divergente** se houver discrepância em qualquer dado relevante (disciplina errada, carga horária incorreta, pré-requisito omitido ou equivocado, etc.).
5. Registrar o número total de operações realizadas e o número de operações com divergência.
6. Calcular TDD aplicando a fórmula.

> **Limitação:** a amostra de cinco operações e um perfil acadêmico permite avaliar os casos executados, mas não representa todos os cursos, perfis e operações suportados pelo produto.

---

### 2.3 CF — Conformidade Funcional

$$
CF = \frac{\text{n° transações de acordo com as normas}}{\text{n° total de transações processadas}} \times 100
$$

1. Adotar como referência a estrutura curricular de Engenharia de Software `6360/1 - 2017.1` publicada no SIGAA.
2. Selecionar os históricos de Engenharia de Software disponíveis e remover documentos duplicados da mesma matrícula, mantendo o mais recente.
3. Processar cada histórico pela página de importação do NoFluxoUNB.
4. Para cada histórico, verificar seis transações independentes: identificação da matriz, cargas horárias, conjunto de 39 componentes obrigatórios, situação dos componentes, equivalências e período letivo atual.
5. Registrar cada transação como **em conformidade** ou **não conforme**.
6. Somar o total de transações e o número de transações em conformidade.
7. Calcular a CF aplicando a fórmula.

> **Limitação:** o resultado abrange somente a estrutura `6360/1 - 2017.1` e não inclui regras de matrícula, limites semestrais ou prazos de conclusão.

---

## 3. Recursos e Ambiente de Avaliação

### 3.1 Recursos humanos

A avaliação será conduzida pelos membros da equipe atuando como avaliadores. Conhecimento exigido:

- **Informática:** (básico/intermediário) uso de navegador web, acesso ao sistema NoFluxoUNB e registro de resultados em planilha.
- **Domínio da aplicação:** conhecimento das funcionalidades do NoFluxoUNB (fluxograma curricular, chatbot de recomendação, pré-requisitos e comparação de cursos) e das normas acadêmicas da UnB (estrutura curricular, regras de pré-requisito e créditos publicadas no SIGAA/DAC).

### 3.2 Hardware

- Computador com acesso à internet capaz de executar o sistema NoFluxoUNB no navegador (mínimo recomendado: 4 GB de RAM).
- Caso a avaliação seja feita localmente, hardware suficiente para rodar o ambiente completo (frontend + backend + banco de dados): mínimo recomendado de 8 GB de RAM.

### 3.3 Software e ferramentas

#### a) Ambiente de execução

| Ferramenta                          | Versão/origem no repositório        | Finalidade na avaliação                                       | Métricas        |
| ----------------------------------- | ----------------------------------- | ------------------------------------------------------------- | --------------- |
| **Navegador web** (Chrome/Firefox)  | versão atual                        | Acessar e operar a interface do NoFluxoUNB durante os testes  | CRF, TDD, CF    |
| **Git + GitHub**                    | repositório oficial                 | Fixar o commit de referência da avaliação                     | todas           |
| **pnpm** (monorepo, workspaces)     | `pnpm@10.12.1`                      | Instalar dependências e iniciar o ambiente local (se aplicável)| todas          |
| **Docker / Supabase CLI** (opcional)| conforme configuração do repositório | Subir banco de dados local para testes controlados           | TDD, CF         |

<p align="center">Tabela 2 - "Ferramentas de ambiente de execução" Autor: Gustavo Oki</p>


#### b) Apoio à inspeção documental

| Ferramenta / Artefato                              | Finalidade na avaliação                                                          | Métricas  |
| -------------------------------------------------- | -------------------------------------------------------------------------------- | --------- |
| **Especificação de requisitos** (StoryMap/PBB/backlog) | Lista-base das funções declaradas para cálculo da CRF                         | CRF       |
| **Grade curricular e pré-requisitos do SIGAA/DAC** | Referência das normas acadêmicas da UnB para validação de TDD e CF              | TDD, CF   |
| **Documentação do produto** (README, wiki do repo) | Compreensão do escopo e das funcionalidades implementadas                        | CRF       |

<p align="center">Tabela 3 - "Ferramentas de apoio à inspeção documental" Autor: Gustavo Oki</p>

#### c) Registro e análise dos resultados

| Ferramenta                              | Finalidade na avaliação                                                          | Métricas     |
| --------------------------------------- | -------------------------------------------------------------------------------- | ------------ |
| **Planilha de coleta** (Google Sheets / Excel) | Registro dos resultados de cada operação/transação e cálculo das métricas | CRF, TDD, CF |
| **GitHub Actions** (workflows de CI)    | Evidência reprodutível da execução dos testes automatizados existentes           | CRF          |
| **Jest + Playwright** (testes E2E)      | Apoio à verificação de comportamento de funções durante a coleta de CRF          | CRF          |

<p align="center">Tabela 4 - "Ferramentas de registro e análise dos resultados" Autor: Gustavo Oki</p>

### 3.4 Massa de dados

A massa de dados da Adequação Funcional é composta por:

- 15 requisitos funcionais de primeiro nível para a CRF;
- cinco operações funcionais e um perfil acadêmico de Engenharia de Software para a TDD;
- cinco históricos acadêmicos únicos de Engenharia de Software para a CF;
- estrutura curricular `6360/1 - 2017.1` e lista oficial de 39 componentes obrigatórios como referência normativa.

### 3.5 Instrumentos de coleta

Para cada métrica, registrar no repositório uma tabela com: identificador da métrica, valores brutos coletados (numerador e denominador), data da coleta, avaliador responsável e evidências (links, prints ou logs).

---

## 4. Cronograma de Avaliação

O cronograma abaixo é parte do planejamento da Fase 3 e define **quando** as atividades de coleta e análise da Adequação Funcional serão **executadas na Fase 4**. Ou seja, nesta fase apenas se planeja a agenda; a obtenção das medidas, a comparação com os critérios e o julgamento ocorrerão na Fase 4, conforme este cronograma. Toda a execução está prevista para o período de **07/06/2026 a 12/06/2026**.

| Etapa | Atividade (a executar na Fase 4)                                                                              | Métricas    | Responsável | Data de execução |
| ----- | ------------------------------------------------------------------------------------------------------------- | ----------- | ----------- | ---------------- |
| 1     | Preparação do ambiente: fixar commit de referência, levantar especificação de requisitos e normas da UnB      | —           | Caio Duarte | 07/06/2026       |
| 2     | Inspeção documental: mapear funções declaradas e verificar implementação; calcular CRF                        | CRF         | Caio Duarte | 07/06/2026       |
| 3     | Preparação dos casos de teste: definir operações-padrão com saídas esperadas para TDD e CF                   | TDD, CF     | Gabriel Flores e Caio Duarte | 08/06/2026       |
| 4     | Execução dos testes de precisão: rodar operações e registrar divergências; calcular TDD                      | TDD         | Gabriel Flores | 09/06/2026       |
| 5     | Execução dos testes de conformidade: rodar transações e verificar conformidade com normas; calcular CF        | CF          | Caio Duarte | 10/06/2026       |
| 6     | Consolidação dos dados brutos e instrumentos de coleta no repositório                                         | todas       | Caio Duarte | 12/06/2026       |
| 7     | Verificação cruzada dos resultados e preparação para a Fase 4                                                 | todas       | Caio Duarte | 12/06/2026       |

Tabela 5 - "Cronograma de execução da avaliação de Adequação Funcional (Fase 4)" Autor: Gustavo Oki

---

## 5. Consistência com a Fase 2

Cada elemento deste plano deriva diretamente da especificação da Fase 2: os métodos e as fontes de dados foram escolhidos para coletar exatamente as métricas CRF, TDD e CF e permitir a comparação com seus respectivos níveis de pontuação e critérios de julgamento. O ambiente (acesso ao sistema em execução, especificação de requisitos e normas acadêmicas da UnB) garante a disponibilidade dos dados necessários para todas as medições, assegurando rastreabilidade entre o que foi especificado e o que será executado na Fase 4.

| Métrica | Critério desejável (Fase 2) | Critério aceitável (Fase 2) | Critério inaceitável (Fase 2) |
| ------- | --------------------------- | --------------------------- | ----------------------------- |
| CRF     | ≥ 90%                       | Entre 60% e 89%             | < 60%                         |
| TDD     | ≤ 1%                        | Entre 1,1% e 5%             | > 5%                          |
| CF      | 100%                        | Entre 80% e 99%             | < 80%                         |

Tabela 6 - "Critérios definidos na fase 2" Autor: Gustavo Oki

---

## 6. Referências

> 1. SOARES RAMOS, Cristiane. Processo de Avaliação de Produto de Software. Brasília: UnB, 2025/2026. Material de aula (slides). Acesso em: 05/06/2026.
>
> 2. ISO/IEC 25010:2023. Características e subcaracterísticas de qualidade de software. Disponível em: https://www.iso.org/standard/82998.html. Acesso em: 05/06/2026.
>
> 3. ISO/IEC 25040:2011. Systems and software engineering — SQuaRE — Evaluation process. Geneva: ISO/IEC, 2011. Acesso em: 05/06/2026.
>
> 4. ISO/IEC WD 25023. Systems and software engineering — SQuaRE — Measurement of system and software product quality. Working Draft. Geneva: ISO/IEC, 2011. Acesso em: 05/06/2026.
>
> 5. UNB-MDS. 2025-1-NoFluxoUNB. Disponível em: https://github.com/unb-mds/2025-1-NoFluxoUNB. Acesso em: 05/06/2026.

---

## Histórico de Versões

| Versão | Data       | Descrição                      | Autor(es)                                                     | Revisor(es) | Data de Revisão | Alterações Realizadas |
| ------ | ---------- | ------------------------------ | ------------------------------------------------------------- | ----------- | --------------- | --------------------- |
| 1.0    | 05/06/2026 | Criação do Plano de Avaliação da Fase 3 para Adequação Funcional | [Gustavo Oki](https://github.com/GustOki) |  |  |  |
| 1.1    | 05/06/2026 | Especificação das ferramentas e definição do cronograma de execução (07/06 a 10/06/2026) | [Gustavo Oki](https://github.com/GustOki) | [Vilmar José Fagundes](https://github.com/VilmarFagundes) | 12/06/2026 | Ajuste na formatação do arquivo e adição de legendas |

<p align="center">Tabela 7 - "Histórico de versões" Autor: Vilmar José</p>
