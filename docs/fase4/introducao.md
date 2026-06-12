# Sobre a Fase 4

## 1. Introdução

A Fase 4, **Executar a Avaliação**, aplica os requisitos da Fase 1, as métricas e os critérios da Fase 2 e os métodos planejados na Fase 3. Conforme o Processo de Avaliação de Produto de Software, esta etapa compreende:

1. obter as medidas;
2. comparar as medidas com os critérios estabelecidos;
3. julgar os resultados e propor ações de melhoria.

---

## 2. Versão e Escopo Avaliados

A avaliação considerou o NoFluxoUNB no seguinte commit:

| Item | Valor |
| :--- | :---- |
| Repositório | `https://github.com/unb-mds/2025-1-NoFluxoUNB` |
| Commit avaliado | `ba6db878b9dfa36fb034916612c4cf58ddf43475` |
| Identificação pelo Git | `V2.3.0-354-gba6db878` |
| Data da coleta | 11/06/2026 |

<p align="center">Tabela 1 - Identificação do produto avaliado. Fonte: Equipe Carol Shaw, 2026.</p>

A Fase 1 referencia a versão `V2.3.0`, cuja tag aponta para o commit `864647346418cc73344b199b95e79d02b3667a6d`. O commit avaliado está 354 commits à frente dessa tag. Portanto, os resultados desta fase correspondem especificamente ao commit `ba6db878`.

O inventário abrangeu documentação, código SvelteKit/TypeScript, backend Express/TypeScript, serviços Python, scripts de banco e Supabase, configurações, dependências, workflows de CI e testes.

---

## 3. Medições Viáveis

A **Tabela 2** consolida a viabilidade e o resultado das métricas.

| Característica | Métrica | Resultado | Classificação | Situação |
| :------------- | :------ | :-------- | :------------ | :------- |
| Adequação Funcional | CRF | 60,00% (9 de 15 requisitos) | Aceitável | Avaliada |
| Adequação Funcional | TDD | Não calculada | Inconclusiva | Sem operações e saídas esperadas |
| Adequação Funcional | CF | Não calculada | Inconclusiva | Sem normas e transações de referência |
| Manutenibilidade | M1 | 28,43% (29 de 102 ativos) | Inaceitável | Avaliada |
| Manutenibilidade | M2 | Não calculada | Inconclusiva | Sem registros de tempo útil |
| Manutenibilidade | M3 | Não calculada | Inconclusiva | Sem cenários de teste requeridos |
| Manutenibilidade | M4 | Não calculada | Inconclusiva | Sem lista de funções exigidas |
| Manutenibilidade | M5 | Não calculada | Inconclusiva | Sem critério objetivo de impacto |

<p align="center">Tabela 2 - Situação consolidada das métricas da Fase 4. Fonte: Equipe Carol Shaw, 2026.</p>

O resultado inconclusivo descreve a disponibilidade dos insumos da avaliação, e não uma reprovação automática do produto.

---

## 4. Resultados das Verificações

As suítes de testes e as verificações de código apresentaram os seguintes resultados:

| Área | Verificação | Resultado |
| :--- | :---------- | :-------- |
| Backend TypeScript | Jest com cobertura | 45 testes aprovados em 6 suítes; 19,67% de statements e 20,11% de linhas |
| Serviços Python | Pytest | 36 aprovados, 10 `xfail` e 1 ignorado, em 47 testes coletados |
| Frontend Svelte | Vitest | Não possui arquivos de teste |
| Frontend Svelte | `svelte-check` | 10 erros e 3 avisos em 8 arquivos |

<p align="center">Tabela 3 - Evidências auxiliares de teste e verificação. Fonte: Equipe Carol Shaw, 2026.</p>

Esses resultados apoiam o julgamento técnico, mas não substituem os denominadores exigidos por M3. A cobertura configurada no Pytest incide sobre o próprio diretório de testes, e não sobre os módulos de produção; portanto, ela não foi usada como medida de cobertura do produto.

Os detalhes estão nas páginas de [Adequação Funcional](adequacao_funcional.md), [Manutenibilidade](manutenibilidade.md) e [Evidências de Testes](evidencias/testes.md).

---

## 5. Relação com o Propósito da Avaliação

O propósito definido na Fase 1 é apoiar a priorização do backlog e a gestão do débito técnico. Os resultados obtidos indicam três prioridades fundamentadas:

1. revisar a especificação funcional para decompor requisitos compostos em capacidades atômicas e verificáveis;
2. completar os requisitos funcionais parcialmente implementados ou ausentes, pois a CRF atingiu apenas o limite inferior da faixa aceitável;
3. ampliar o reaproveitamento dos ativos de frontend, pois a M1 ficou abaixo do limite de 50%.

As demais decisões dependem de coleta adicional. Em especial, TDD e CF exigem massa de dados com resultados esperados e normas acadêmicas oficiais; M2 exige registro de tempo; e M3, M4 e M5 exigem denominadores que não estão definidos nos artefatos disponíveis.

---

## 6. Limitações

- A CRF considera a presença e a aderência estática da implementação; não abrange testes funcionais ponta a ponta em ambiente integrado.
- Parte dos requisitos funcionais não é atômica e reúne comportamentos independentes. A CRF considera o requisito completo como unidade binária, o que reduz a precisão da medida em casos de implementação parcial.
- Ausência de históricos acadêmicos de teste com resultados oficiais esperados.
- Ausência de um conjunto versionado de regras acadêmicas da UnB suficiente para TDD e CF.
- A especificação não enumera cenários de teste nem funções de diagnóstico requeridas.
- Não há registros de tempo útil por modificação.
- O método de M5 não define de forma inequívoca o que constitui impacto entre componentes.
- O commit avaliado difere da tag `V2.3.0` citada na Fase 1.

---

## 7. Referências

> 1. SOARES RAMOS, Cristiane. Processo de Avaliação de Produto de Software. Brasília: UnB, 2025. Material de aula (slides). Acesso em: 11/06/2026.
>
> 2. SOARES RAMOS, Cristiane. Projeto Final da Disciplina: Avaliação da Qualidade de Produto de Software. Brasília: UnB, 2026. Enunciado do trabalho final. Acesso em: 11/06/2026.
>
> 3. UNB-MDS. 2025-1-NoFluxoUNB. Disponível em: https://github.com/unb-mds/2025-1-NoFluxoUNB. Acesso em: 11/06/2026.

---

## Histórico de Versões

| Versão | Data | Descrição | Autor(es) | Revisor(es) | Data de Revisão | Alterações Realizadas |
| :----- | :--- | :-------- | :-------- | :----------- | :--------------- | :-------------------- |
| 1.0 | 11/06/2026 | Criação da introdução e consolidação da situação da Fase 4 | Equipe Carol Shaw |  |  |  |
| 1.1 | 11/06/2026 | Identificação do commit, consolidação das medidas e registro das limitações | Equipe Carol Shaw |  |  |  |
| 1.2 | 11/06/2026 | Revisão da redação acadêmica da página | Equipe Carol Shaw |  |  |  |
| 1.3 | 11/06/2026 | Inclusão da limitação de atomicidade da especificação funcional | Equipe Carol Shaw |  |  |  |
