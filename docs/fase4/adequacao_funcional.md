# Adequação Funcional

Esta página apresenta a execução da avaliação de **Adequação Funcional** sobre o commit [`ba6db878b9dfa36fb034916612c4cf58ddf43475`](https://github.com/unb-mds/2025-1-NoFluxoUNB/commit/ba6db878b9dfa36fb034916612c4cf58ddf43475) do [NoFluxoUNB](https://github.com/unb-mds/2025-1-NoFluxoUNB). A análise preserva a rastreabilidade com as métricas CRF, TDD e CF especificadas na Fase 2 e com os procedimentos definidos na Fase 3.

---

## 1. Obtenção das Medidas

### 1.1 CRF - Cobertura de Requisitos Funcionais

Foram identificados 15 requisitos funcionais de primeiro nível no documento [`documentacao/planejamento/Requivitos/requisitos.md`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/documentacao/planejamento/Requivitos/requisitos.md). Cada requisito foi classificado segundo uma das seguintes situações:

- **implementado:** todos os comportamentos descritos possuem evidência no código;
- **ausente/incorreto:** não há implementação ou existe apenas parte do comportamento exigido.

Conforme o método estabelecido na Fase 3, requisitos parcialmente implementados foram contabilizados como ausentes ou incorretos.

#### 1.1.1 Problema identificado na especificação

Alguns requisitos não atendem ao princípio da **atomicidade**, pois agregam comportamentos que podem ser implementados e verificados de forma independente. Um requisito atômico deve representar uma única capacidade funcional e possibilitar uma classificação objetiva entre atendimento e não atendimento.

O RF05, por exemplo, reúne quatro capacidades:

1. mostrar o fluxograma do curso;
2. destacar as disciplinas cursadas;
3. apresentar as equivalências;
4. informar o número de tentativas ou reprovações.

As três primeiras capacidades possuem evidências de implementação, enquanto a quarta permanece ausente. Como todas integram o mesmo requisito, o RF05 foi classificado como **ausente/incorreto**, apesar do atendimento parcial. A mesma limitação ocorre em requisitos que combinam cálculo e apresentação, dados atuais e históricos ou diferentes resultados acadêmicos.

Essa estrutura reduz a precisão da CRF. A classificação binária desconsidera as capacidades implementadas quando o requisito é avaliado negativamente; em sentido oposto, uma classificação positiva ocultaria capacidades ainda ausentes. O resultado de 60,00% foi mantido para preservar o método definido nas Fases 2 e 3, cuja unidade de contagem corresponde aos 15 requisitos de primeiro nível. Assim, o valor expressa a cobertura integral dos requisitos compostos, e não o percentual de capacidades funcionais individuais implementadas.

Para avaliações futuras, os requisitos compostos devem ser decompostos em requisitos atômicos, identificados individualmente e acompanhados de critérios de aceitação próprios.

$$
CRF = \frac{\text{funções declaradas} - \text{funções ausentes ou incorretas}}{\text{funções declaradas}} \times 100
$$

$$
CRF = \frac{15 - 6}{15} \times 100 = 60{,}00\%
$$

| Dado bruto | Valor |
| :--------- | ----: |
| Funções declaradas | 15 |
| Funções implementadas | 9 |
| Funções ausentes ou incorretas | 6 |
| CRF | 60,00% |

<p align="center">Tabela 1 - Memória de cálculo da CRF. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

Os seis itens ausentes ou incompletos são:

1. exibição do número de tentativas ou reprovações por disciplina;
2. exportação da simulação em PDF, pois a funcionalidade disponível gera PNG;
3. exibição de semestres restantes com base no tempo máximo do curso;
4. exibição dos trancamentos detectados;
5. identificação de mudança de curso já ocorrida, com curso anterior, data e aproveitamentos;
6. recomendação baseada em inteligência artificial que considere, de forma conjunta, cursos, disciplinas, histórico acadêmico e preferências pessoais.

A matriz completa de inspeção está disponível em [Evidência da CRF](evidencias/adequacao_funcional/crf.md).

### 1.2 TDD - Taxa de Divergência de Dados

#### 1.2.1 Definição das operações-padrão

Para obter a Taxa de Divergência de Dados (TDD), foram executadas cinco operações: login, importação de histórico, verificação do fluxograma, consulta de pré-requisitos e geração de recomendação. A recomendação foi avaliada com um perfil acadêmico:

- **Contexto acadêmico:** estudante de Engenharia de Software com bom desempenho em disciplinas de programação, algoritmos, estrutura de dados e matemática aplicada.
- **Objetivo principal:** escolher disciplinas que maximizem aprofundamento técnico, formação em desenvolvimento de software e preparo para áreas como engenharia de dados, backend, inteligência artificial ou infraestrutura.
- **Preferências de recomendação:** prioriza disciplinas com alta carga prática, forte relação com pré-requisitos técnicos e maior alinhamento com conteúdos de implementação, raciocínio lógico e resolução de problemas.

#### 1.2.2 Saída esperada das operações

1. Login: autenticação realizada com sucesso e redirecionamento automático para a página de escolha de curso.
2. Importar histórico: importação realizada com sucesso.
3. Geração do fluxograma: geração de um fluxograma que represente corretamente o curso e as disciplinas cursadas pelo discente até aquele momento.
4. Consulta de pré-requisitos: Algoritmos e Programação de Computadores (APC) não deve ter pré-requisitos; Estruturas de Dados e Algoritmos 1 (EDA1) deve ter APC como pré-requisito; e Estruturas de Dados e Algoritmos 2 (EDA2) deve ter EDA1 como pré-requisito.
5. Geração de recomendação: o sistema deve recomendar disciplinas disponíveis para matrícula e alinhadas ao perfil acadêmico informado.

#### 1.2.3 Execução das operações

[Vídeo de execução das operações](https://www.youtube.com/embed/pcNCkT13_kI)

#### 1.2.4 Análise e comparação das saídas

| Operação | Resultado | Situação |
| :------- | :-------- | :------- |
| Login | Autenticação e redirecionamento realizados | Conforme |
| Importação de histórico | Histórico processado com sucesso | Conforme |
| Geração do fluxograma | Fluxograma gerado, mas com disciplinas sem oferta atual, como Qualidade de Software 2 e Compiladores 2 | Divergente |
| Consulta de pré-requisitos | Relações de APC, EDA1 e EDA2 apresentadas conforme o esperado | Conforme |
| Geração de recomendação | Recomendações incluem disciplinas sem oferta atual e dependem de solicitação explícita para considerar o perfil | Divergente |

<p align="center">Tabela 2 - Resultado das operações utilizadas na TDD. Fonte: Gabriel Flores, 2026.</p>

#### 1.2.5 Medidas obtidas

- **Total de operações realizadas:** 5;
- **Operações com divergência:** 2.

#### 1.2.6 Cálculo da métrica TDD


$$
TDD = \frac{\text{operações com divergência}}{\text{total de operações realizadas}} \times 100
$$

$$
TDD = \frac{\text{2}}{\text{5}} \times 100 = 40\%
$$

#### 1.2.7 Análise e Conclusão 

O cálculo de 40% enquadra-se no critério **Inaceitável: > 5%**, refutando a hipótese H2 na amostra executada. O resultado se restringe às cinco operações e ao único perfil acadêmico avaliados.

As divergências indicam defasagem na fonte de dados de disciplinas. O sistema considera optativas que foram alteradas ou não estão mais sendo ofertadas, o que pode comprometer o planejamento de grades.

### 1.3 CF - Conformidade Funcional

$$
CF = \frac{\text{transações em conformidade}}{\text{total de transações processadas}} \times 100
$$

A referência normativa adotada foi a estrutura curricular do curso de Engenharia de Software da FCTE, código `6360/1`, vigente desde `2017.1`, registrada no arquivo `spec/SIGAA - Sistema Integrado de Gestão de Atividades Acadêmicas.html`. Essa estrutura estabelece:

- carga horária total mínima de 3.480 horas;
- carga horária obrigatória de 2.580 horas;
- carga horária optativa mínima de 900 horas;
- 39 componentes obrigatórios;
- relação dos componentes obrigatórios e optativos por nível.

Embora o [diretório de históricos](https://github.com/unb-mds/2025-1-NoFluxoUNB/tree/ba6db878b9dfa36fb034916612c4cf58ddf43475/test_historicos/historicos) contenha documentos de outros cursos e matrículas, a CF abrange somente Engenharia de Software, pois a referência normativa disponível corresponde especificamente à estrutura curricular `6360/1 - 2017.1`. Dos seis documentos desse curso, dois pertencem à matrícula `211029503`; para evitar duplicidade, foi mantido apenas o documento mais recente, emitido em 29/06/2024. A amostra final contém, portanto, cinco matrículas únicas.

Para cada histórico, o PDF foi processado na página de importação do NoFluxoUNB e foram verificadas seis transações atômicas:

1. identificação da matriz `6360/1 - 2017.1`;
2. apresentação das cargas horárias oficiais;
3. composição do conjunto de 39 componentes obrigatórios;
4. classificação dos componentes obrigatórios como concluídos ou pendentes;
5. reconhecimento das equivalências registradas no histórico;
6. apresentação do período letivo atual informado no histórico.

Para assegurar a rastreabilidade da coleta, os históricos foram identificados pelos casos H01 a H05:

| Caso | Histórico |
| :--- | :-------- |
| H01 | `historico_190012579` |
| H02 | `historico_211029503` |
| H03 | `historico_222006202` |
| H04 | `historico_222037700` |
| H05 | `historico_231026330` |

<p align="center">Tabela 3 - Identificação dos históricos da CF. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

| Verificação | Transações | Em conformidade | Não conformes |
| :----------- | ---------: | --------------: | ------------: |
| Identificação da matriz | 5 | 5 | 0 |
| Cargas horárias da matriz | 5 | 5 | 0 |
| Componentes obrigatórios | 5 | 3 | 2 |
| Situação dos componentes | 5 | 4 | 1 |
| Equivalências | 5 | 4 | 1 |
| Período letivo atual | 5 | 0 | 5 |
| **Total** | **30** | **21** | **9** |

<p align="center">Tabela 4 - Consolidação das transações da CF. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

Todos os cinco históricos apresentaram divergência no campo exibido como **Semestre Atual**. O documento acadêmico informa o período letivo atual como posição ordinal do estudante no curso, enquanto o NoFluxoUNB apresenta o ano e o período da disciplina com situação `MATR`. Desse modo, o rótulo da interface não corresponde ao significado do dado exibido.

Os valores encontrados em cada histórico e os valores exibidos pelo sistema estão registrados na [evidência da verificação do Período Letivo Atual](evidencias/adequacao_funcional/cf.md#evidencia-periodo-letivo-atual).

Também foram identificadas divergências curriculares em dois históricos:

- `H03` — `historico_222006202`: o sistema incluiu `FGA0146` como obrigatória, não reconheceu `MAT0025` como cumprida por equivalência e não classificou `MAT0031` com situação `CUMP` como concluída;
- `H05` — `historico_231026330`: o sistema incluiu `FGA0146` como obrigatória, elevando o resumo para 40 componentes, embora a estrutura oficial contenha 39.

$$
CF = \frac{21}{30} \times 100 = 70{,}00\%
$$

| Dado bruto | Valor |
| :--------- | ----: |
| Transações processadas | 30 |
| Transações em conformidade | 21 |
| Transações não conformes | 9 |
| CF | 70,00% |

<p align="center">Tabela 5 - Memória de cálculo da CF. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

A coleta detalhada, os resultados por histórico e a relação das regras utilizadas estão disponíveis em [Evidência da CF](evidencias/adequacao_funcional/cf.md).

---

## 2. Comparação com os Critérios

| Métrica | Desejável | Aceitável | Inaceitável | Resultado | Classificação |
| :------ | :-------- | :-------- | :----------- | :-------- | :------------ |
| CRF | >= 90% | 60% a 89% | < 60% | 60,00% | Aceitável |
| TDD | <= 1% | 1,1% a 5% | > 5% | 40% | Inaceitável |
| CF | 100% | 80% a 99% | < 80% | 70,00% | Inaceitável |

<p align="center">Tabela 6 - Comparação das métricas de Adequação Funcional com os critérios da Fase 2. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

A CRF situa-se no limite inferior da faixa aceitável. A TDD supera em 35 pontos percentuais o limite máximo da faixa aceitável, enquanto a CF ficou 10 pontos percentuais abaixo do limite de aceitabilidade. A interpretação deve considerar a atomicidade limitada dos requisitos da CRF, a amostra de cinco operações da TDD e o escopo da CF restrito à estrutura curricular `6360/1 - 2017.1`.

---

## 3. Respostas às Questões GQM

### Q1. Quão completa está a implementação de acordo com as especificações de requisitos?

**Resposta:** 60,00% dos requisitos funcionais estão integralmente representados no código avaliado. Embora aceitável segundo o critério definido, o resultado não confirma a hipótese H1 no nível desejável.

### Q2. Com que frequência ocorrem resultados imprecisos durante a construção do fluxograma?

**Resposta:** duas das cinco operações apresentaram divergência, resultando em TDD de 40,00%. O resultado é inaceitável para a amostra executada.

### Q3. Qual é o percentual de transações processadas de acordo com as regras e normas acadêmicas da UnB?

**Resposta:** 70,00% das transações processadas para o currículo de Engenharia de Software `6360/1 - 2017.1` apresentaram conformidade com a estrutura publicada no SIGAA e com os dados dos históricos. O resultado é inaceitável e não confirma a hipótese H3.

---

## 4. Julgamento e Ações de Melhoria

O [NoFluxoUNB](https://github.com/unb-mds/2025-1-NoFluxoUNB) implementa autenticação, envio e leitura de histórico, consulta curricular, cálculo de progresso e indicadores, tratamento de carga horária complementar, simulação de mudança de curso e persistência dos envios realizados. Apesar dessas capacidades, a CRF permaneceu no limite inferior da faixa aceitável, a TDD foi inaceitável em duas das cinco operações e a CF apresentou nove divergências em 30 transações.

As ações prioritárias derivadas da avaliação funcional são:

1. decompor os requisitos compostos em requisitos atômicos com critérios de aceitação independentes;
2. implementar exportação real da simulação em PDF;
3. exibir tentativas e reprovações por disciplina;
4. calcular e exibir os semestres restantes a partir do prazo máximo do curso;
5. apresentar na interface os períodos de trancamento já extraídos;
6. modelar a mudança de curso ocorrida no passado e seus aproveitamentos;
7. integrar ao assistente o histórico acadêmico e tornar explícita a recomendação de cursos e disciplinas por preferências;
8. corrigir a natureza de `FGA0146` na matriz `6360/1 - 2017.1`;
9. revisar o casamento de componentes cumpridos e equivalentes, especialmente os casos `MAT0031` com situação `CUMP` e `MAT0025` cumprida por `MAT0137`;
10. exibir como semestre atual o valor do campo `Período Letivo Atual` do histórico ou alterar o rótulo para indicar que o valor representa o ano e período da matrícula mais recente.

Para diminuir a **Taxa de Divergência de Dados**, é necessário atualizar as fontes de oferta de disciplinas, restringir as recomendações às matérias disponíveis e estabilizar a integração com o assistente Darcy AI.

---

## 5. Rastreabilidade

- [Propósito e Escopo - Fase 1](../fase1/proposito_escopo.md)
- [Especificação da Adequação Funcional - Fase 2](../fase2/adequacao_funcional.md)
- [Plano da Adequação Funcional - Fase 3](../fase3/adequacao_funcional.md)
- [Evidência da CRF](evidencias/adequacao_funcional/crf.md)
- [Evidência da CF](evidencias/adequacao_funcional/cf.md)
- [Especificações das Funcionalidades](evidencias/adequacao_funcional/especificacao_funcionalidades.md)
- [Visão Geral da Fase 4](introducao.md)

---

## 6. Referências

> 1. SOARES RAMOS, Cristiane. Processo de Avaliação de Produto de Software. Brasília: UnB, 2025. Material de aula (slides). Acesso em: 11/06/2026.
>
> 2. SOARES RAMOS, Cristiane. Projeto Final da Disciplina: Avaliação da Qualidade de Produto de Software. Brasília: UnB, 2026. Enunciado do trabalho final. Acesso em: 11/06/2026.
>
> 3. UNB-MDS. [2025-1-NoFluxoUNB](https://github.com/unb-mds/2025-1-NoFluxoUNB). Acesso em: 11/06/2026.
>
> 4. UNIVERSIDADE DE BRASÍLIA. SIGAA: estrutura curricular de Engenharia de Software/FCTE, código 6360/1, vigência 2017.1. Acesso em: 12/06/2026.

---

## Histórico de Versões

| Versão | Data | Descrição | Autor(es) |
| :----- | :--- | :-------- | :-------- |
| 1.0 | 11/06/2026 | Registro inicial da execução da avaliação de Adequação Funcional | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.1 | 11/06/2026 | Cálculo da CRF, julgamento e registro das métricas inviáveis | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.2 | 11/06/2026 | Registro do problema de atomicidade dos requisitos funcionais | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.3 | 12/06/2026 | Execução da CF para o currículo 6360/1 - 2017.1 | [Caio Duarte](https://github.com/caioduart3) |
| 1.4 | 12/06/2026 | Deduplicação da amostra e inclusão da conformidade do período letivo atual | [Caio Duarte](https://github.com/caioduart3)  |
| 1.5 | 12/06/2026 | Cálculo da TDD, registro das métricas e análise | [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.6 | 13/06/2026 | Registro da limitação amostral da TDD após auditoria dos cálculos | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.7 | 13/06/2026 | Sincronização dos resultados e limitações com as evidências da Fase 4 | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
