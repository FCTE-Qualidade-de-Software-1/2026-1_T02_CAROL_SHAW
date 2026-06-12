# Sobre a Fase 4

## 1. Introdução

A Fase 4, denominada **Executar a Avaliação**, corresponde à aplicação dos requisitos definidos na Fase 1, das métricas e dos critérios estabelecidos na Fase 2 e dos procedimentos planejados na Fase 3. De acordo com o Processo de Avaliação de Produto de Software, esta etapa compreende três atividades:

1. obter as medidas;
2. comparar as medidas com os critérios estabelecidos;
3. julgar os resultados e propor ações de melhoria.

---

## 2. Versão e Escopo Avaliados

A avaliação incidiu sobre o [NoFluxoUNB](https://github.com/unb-mds/2025-1-NoFluxoUNB) no estado identificado a seguir:

| Item | Valor |
| :--- | :---- |
| Repositório | [unb-mds/2025-1-NoFluxoUNB](https://github.com/unb-mds/2025-1-NoFluxoUNB) |
| Commit avaliado | [`ba6db878b9dfa36fb034916612c4cf58ddf43475`](https://github.com/unb-mds/2025-1-NoFluxoUNB/commit/ba6db878b9dfa36fb034916612c4cf58ddf43475) |
| Identificação pelo Git | `V2.3.0-354-gba6db878` |
| Data da coleta | 11/06/2026 |

<p align="center">Tabela 1 - Identificação do produto avaliado. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

A Fase 1 referencia a versão [`V2.3.0`](https://github.com/unb-mds/2025-1-NoFluxoUNB/tree/V2.3.0), associada ao commit [`864647346418cc73344b199b95e79d02b3667a6d`](https://github.com/unb-mds/2025-1-NoFluxoUNB/commit/864647346418cc73344b199b95e79d02b3667a6d). O estado avaliado encontra-se 354 commits à frente dessa tag. Consequentemente, os resultados apresentados nesta fase são válidos para o commit [`ba6db878`](https://github.com/unb-mds/2025-1-NoFluxoUNB/commit/ba6db878b9dfa36fb034916612c4cf58ddf43475) e não devem ser generalizados para outras versões sem nova coleta.

O inventário contemplou a documentação, o frontend em [SvelteKit](https://svelte.dev/docs/kit) e TypeScript, o backend em Express e TypeScript, os serviços Python, os scripts de banco de dados, a integração com [Supabase](https://supabase.com/docs), os arquivos de configuração, as dependências, os [fluxos de integração contínua](https://github.com/unb-mds/2025-1-NoFluxoUNB/tree/ba6db878b9dfa36fb034916612c4cf58ddf43475/.github/workflows) e as suítes de testes.

---

## 3. Medições Viáveis

A **Tabela 2** sintetiza a viabilidade de execução e os resultados obtidos para cada métrica.

| Característica | Métrica | Resultado | Classificação | Situação |
| :------------- | :------ | :-------- | :------------ | :------- |
| Adequação Funcional | CRF | 60,00% (9 de 15 requisitos) | Aceitável | Avaliada |
| Adequação Funcional | TDD | Não calculada | Inconclusiva | Amostra incompatível com o plano |
| Adequação Funcional | CF | 70,00% (21 de 30 transações) | Inaceitável | Avaliada |
| Manutenibilidade | M1 | 28,43% (29 de 102 ativos) | Inaceitável | Avaliada |
| Manutenibilidade | M2 | Não calculada | Inconclusiva | Sem registros de tempo útil |
| Manutenibilidade | M3 | Não calculada | Inconclusiva | Sem cenários de teste requeridos |
| Manutenibilidade | M4 | Não calculada | Inconclusiva | Sem lista de funções exigidas |
| Manutenibilidade | M5 | 30,00% (6 de 20 componentes) | Inaceitável | Avaliada no backend |

<p align="center">Tabela 2 - Situação consolidada das métricas da Fase 4. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

A classificação **inconclusiva** indica insuficiência dos dados necessários ao cálculo e não constitui, por si só, uma avaliação negativa do produto.

---

## 4. Resultados das Verificações

As execuções das suítes de testes e das verificações estáticas produziram os resultados apresentados na **Tabela 3**.

| Área | Verificação | Resultado |
| :--- | :---------- | :-------- |
| Backend TypeScript | [Jest](https://jestjs.io/docs/getting-started) com cobertura | 45 testes aprovados em 6 suítes; 19,67% de instruções e 20,11% de linhas |
| Serviços Python | [pytest](https://docs.pytest.org/) | 36 testes aprovados, 10 falhas esperadas (`xfail`) e 1 teste ignorado, em 47 testes coletados |
| Frontend Svelte | [Vitest](https://vitest.dev/guide/) | Nenhum arquivo de teste localizado |
| Frontend Svelte | [`svelte-check`](https://svelte.dev/docs/cli/sv-check) | 10 erros e 3 avisos distribuídos em 8 arquivos |

<p align="center">Tabela 3 - Evidências auxiliares de teste e verificação. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

Esses resultados constituem evidências auxiliares para o julgamento técnico, mas não fornecem o denominador exigido pela M3. Além disso, a configuração de cobertura do pytest incide predominantemente sobre o próprio diretório de testes, e não sobre os módulos de produção. Por essa razão, o percentual resultante não foi interpretado como cobertura do produto.

Os detalhes estão nas páginas de [Adequação Funcional](adequacao_funcional.md), [Manutenibilidade](manutenibilidade.md) e [Evidência da M3](evidencias/manutenibilidade/m3.md).

---

## 5. Relação com o Propósito da Avaliação

O propósito estabelecido na Fase 1 consiste em apoiar a priorização do backlog e a gestão do débito técnico. À luz dos resultados obtidos, foram identificadas cinco prioridades:

1. revisar a especificação funcional para decompor requisitos compostos em capacidades atômicas e verificáveis;
2. completar os requisitos funcionais parcialmente implementados ou ausentes, pois a CRF atingiu apenas o limite inferior da faixa aceitável;
3. corrigir as divergências da matriz 6360/1, especialmente a natureza de `FGA0146`, o reconhecimento de componentes cumpridos e equivalentes e a apresentação do semestre atual;
4. ampliar o reaproveitamento dos ativos de frontend, pois a M1 ficou abaixo do limite de 50%;
5. reduzir a concentração de dependências em `index.ts`, `assistente_controller.ts` e `fluxograma_controller.ts` no backend.

As demais decisões requerem coleta complementar. A TDD depende de uma massa de dados compatível com os cursos e os tipos de operação definidos na Fase 3; a M2 requer registros de tempo útil; e as métricas M3 e M4 dependem de denominadores que não estão especificados nos artefatos disponíveis.

---

## 6. Limitações

- A CRF considera a presença e a aderência estática da implementação; não abrange testes funcionais ponta a ponta em ambiente integrado.
- Parte dos requisitos funcionais não é atômica e reúne comportamentos independentes. A CRF considera o requisito completo como unidade binária, o que reduz a precisão da medida em casos de implementação parcial.
- A CF abrange somente a estrutura curricular de Engenharia de Software 6360/1, vigente desde 2017.1.
- A amostra da CF contém cinco matrículas únicas; o documento mais antigo da matrícula `211029503` foi excluído.
- A massa disponível não cobre a variedade de cursos e operações planejada para a TDD.
- Regras de pré-requisito, limites de matrícula e prazos de conclusão não foram exercitados na CF.
- A M5 abrange exclusivamente o backend TypeScript. As ferramentas examinadas não resolveram de forma confiável as importações dos componentes `.svelte`, enquanto o [Pydeps](https://pydeps.readthedocs.io/) não construiu o grafo dos módulos Python em razão da organização dos nomes de arquivos e caminhos.
- A M5 mede dependências internas diretas no nível de arquivo; não estima impacto semântico nem dependências de execução não expressas por imports.
- A especificação não enumera cenários de teste nem funções de diagnóstico requeridas.
- Não há registros de tempo útil por modificação.
- O commit avaliado difere da tag `V2.3.0` citada na Fase 1.

---

## 7. Referências

> 1. SOARES RAMOS, Cristiane. Processo de Avaliação de Produto de Software. Brasília: UnB, 2025. Material de aula (slides). Acesso em: 11/06/2026.
>
> 2. SOARES RAMOS, Cristiane. Projeto Final da Disciplina: Avaliação da Qualidade de Produto de Software. Brasília: UnB, 2026. Enunciado do trabalho final. Acesso em: 11/06/2026.
>
> 3. UNB-MDS. [2025-1-NoFluxoUNB](https://github.com/unb-mds/2025-1-NoFluxoUNB). Acesso em: 11/06/2026.

---

## Histórico de Versões

| Versão | Data | Descrição | Autor(es) |
| :----- | :--- | :-------- | :-------- |
| 1.0 | 11/06/2026 | Criação da introdução e consolidação da situação da Fase 4 | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.1 | 11/06/2026 | Identificação do commit, consolidação das medidas e registro das limitações | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.2 | 11/06/2026 | Inclusão da limitação de atomicidade da especificação funcional | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.3 | 12/06/2026 | Consolidação do resultado da CF para o currículo 6360/1 - 2017.1 | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.4 | 12/06/2026 | Atualização da CF após deduplicação e verificação do semestre atual | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.5 | 12/06/2026 | Consolidação do resultado da M5 | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.6 | 12/06/2026 | Restrição da M5 ao backend TypeScript | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.7 | 12/06/2026 | Consolidação das evidências e da inviabilidade de cálculo da M3 | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
