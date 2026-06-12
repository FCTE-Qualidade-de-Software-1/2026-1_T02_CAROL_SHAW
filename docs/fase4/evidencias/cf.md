# Evidência da CF

Esta página registra os dados brutos e o procedimento utilizado no cálculo da **Conformidade Funcional (CF)** para a estrutura curricular de Engenharia de Software da FCTE.

## 1. Fontes

| Fonte | Utilização |
| :---- | :--------- |
| `spec/SIGAA - Sistema Integrado de Gestão de Atividades Acadêmicas.html` | Estrutura curricular oficial e cargas horárias |
| `2025-1-NoFluxoUNB/test_historicos/historicos/` | Históricos acadêmicos processados |
| `2025-1-NoFluxoUNB/test_historicos/pdfDataExtractor.mjs` | Apoio à extração das situações e equivalências presentes nos documentos |
| `https://no-fluxo.crianex.com/upload-historico` | Ambiente de execução das transações |
| Commit `ba6db878b9dfa36fb034916612c4cf58ddf43475` | Código-fonte inspecionado |

<p align="center">Tabela 1 - Fontes utilizadas na CF. Fonte: Equipe Carol Shaw, 2026.</p>

A execução ocorreu em 12/06/2026. Nenhuma ação de salvamento do fluxograma foi executada após o processamento.

Apesar de a pasta do NoFluxoUNB disponibilizar históricos de outras matrículas e cursos, esta avaliação considera somente os documentos de Engenharia de Software vinculados à estrutura `6360/1 - 2017.1`. Aplicar a mesma referência curricular a outros cursos produziria uma comparação inválida.

Foram encontrados seis documentos de Engenharia de Software, mas dois pertencem à matrícula `211029503`. O arquivo emitido em 14/08/2023 foi excluído e foi mantido o documento mais recente, emitido em 29/06/2024. A amostra final contém cinco matrículas:

| Caso | Histórico | Documento processado |
| :--- | :-------- | :------------------- |
| H01 | `historico_190012579` | `historico_190012579 (5) (1).pdf` |
| H02 | `historico_211029503` | `historico_211029503 (1).pdf` |
| H03 | `historico_222006202` | `historico_222006202 (1).pdf` |
| H04 | `historico_222037700` | `historico_222037700-1.pdf` |
| H05 | `historico_231026330` | `historico_231026330.pdf` |

<p align="center">Tabela 2 - Correspondência entre casos e históricos. Fonte: Equipe Carol Shaw, 2026.</p>

Após a remoção do documento duplicado, não existe um caso `H06` na amostra revisada.

## 2. Regras de Referência

O arquivo do SIGAA identifica a estrutura `6360/1`, vigente desde `2017.1`, com os seguintes valores:

| Regra | Valor oficial |
| :---- | ------------: |
| Carga horária total mínima | 3.480h |
| Carga horária obrigatória | 2.580h |
| Carga horária optativa mínima | 900h |
| Componentes obrigatórios | 39 |
| Prazo mínimo | 9 semestres |
| Prazo médio | 10 semestres |
| Prazo máximo | 16 semestres |
| Carga horária mínima por semestre | 240h |
| Carga horária máxima por semestre | 480h |

<p align="center">Tabela 3 - Regras da estrutura curricular 6360/1. Fonte: SIGAA/UnB.</p>

Os 39 componentes obrigatórios utilizados na comparação são:

| Nível | Componentes obrigatórios |
| :---- | :----------------------- |
| 1º | `FGA0161`, `FGA0163`, `FGA0168`, `MAT0025` |
| 2º | `FGA0157`, `IFD0171`, `IFD0173`, `MAT0026`, `MAT0031` |
| 3º | `FGA0133`, `FGA0158`, `FGA0160`, `FGA0164` |
| 4º | `FGA0108`, `FGA0138`, `FGA0142`, `FGA0147`, `FGA0150`, `FGA0184` |
| 5º | `FGA0003`, `FGA0030`, `FGA0137`, `FGA0170`, `FGA0172`, `FGA0173` |
| 6º | `FGA0060`, `FGA0208`, `FGA0211`, `FGA0238`, `FGA0278` |
| 7º | `FGA0109`, `FGA0210`, `FGA0244` |
| 8º | `FGA0021`, `FGA0206`, `FGA0240` |
| 9º | `FGA0009`, `FGA0250` |
| 10º | `FGA0011` |

<p align="center">Tabela 4 - Componentes obrigatórios por nível. Fonte: SIGAA/UnB.</p>

Os limites semestrais e os prazos de conclusão não entraram no cálculo porque a operação de importação não realiza matrícula nem valida o tempo de permanência do estudante.

## 3. Procedimento

Para cada histórico:

