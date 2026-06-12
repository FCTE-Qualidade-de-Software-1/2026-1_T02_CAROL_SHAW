# Adequação Funcional

Esta página registra a execução da avaliação de **Adequação Funcional** no commit `ba6db878b9dfa36fb034916612c4cf58ddf43475`, mantendo rastreabilidade com as métricas CRF, TDD e CF especificadas na Fase 2 e com os procedimentos da Fase 3.

> **Resultado:** a CRF atingiu 60,00%. TDD e CF não foram calculadas devido à ausência de dados acadêmicos com saídas esperadas e de normas institucionais de referência.

---

## 1. Obtenção das Medidas

### 1.1 CRF - Cobertura de Requisitos Funcionais

Foram identificados 15 requisitos funcionais de primeiro nível em `documentacao/planejamento/Requivitos/requisitos.md`. Cada requisito foi classificado como:

- **implementado:** todos os comportamentos descritos possuem evidência no código;
- **ausente/incorreto:** não há implementação ou existe apenas parte do comportamento exigido.

Requisitos parcialmente implementados foram contabilizados como ausentes/incorretos, conforme o método da Fase 3.

#### 1.1.1 Problema identificado na especificação

Durante a avaliação, observou-se que alguns requisitos não atendem ao princípio da **atomicidade**, pois reúnem comportamentos que podem ser implementados e verificados separadamente. Um requisito atômico deve representar uma única capacidade e permitir uma classificação objetiva entre implementado e não implementado.

O RF05, por exemplo, reúne quatro capacidades:

1. mostrar o fluxograma do curso;
2. destacar as disciplinas cursadas;
3. apresentar as equivalências;
4. informar o número de tentativas ou reprovações.

As três primeiras capacidades estão implementadas, enquanto a quarta não está. Como todas pertencem ao mesmo requisito, o RF05 recebeu a classificação **ausente/incorreto**, apesar de sua implementação parcial. Situação semelhante ocorre em requisitos que combinam cálculo e exibição, dados atuais e históricos ou múltiplos resultados acadêmicos.

Essa estrutura prejudica a imparcialidade da CRF: a classificação binária desconsidera partes implementadas, enquanto uma classificação positiva desconsideraria partes ausentes. O resultado de 60,00% foi mantido para preservar o método definido nas Fases 2 e 3, que utiliza os 15 requisitos de primeiro nível como unidade de contagem. Portanto, o valor representa a cobertura integral dos requisitos compostos, e não o percentual de capacidades funcionais individuais implementadas.

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

<p align="center">Tabela 1 - Memória de cálculo da CRF. Fonte: Equipe Carol Shaw, 2026.</p>

Os seis itens ausentes ou incompletos são:

1. exibição do número de tentativas ou reprovações por disciplina;
2. exportação da simulação em PDF, pois a funcionalidade disponível gera PNG;
3. exibição de semestres restantes com base no tempo máximo do curso;
4. exibição dos trancamentos detectados;
5. identificação de mudança de curso já ocorrida, com curso anterior, data e aproveitamentos;
6. recomendação por IA cobrindo conjuntamente cursos, disciplinas, histórico e preferências pessoais.

A matriz completa de inspeção está disponível em [Evidência da CRF](evidencias/crf.md).

### 1.2 TDD - Taxa de Divergência de Dados

$$
TDD = \frac{\text{operações com divergência}}{\text{total de operações realizadas}} \times 100
$$

- Operações-padrão com saída esperada: **não disponíveis**;
- Históricos acadêmicos de teste: **não disponíveis**;
- Referência oficial para conferência das saídas: **não disponível**;
- Resultado: **não calculado**.

Os testes automatizados do projeto verificam unidades específicas, mas não constituem a amostra mínima de 30 operações com resultados acadêmicos previamente conhecidos exigida pelo plano.

### 1.3 CF - Conformidade Funcional

$$
CF = \frac{\text{transações em conformidade}}{\text{total de transações processadas}} \times 100
$$

- Regras e normas acadêmicas versionadas: **não disponíveis**;
- Transações-padrão vinculadas às normas: **não disponíveis**;
- Resultado: **não calculado**.

