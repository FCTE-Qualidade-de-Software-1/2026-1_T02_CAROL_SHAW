# Manutenibilidade

Esta página apresenta a execução da avaliação de **Manutenibilidade** sobre o commit [`ba6db878b9dfa36fb034916612c4cf58ddf43475`](https://github.com/unb-mds/2025-1-NoFluxoUNB/commit/ba6db878b9dfa36fb034916612c4cf58ddf43475) do [NoFluxoUNB](https://github.com/unb-mds/2025-1-NoFluxoUNB), em conformidade com as métricas especificadas na Fase 2 e com os procedimentos definidos na Fase 3.

---

## 1. Obtenção das Medidas

### 1.1 M1 - Execução de reusabilidade

O inventário foi elaborado exclusivamente a partir do diretório `no_fluxo_frontend_svelte/src/lib/components`. Foram aplicadas as seguintes regras:

1. componentes Svelte independentes foram contados por arquivo;
2. componentes internos de uma família em `components/ui/<familia>/` foram agrupados pelo módulo público `index.ts`;
3. arquivos fora da pasta `components` não foram incluídos;
4. um componente foi considerado reutilizado quando importado por dois ou mais arquivos de contexto distintos;
5. imports internos de uma família de UI não foram considerados contexto externo.

A identificação dos contextos de importação foi realizada com a extensão Svelte no ambiente de desenvolvimento, conforme demonstrado no vídeo disponível na [Evidência da M1](evidencias/manutenibilidade/m1.md).

$$
M1 = \frac{\text{componentes reutilizados}}{\text{total de componentes inventariados}} \times 100
$$

$$
M1 = \frac{21}{82} \times 100 = 25{,}61\%
$$

| Tipo de componente | Total | Reutilizados | Não reutilizados |
| :----------------- | ----: | ------------: | ----------------: |
| Componentes Svelte independentes | 68 | 20 | 48 |
| Famílias de componentes de UI | 14 | 1 | 13 |
| **Total** | **82** | **21** | **61** |

<p align="center">Tabela 1 - Dados brutos da M1 por tipo de componente. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

A relação dos 21 componentes reutilizados, dos 61 componentes abaixo do limiar e suas contagens de contextos está na [Evidência da M1](evidencias/manutenibilidade/m1.md).

### 1.2 M2 - Complexidade de modificação

#### 1.2.1 Seleção da amostra

Foram examinadas issues fechadas durante o primeiro semestre de 2026 no repositório do [NoFluxoUNB](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues?q=is%3Aissue%20state%3Aclosed).

| Issue | Status | Tempo registrado |
| :---- | :----- | ---------------: |
| [[EPIC] Atualização da função do Darcy AI](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues/116) | Implementado | 1 dia |
| [[FEAT] Implementar Recomendação Automática de Grade](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues/101) | Não implementado | Não contabilizado |
| [[FEAT] Criar Organizador de Grade para Próximo Semestre](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues/100) | Não implementado | Não contabilizado |
| [[FEAT/SPRINTS] Implementar Analytics de Vagas por Semestre](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues/99) | Não implementado | Não contabilizado |
| [[UPDATE] Refatoração sobre nós](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues/98) | Implementado | 3 dias |
| [[FEAT/SPRINTS] Validação e Padronização dos Fluxogramas Acadêmicos](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues/97) | Implementado | 8 dias |
| [[FEAT/SPRINTS] Implementação e Otimização do Agente de IA](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues/96) | Implementado | 15 dias |

<p align="center">Tabela 2 - Dados brutos da M2 obtidos no Repositório do GitHub do NoFluxo. Fonte: Gabriel Flores, 2026.</p>


#### 1.2.2 Cálculo

$$
M2 = \frac{\text{tempo total de resolução das modificações implementadas}}{\text{número de modificações implementadas}}
$$

Foram contabilizadas quatro modificações implementadas, com tempos registrados de 1, 3, 8 e 15 dias:

$$
M2 = \frac{1 + 3 + 8 + 15}{4} = \frac{27}{4} = 6{,}75 \text{ dias por modificação}
$$

O resultado de **6,75 dias por modificação** está na faixa aceitável, acima de 4 e até 8 dias. A medida representa o tempo de resolução registrado na amostra e não o esforço ativo dedicado exclusivamente à implementação.

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

#### 1.4.1 Lista de funções de diagnóstico

Funções de diagnóstico previstas:

1. Tratamento de Exceções: lidar com falhas estruturais ou PDFs corrompidos no parser de PDF.
2. Monitoramento de Performance: garantir tempo de resposta inferior a 5 segundos para fluxograma, geração de grade e parser.
3. Alertas Visuais: apresentar mensagens de erro e avisos sobre disciplinas críticas na interface.
4. Monitoramento de Integração: utilizar o pipeline de CI/CD do GitHub Actions para rastrear erros de build.

#### 1.4.2 Funções de diagnóstico encontradas

| Função Implementada | Localização no Repositório (Exemplos) | Categoria | Descrição |
| :--- | :--- | :--- | :--- |
| **Custom Logger Service** | `no_fluxo_backend/src/logger.ts` | Logging | Sistema estruturado para registrar eventos, avisos e erros críticos do servidor Node.js. |
| **Controller Request Logger** | `no_fluxo_backend/src/utils/controller_logger.ts` | Logging / Tracing | Rastreamento específico de requisições HTTP e latência nas rotas (fluxograma, cursos, etc). |
| **File-based AI Agent Logs** | `logs/ai_agent.log` | Logging | Persistência de logs do comportamento do Agente de IA e integração RAGFlow em arquivo físico. |
| **Global Error Route** | `no_fluxo_frontend_svelte/src/routes/+error.svelte` | Tratamento de Erro | Captura falhas críticas de roteamento ou exceções não tratadas e renderiza uma página de erro amigável. |
| **Authentication Error Boundary** | `.../components/auth/AuthErrorBoundary.svelte` | Tratamento de Erro | Impede que erros durante o processo de comunicação com o Supabase crashem o app inteiro. |
| **Parser Exception Handling** | `no_fluxo_backend/parse-pdf/pdf_parser_final.py` | Tratamento de Erro | Blocos try/except para evitar que PDFs ilegíveis interrompam o processamento de históricos. |
| **Toasts de Feedback (UI)** | `no_fluxo_frontend_svelte/src/lib/utils/toast.ts` | Mensagem de Erro | Componente dinâmico para avisar o usuário de forma visual sobre falhas de rede ou validação no frontend. |
| **Alertas de Segurança (UI)** | `.../components/ui/AuthErrorAlert.svelte` | Mensagem de Erro | Renderização visual específica para credenciais inválidas ou acesso não autorizado. |
| **Grafana Logs Dashboard** | `kubernetes_docs/.../apps-logs-dashboard.json` | Monitoramento | Telemetria para visualização centralizada dos logs dos containers da aplicação. |
| **Grafana Node/Build Dashboard** | `kubernetes_docs/.../node-connectivity-dashboard.json` | Monitoramento | Telemetria para monitorar latência, quedas de rede e desempenho de infraestrutura. |
| **Shell Memory Monitor** | `no_fluxo_backend/monitor_memory.sh` | Monitoramento | Script utilitário em bash para auditoria ativa do consumo de memória do servidor. |
| **Code Coverage Telemetry** | `codecov.yml (raiz)` | Monitoramento / CI | Rastreamento automatizado da porcentagem de código validada por testes automatizados. |

<p align="center">Tabela 3 - Dados brutos da M4 obtidos no Repositório do GitHub do NoFluxo. Fonte: Gabriel Flores, 2026.</p>

#### 1.4.3 Cálculo da M4

$$
M4 = \frac{\text{funções de diagnóstico implementadas}}{\text{funções exigidas na especificação}} \times 100
$$

$$
M4 = \frac{12}{4} \times 100 = 300\%
$$

#### 1.4.4 Análise e conclusão

Foram identificadas 12 funções de diagnóstico e monitoramento para quatro funções previstas. O resultado da M4 foi de **300%**, classificado como **desejável**, confirmando a hipótese H4.

### 1.5 M5 - Condensabilidade

O mapa de dependências internas foi obtido por análise estática dos arquivos `.ts` de produção localizados em [`no_fluxo_backend/src/`](https://github.com/unb-mds/2025-1-NoFluxoUNB/tree/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_backend/src). Foram excluídos testes, arquivos de declaração, código gerado e dependências externas. Um componente foi classificado como **sem dependências internas** quando não importava outro componente do backend.

O escopo foi restringido ao backend porque o [Madge 8.0.0](https://github.com/pahen/madge) processou diretamente todos os módulos TypeScript e produziu resultados reproduzíveis por linha de comando. No frontend, as ferramentas examinadas não resolveram de forma confiável as importações declaradas nos componentes `.svelte`. Nos serviços Python, o [Pydeps](https://pydeps.readthedocs.io/) não construiu o grafo em razão de nomes e caminhos incompatíveis com sua resolução de módulos. A exclusão desses subsistemas evita que a medida dependa de conversões, renomeações ou programas auxiliares não previstos no procedimento.

$$
M5 = \frac{\text{componentes sem dependências internas}}{\text{total de componentes avaliados}} \times 100
$$

$$
M5 = \frac{6}{20} \times 100 = 30{,}00\%
$$

| Subsistema | Componentes | Sem dependências internas | Com dependências internas | Relações internas |
| :--------- | ----------: | --------------: | ----------: | ----------------: |
| Backend TypeScript | 20 | 6 | 14 | 51 |

<p align="center">Tabela 4 - Dados brutos da M5 no backend. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

O resultado de 30,00% indica que 6 dos 20 componentes não importam outros arquivos internos, enquanto 14 possuem ao menos uma dependência interna direta. Não foram identificadas dependências circulares no escopo avaliado.

O mapa, as ferramentas, as relações de maior concentração e os componentes sem dependências internas estão em [Evidência da M5](evidencias/manutenibilidade/m5.md).

---

## 2. Comparação com os Critérios

| Métrica | Desejável | Aceitável | Inaceitável | Resultado | Classificação |
| :------ | :-------- | :-------- | :----------- | :-------- | :------------ |
| M1 | >= 80% | 50% a 79% | < 50% | 25,61% | Inaceitável |
| M2 | <= 4 dias/modificação | > 4 e <= 8 dias/modificação | > 8 dias/modificação | 6,75 dias/modificação | Aceitável |
| M3 | 100% | 80% a 99% | < 80% | Não calculado | Inconclusiva |
| M4 | 100% | 80% a 99% | < 80% | 300% | Desejável |
| M5 | >= 80% | 50% a 79% | < 50% | 30,00% (backend) | Inaceitável |

<p align="center">Tabela 5 - Comparação das métricas de Manutenibilidade com os critérios da Fase 2. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

---

## 3. Respostas às Questões GQM

| Questão | Métrica | Resposta | Hipótese |
| :------ | :------ | :------- | :------- |
| Q1. Quão elevado é o reaproveitamento dos componentes do frontend? | M1 | 25,61%, classificação inaceitável | H1 refutada |
| Q2. Qual é o tempo médio necessário para concluir modificações? | M2 | 6,75 dias por modificação, classificação aceitável | H2 não confirmada |
| Q3. Quão completa está a implementação dos testes previstos? | M3 | Inconclusiva | H3 não confirmada nem refutada |
| Q4. Quão completa está a implementação de monitoramento e diagnóstico? | M4 | 300%, classificação desejável | H4 confirmada |
| Q5. Qual é a proporção de componentes sem dependências internas diretas? | M5 | No backend, 30,00%, classificação inaceitável | H5 refutada no escopo avaliado |

<p align="center">Tabela 6 - Respostas às questões GQM de Manutenibilidade. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

---

## 4. Julgamento e Ações de Melhoria

O resultado da M1 indica baixo reaproveitamento segundo o critério estabelecido. Entre os 82 componentes inventariados, 61 aparecem em menos de dois contextos. Parte desses componentes pode ser legitimamente específica de uma única tela; contudo, a métrica adotada não distingue especialização arquitetural de ausência de reutilização.

A M2 apresentou resultado aceitável, com média de 6,75 dias por modificação implementada. Como a hipótese H2 estabelece o nível desejável de até 4 dias, ela não foi confirmada. A M3 permanece inconclusiva porque a especificação não enumera os cenários de teste requeridos. A M4 atingiu 300%, resultado classificado como desejável.

A M5 indica baixa independência de importação entre os componentes do backend. O arquivo [`index.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_backend/src/index.ts) importa 9 componentes internos, [`assistente_controller.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_backend/src/controllers/assistente_controller.ts) importa 8 e [`fluxograma_controller.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_backend/src/controllers/fluxograma_controller.ts) importa 7. Embora não tenham sido encontrados ciclos, essa concentração amplia o conjunto de módulos que precisa ser compreendido durante alterações nesses componentes.

As ações fundamentadas pelas evidências são:

1. revisar os 61 componentes não reutilizados e remover os que não possuem imports;
2. consolidar padrões repetidos de formulários, modais e layouts em componentes compartilhados;
3. manter famílias de UI expostas por módulos públicos e documentar seu uso;
4. criar a matriz de cenários requeridos para permitir o cálculo de M3;
5. adicionar testes de frontend e corrigir os 10 erros identificados pelo `svelte-check`;
6. documentar com maior clareza as funções de diagnóstico previstas;
7. manter o registro padronizado do tempo de resolução das issues;
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

| Versão | Data       | Descrição                      | Autor(es)                                                     | Revisor(es) | Data de Revisão | Alterações Realizadas |
| ------ | ---------- | ------------------------------ | ------------------------------------------------------------- | ----------- | --------------- | --------------------- |
| 1.0    | 11/06/2026 | Registro inicial da execução da avaliação de Manutenibilidade | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |  |  |  |
| 1.1    | 11/06/2026 | Cálculo da M1, evidências auxiliares e registro das métricas inviáveis | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |  |  |  |
| 1.2    | 12/06/2026 | Cálculo da M5 por análise estática de dependências | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |  |  |  |
| 1.3    | 12/06/2026 | Restrição da M5 ao backend TypeScript para garantir reprodutibilidade | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |  |  |  |
| 1.4    | 12/06/2026 | Consolidação da execução e da inviabilidade de cálculo da M3 | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |  |  |  |
| 1.6    | 12/06/2026 | Cálculo das métricas M2 e M4, registro das métricas e análise | [Gabriel Flores](https://github.com/Gabrielfcoelho) |  |  |  |
| 1.7    | 13/06/2026 | Correção da M1 e revisão das métricas M2 e M4 | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |  |  |  |
| 1.8    | 13/06/2026 | Adequação da definição da M2 ao tempo de resolução utilizado na execução | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |  |  |  |
| 1.9    | 13/06/2026 | Sincronização das medidas e do escopo com as evidências da Fase 4 | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |  |  |  |
| 1.10   | 13/06/2026 | Restauração do cálculo e da classificação original da M4 conforme o commit 443ee2e | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |  |  |  |
| 1.11   | 13/06/2026 | Alinhamento da M1 à inspeção de referências dos componentes | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |  |  |  |