1. o PDF foi enviado pela página de importação;
2. a matriz identificada pelo sistema foi comparada com `6360/1 - 2017.1`;
3. as cargas horárias exibidas foram comparadas com a Tabela 3;
4. o conjunto retornado como obrigatório foi comparado com os 39 componentes obrigatórios do SIGAA;
5. as situações `APR`, `CUMP` e `DISP` foram consideradas concluídas;
6. as demais situações foram consideradas pendentes;
7. as equivalências registradas no histórico foram comparadas com as equivalências reconhecidas pelo sistema;
8. o campo `Período Letivo Atual` do histórico foi comparado com o valor apresentado como `Semestre Atual` na interface.

Cada item de comparação foi contabilizado como uma transação independente. Uma divergência em qualquer dado da transação resultou na classificação **não conforme**.

## 4. Dados Brutos

| Caso | Matriz | Cargas horárias | 39 obrigatórias | Concluídas/pendentes | Equivalências | Semestre atual | Conformes |
| :--- | :----: | :-------------: | :--------------: | :------------------: | :-----------: | :-------------: | ---------: |
| H01 | Conforme | Conforme | Conforme | 18/21 conforme | 0/0 conforme | Não conforme | 5 |
| H02 | Conforme | Conforme | Conforme | 16/23 conforme | 0/0 conforme | Não conforme | 5 |
| H03 | Conforme | Conforme | Não conforme | Esperado 10/29; obtido 8/32 | Esperado 1; obtido 0 | Não conforme | 2 |
| H04 | Conforme | Conforme | Conforme | 14/25 conforme | 2/2 conforme | Não conforme | 5 |
| H05 | Conforme | Conforme | Não conforme | 22/17 oficiais conformes | 5/5 conforme | Não conforme | 4 |
| **Total** | **5/5** | **5/5** | **3/5** | **4/5** | **4/5** | **0/5** | **21/30** |

<p align="center">Tabela 5 - Resultado das transações por histórico. Fonte: Equipe Carol Shaw, 2026.</p>

O caso `H02` não apresenta a vigência da matriz em campo próprio no texto extraído. Ainda assim, o sistema associou o histórico à estrutura completa `6360/1 - 2017.1`, e o conjunto de componentes retornado foi comparado integralmente com a referência do SIGAA.

## 5. Não Conformidades

<a id="evidencia-periodo-letivo-atual"></a>

### 5.1 Semestre atual

O NoFluxoUNB não apresentou o valor do campo `Período Letivo Atual` de nenhum dos cinco históricos:

| Caso | Histórico | Valor no histórico | Valor exibido pelo NoFluxoUNB |
| :--- | :-------- | :----------------- | :---------------------------- |
| H01 | `historico_190012579` | 10 | `2024.2` |
| H02 | `historico_211029503` | 7 | `2024.1` |
| H03 | `historico_222006202` | 6 | `2025.1` |
| H04 | `historico_222037700` | 6 | `2025.1` |
| H05 | `historico_231026330` | 6 | `2025.4` |

<p align="center">Tabela 6 - Divergências no semestre atual. Fonte: Equipe Carol Shaw, 2026.</p>

A interface utiliza o rótulo **Semestre Atual**, mas apresenta o ano e período da disciplina mais recente com situação `MATR`. O histórico utiliza **Período Letivo Atual** para indicar a posição ordinal do estudante no curso. Como os conceitos não são equivalentes, as cinco transações foram classificadas como não conformes.

### 5.2 Caso H03 — `historico_222006202`

O sistema retornou 40 componentes obrigatórios, com 8 concluídos e 32 pendentes. Foram observadas três divergências:

- `FGA0146 - Estruturas de Dados 1` foi incluída como obrigatória, embora não faça parte dos 39 componentes obrigatórios da estrutura;
- `MAT0025 - Cálculo 1`, cumprida por equivalência com `MAT0137`, permaneceu pendente;
- `MAT0031 - Introdução a Álgebra Linear`, registrada com situação `CUMP`, permaneceu pendente.

### 5.3 Caso H05 — `historico_231026330`

As situações dos 39 componentes oficiais e as cinco equivalências foram processadas corretamente. Entretanto, `FGA0146 - Estruturas de Dados 1` também foi incluída como obrigatória, elevando o resumo para 40 componentes, com 23 concluídos e 17 pendentes.

## 6. Cálculo

$$
CF = \frac{\text{transações em conformidade}}{\text{total de transações processadas}} \times 100
$$

$$
CF = \frac{21}{30} \times 100 = 70{,}00\%
$$

O resultado da CF foi **70,00%**, classificado como **inaceitável**, pois ficou abaixo de 80%.

## Histórico de Versões

| Versão | Data | Descrição | Autor(es) | Revisor(es) | Data de Revisão | Alterações Realizadas |
| :----- | :--- | :-------- | :-------- | :----------- | :--------------- | :-------------------- |
| 1.0 | 12/06/2026 | Registro da execução e dos dados brutos da CF | Equipe Carol Shaw |  |  |  |
| 1.1 | 12/06/2026 | Deduplicação da amostra e inclusão da verificação do semestre atual | Equipe Carol Shaw |  |  |  |