O código contém regras relacionadas a pré-requisitos, equivalências e mudança de curso, mas a implementação não pode ser declarada conforme sem uma referência institucional documentada. A própria interface de mudança de curso informa que o resultado é apenas indicativo e que a decisão oficial depende do PPC, do SIGAA e do edital vigente.

---

## 2. Comparação com os Critérios

| Métrica | Desejável | Aceitável | Inaceitável | Resultado | Classificação |
| :------ | :-------- | :-------- | :----------- | :-------- | :------------ |
| CRF | >= 90% | 60% a 89% | < 60% | 60,00% | Aceitável |
| TDD | <= 1% | 1,1% a 5% | > 5% | Não calculado | Inconclusiva |
| CF | 100% | 80% a 99% | < 80% | Não calculado | Inconclusiva |

<p align="center">Tabela 2 - Comparação das métricas de Adequação Funcional com os critérios da Fase 2. Fonte: Equipe Carol Shaw, 2026.</p>

A CRF está exatamente no limite inferior da faixa aceitável e 30 pontos percentuais abaixo do nível desejável. A classificação representa a cobertura integral dos 15 requisitos de primeiro nível e é influenciada pela presença de requisitos não atômicos.

---

## 3. Respostas às Questões GQM

### Q1. Quão completa está a implementação de acordo com as especificações de requisitos?

**Resposta:** 60,00% dos requisitos funcionais estão integralmente representados no código avaliado. O resultado é aceitável, mas não confirma H1 no nível desejável.

### Q2. Com que frequência ocorrem resultados imprecisos durante a construção do fluxograma?

**Resposta:** inconclusiva. Sem operações controladas e saídas esperadas, a TDD não pode ser calculada e H2 não pode ser confirmada ou refutada.

### Q3. Qual é o percentual de transações processadas de acordo com as regras e normas acadêmicas da UnB?

**Resposta:** inconclusiva. Sem normas versionadas e transações vinculadas a elas, a CF não pode ser calculada e H3 não pode ser confirmada ou refutada.

---

## 4. Julgamento e Ações de Melhoria

O NoFluxoUNB implementa autenticação, upload e leitura de histórico, consulta curricular, cálculo de progresso e indicadores, carga horária complementar, simulação de mudança de curso e persistência do histórico de envios. Entretanto, a cobertura funcional permanece no menor valor aceitável.

As ações prioritárias derivadas da CRF são:

1. decompor os requisitos compostos em requisitos atômicos com critérios de aceitação independentes;
2. implementar exportação real da simulação em PDF;
3. exibir tentativas e reprovações por disciplina;
4. calcular e exibir os semestres restantes a partir do prazo máximo do curso;
5. apresentar na interface os períodos de trancamento já extraídos;
6. modelar a mudança de curso ocorrida no passado e seus aproveitamentos;
7. integrar ao assistente o histórico acadêmico e tornar explícita a recomendação de cursos e disciplinas por preferências.

Para concluir TDD e CF, deve-se preparar uma massa de dados anonimizada, definir saídas esperadas com fonte oficial e versionar as normas acadêmicas utilizadas em cada transação.

---

## 5. Rastreabilidade

- [Propósito e Escopo - Fase 1](../fase1/proposito_escopo.md)
- [Especificação da Adequação Funcional - Fase 2](../fase2/adequacao_funcional.md)
- [Plano da Adequação Funcional - Fase 3](../fase3/adequacao_funcional.md)
- [Evidência da CRF](evidencias/crf.md)
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
| 1.0 | 11/06/2026 | Registro inicial da execução da avaliação de Adequação Funcional | Equipe Carol Shaw |  |  |  |
| 1.1 | 11/06/2026 | Cálculo da CRF, julgamento e registro das métricas inviáveis | Equipe Carol Shaw |  |  |  |
| 1.2 | 11/06/2026 | Revisão da redação acadêmica da página | Equipe Carol Shaw |  |  |  |
| 1.3 | 11/06/2026 | Registro do problema de atomicidade dos requisitos funcionais | Equipe Carol Shaw |  |  |  |
