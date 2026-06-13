# Adequação Funcional

## Objetivo 

| Dimensão | Descrição |
|----------|-----------|
| Analisar | O NoFluxoUNB |
| Para o propósito de | Avaliar | 
| Com respeito a | Adequação Funcional | 
| Do ponto de visto do/a | Equipe de desenvolvimento |
| No contexto de | Disciplina de Qualidade de Software |

## Questões, Hipóteses e  Métricas

### Q1: Quão completa está a implementação de acordo com as especificações de requisitos?

#### H1: Espera-se que o NoFluxo tenha implementado maior parte dos requisitos elicitados 

#### Métrica 1: CRF (Cobertura de Requisitos Funcionais)
Fórmula:
$$
\frac{\text{n° funções declaradas} - \text{n° funções ausentes ou incorretas}}{\text{n° funções declaradas}} \times 100
$$

Critérios: 

- Desejável (H1 Confirmada): ≥ 90%

- Aceitável: Entre 60% e 89%

- Inaceitável (H1 Refutada): < 60%

### Q2: Com que frequência ocorrem divergências nas operações funcionais avaliadas?

#### H2: A frequência de operações com divergência de dados é inferior ou igual a 1% do total de operações avaliadas.

#### Métrica 2: TDD (Taxa de Divergência de Dados)
Fórmula:
$$
\frac{\text{n° operações reportadas com divergência de dados}}{\text{n° total de operações realizadas no período}} \times 100
$$

Critérios: 

- Desejável (H2 Confirmada): ≤ 1%

- Aceitável: Entre 1,1% e 5%

- Inaceitável (H2 Refutada): > 5%

### Q3: Qual é o percentual de transações processadas que estão de acordo com as regras e normas acadêmicas da UnB?

#### H3: O sistema garante 100% de conformidade no processamento de transações relacionadas as diretrizes UnB.

#### Métrica 3: CF (Conformidade Funcional)
Fórmula:
$$
\frac{\text{n° transações de acordo com as normas}}{\text{n° total de transações processadas}} \times 100
$$

Critérios: 

- Desejável (H3 Confirmada): 100%

- Aceitável: Entre 80% e 99%

- Inaceitável (H3 Refutada): < 80%

## Modelo GQM

<figure markdown>

![Diagrama GQM - Adequação Funcional](../assets/img/GQM-AdequacaoFuncional.svg)

<figcaption>

<b>Figura 1 – GQM de Adequação Funcional</b>
</br>
Fonte: Caio Duarte, 2026.

</figcaption>
</figure>


## Referências

> 1. ISO/IEC JTC 1/SC 7/WG 6, Systems and software engineering - Systems and software Quality Requirements and Evaluation (SQuaRE) - Measurement of system and software product quality, ISO/IEC WD 25023, Version 0.1.0 Working Draft, Aug. 31, 2011. Acesso em: 04/06/2026

> 2. SOARES RAMOS, Cristiane. Processo de Avaliação de Qualidade de Software. Brasília: UnB, 2026. Material de aula (slides). Acesso em: 04/06/2026

> 3. UNB-MDS. 2025-1-NoFluxoUNB. [S. l.], 2025. Disponível em: https://github.com/unb-mds/2025-1-NoFluxoUNB. Acesso em: 04/06/2026

## Histórico de Versões

| Versão | Data       | Descrição                      | Autor(es)                                                     | Revisor(es) | Data de Revisão | Alterações Realizadas |
| ------ | ---------- | ------------------------------ | ------------------------------------------------------------- | ----------- | --------------- | --------------------- |
| 1.0    | 04/06/2026 | Criação da documentação inicial e estruturação | [Vilmar José Fagundes](https://github.com/VilmarFagundes) |  |  |  |
| 1.0    | 04/06/2026 | Adiciona GQM de adequação funcional | [Caio Duarte](https://github.com/caioduart3) |  |  |  |
| 1.1    | 13/06/2026 | Correção da fórmula da CRF e da identificação da hipótese da CF | [Caio Duarte](https://github.com/caioduart3) |  |  |  |
| 1.2    | 13/06/2026 | Alinhamento da questão e da hipótese da TDD às operações executadas | [Caio Duarte](https://github.com/caioduart3) |  |  |  |
