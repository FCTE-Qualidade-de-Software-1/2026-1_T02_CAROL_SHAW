# Manutenibilidade

Esta página apresenta a execução da avaliação de **Manutenibilidade** sobre o commit [`ba6db878b9dfa36fb034916612c4cf58ddf43475`](https://github.com/unb-mds/2025-1-NoFluxoUNB/commit/ba6db878b9dfa36fb034916612c4cf58ddf43475) do [NoFluxoUNB](https://github.com/unb-mds/2025-1-NoFluxoUNB), em conformidade com as métricas especificadas na Fase 2 e com os procedimentos definidos na Fase 3.

---

## 1. Obtenção das Medidas

### 1.1 M1 - Execução de reusabilidade

Para a M1, o inventário adotou as seguintes unidades de análise:

- cada componente Svelte fora das famílias de UI;
- cada família de UI com arquivo público `index.ts`, contada como um ativo;
- cada módulo de hook, utilitário ou action;
- cada folha de estilo compartilhada.

Os arquivos internos de uma mesma família de interface não foram contabilizados separadamente. Um ativo foi classificado como reutilizado quando era importado por dois ou mais arquivos pertencentes a contextos distintos.

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

<p align="center">Tabela 1 - Dados brutos da M1 por tipo de ativo. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

Como verificação estática complementar, foi utilizado o [Knip 6.16.1](https://knip.dev/), que possui suporte a projetos [Svelte](https://knip.dev/reference/plugins/svelte) e [SvelteKit](https://knip.dev/reference/plugins/sveltekit). O comando abaixo foi executado a partir do diretório `no_fluxo_frontend_svelte`:

```powershell
npx.cmd --yes knip@6.16.1 --production --files
```

O Knip sinalizou 77 arquivos como não alcançados a partir dos pontos de entrada reconhecidos, dos quais 74 estavam em `src/lib`. Esse resultado foi utilizado para apoiar a identificação de candidatos sem uso, mas não compôs diretamente o numerador ou o denominador da M1.

O relatório possui as seguintes limitações em relação ao método da métrica:

- o Knip classifica arquivos não utilizados, enquanto a M1 conta ativos reutilizados por dois ou mais contextos;
- a ferramenta não informa diretamente a quantidade de arquivos distintos que importam cada ativo;
- cada arquivo interno de uma família de UI é analisado separadamente, enquanto a M1 agrupa a família pelo módulo público `index.ts`; entre os arquivos sinalizados, 46 pertenciam a essas famílias;
- arquivos auxiliares, gerados ou vinculados por convenções do framework podem exigir configuração adicional e revisão manual.

Portanto, o Knip foi adotado como evidência auxiliar de análise estática. O resultado de 29 ativos reutilizados em 102 permaneceu fundamentado no inventário e na inspeção dos contextos de importação definidos para a M1.

A relação dos 29 ativos reutilizados e suas contagens de contextos está em [Evidência da M1](evidencias/manutenibilidade/m1.md).

### 1.2 M2 - Complexidade de modificação

#### 1.2.1 Seleção de amostra de modificações e registro de tempo gasto

Para a realização do cálculo desta métrica foi selecionada uma amostra de modificações representativas recentes. As amostras foram obtidas no repositório do projeto no GitHub [NoFluxo](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues?q=is%3Aissue%20state%3Aclosed) e representam as issues fechadas durante o primeiro semestre de 2026.

| Issue | Abertura | Fechamento| Status | tempo em dias |
| ----- | -------- | --------- | ------ | ------------- |
|[[EPIC] Atualização da função do Darcy AI](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues/116)                          |02/04/2026|03/04/2026|implementado| 1 |
|[[FEAT] Implementar Recomendação Automática de Grade](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues/101)               |03/03/2026|11/03/2026|não implementado| NaN |
|[[FEAT] Criar Organizador de Grade para Próximo Semestre](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues/100)           |03/03/2026|11/03/2026|não implementado| NaN |
|[[FEAT/SPRINTS] Implementar Analytics de Vagas por Semestre](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues/99)        |03/03/2026|11/03/2026|não implementado| NaN |
|[[UPDATE] Refatoração sobre nós](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues/98)                                    |03/03/2026|06/04/2026|implementado| 3 |
|[[FEAT/SPRINTS] Validação e Padronização dos Fluxogramas Acadêmicos](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues/97)|03/03/2026|11/03/2026|implementado| 8 |
|[[FEAT/SPRINTS] Implementação e Otimização do Agente de IA](https://github.com/unb-mds/2025-1-NoFluxoUNB/issues/96)         |25/02/1026|12/03/2026|implementado| 15 |

<p align="center">Tabela 2 - Dados brutos da M2 obtidos no Repositório do GitHub do NoFluxo. Fonte: Gabriel Flores, 2026.</p>


#### 1.2.2 Consolidação das medidas obtidas

- **Número de Modificações:** 4
- **Tempo Total de Trabalho:** 27

#### 1.2.3 Cálculo M2

$$
M2 = \frac{\text{tempo total de trabalho}}{\text{número de modificações}}
$$

$$
M2 = \frac{\text{27}}{\text{4}}= 6{,}75
$$

#### 1.2.4 Análise e Conclusão

Após o cálculo da métrica M2 quanto a manutenabilidade é possível concluir que o time de desenvolvimento do NoFluxo leva em média 6,75 dias para concluir cada issue o que se enquadra como **Aceitável: entre 4 e 8 dias** de acordo com os critérios estabelecidos na fase 2.

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
1. Tratamento de Exceções: Lidar com falhas estruturais ou PDFs corrompidos no "Parser PDF".

2. Monitoramento de Performance: Garantir tempo de resposta inferior a 5 segundos (para fluxograma, geração de grade e parser).

3. Alertas Visuais: Mensagens de erro e avisos sobre disciplinas críticas na interface.

4. Monitoramento de Integração: Configuração de pipeline CI/CD (GitHub Actions) para rastrear erros de build.

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

#### 1.4.3 Cáculo M4

$$
M4 = \frac{\text{funções de diagnóstico implementadas}}{\text{funções exigidas na especificação}} \times 100
$$

$$
M4 = \frac{\text{12}}{\text{4}} \times 100 = 300\%
$$

#### 1.4.4 Análise e Conclusão

Após o cálculo da métrica M4 quanto a manutenabilidade é possível concluir que o time de desenvolvimento do NoFluxo possui mais funções de monitoramento implementadas do que especificadas o que demonstra bastante completude e se enquandra no critério **Desejável:>=100%** .

### 1.5 M5 - Condensabilidade

O mapa de dependências internas foi obtido por análise estática dos arquivos `.ts` de produção localizados em [`no_fluxo_backend/src/`](https://github.com/unb-mds/2025-1-NoFluxoUNB/tree/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_backend/src). Foram excluídos testes, arquivos de declaração, código gerado e dependências externas. Um componente foi classificado como **não dependente** quando não importava outro componente interno do backend.

O escopo foi restringido ao backend porque o [Madge 8.0.0](https://github.com/pahen/madge) processou diretamente todos os módulos TypeScript e produziu resultados reproduzíveis por linha de comando. No frontend, as ferramentas examinadas não resolveram de forma confiável as importações declaradas nos componentes `.svelte`. Nos serviços Python, o [Pydeps](https://pydeps.readthedocs.io/) não construiu o grafo em razão de nomes e caminhos incompatíveis com sua resolução de módulos. A exclusão desses subsistemas evita que a medida dependa de conversões, renomeações ou programas auxiliares não previstos no procedimento.

$$
M5 = \frac{\text{componentes não dependentes}}{\text{total de componentes}} \times 100
$$

$$
M5 = \frac{6}{20} \times 100 = 30{,}00\%
$$

| Subsistema | Componentes | Não dependentes | Dependentes | Relações internas |
| :--------- | ----------: | --------------: | ----------: | ----------------: |
| Backend TypeScript | 20 | 6 | 14 | 51 |

<p align="center">Tabela 4 - Dados brutos da M5 no backend. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

O resultado de 30,00% indica que 14 dos 20 componentes do backend possuem ao menos uma dependência interna direta. Não foram identificadas dependências circulares no escopo avaliado.

O mapa, as ferramentas, as relações de maior concentração e os componentes não dependentes estão em [Evidência da M5](evidencias/manutenibilidade/m5.md).

---

## 2. Comparação com os Critérios

| Métrica | Desejável | Aceitável | Inaceitável | Resultado | Classificação |
| :------ | :-------- | :-------- | :----------- | :-------- | :------------ |
| M1 | >= 80% | 50% a 79% | < 50% | 28,43% | Inaceitável |
| M2 | <= 4 h/modificação | > 4 e <= 8 d/modificação | > 8 d/modificação | 6,75 | Aceitável |
| M3 | 100% | 80% a 99% | < 80% | Não calculado | Inconclusiva |
| M4 | 100% | 80% a 99% | < 80% | 300% | Desejável |
| M5 | >= 80% | 50% a 79% | < 50% | 30,00% (backend) | Inaceitável |

<p align="center">Tabela 5 - Comparação das métricas de Manutenibilidade com os critérios da Fase 2. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

---

## 3. Respostas às Questões GQM

| Questão | Métrica | Resposta | Hipótese |
| :------ | :------ | :------- | :------- |
| Q1. Quão elevado é o reaproveitamento de componentes e ativos do frontend? | M1 | 28,43%, classificação inaceitável | H1 refutada |
| Q2. Qual é o esforço médio necessário para realizar modificações? | M2 | 6,75, classificação aceitável | H2 não confirmada nem refutada |
| Q3. Quão completa está a implementação dos testes previstos? | M3 | Inconclusiva | H3 não confirmada nem refutada |
| Q4. Quão completa está a implementação de monitoramento e diagnóstico? | M4 | 300%, classificação desejável | H4 confirmada |
| Q5. Quão independentes são os componentes do sistema? | M5 | No backend, 30,00%, classificação inaceitável | H5 refutada no escopo avaliado |

<p align="center">Tabela 5 - Respostas às questões GQM de Manutenibilidade. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

---

## 4. Julgamento e Ações de Melhoria

O resultado da M1 indica baixo reaproveitamento segundo o critério estabelecido. Entre os 102 ativos inventariados, 73 aparecem em menos de dois contextos. Parte desses ativos pode ser legitimamente específica de uma única tela; contudo, a métrica adotada não distingue especialização arquitetural de ausência de reutilização.

Quanto as métricas M2 e M4, é preciso melhorar produtividade da equipe para fechamento de issues e implementação de novas funcionalidades além de especificar na documentação as funções de monitoramento de maneira mais clara para melhor manutenção do código.

A M5 indica baixa independência entre os componentes do backend. O arquivo [`index.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_backend/src/index.ts) concentra 9 dependências internas diretas, [`assistente_controller.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_backend/src/controllers/assistente_controller.ts) possui 8 e [`fluxograma_controller.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_backend/src/controllers/fluxograma_controller.ts) possui 7. Embora não tenham sido encontrados ciclos, essa concentração amplia o conjunto de módulos que precisa ser compreendido e verificado durante alterações nesses componentes.

As ações fundamentadas pelas evidências são:

1. revisar os 73 ativos não reutilizados e remover os que não possuem import;
2. consolidar padrões repetidos de formulários, modais e layouts em componentes compartilhados;
3. manter famílias de UI expostas por módulos públicos e documentar seu uso;
4. criar a matriz de cenários requeridos para permitir o cálculo de M3;
5. adicionar testes de frontend e corrigir os 10 erros identificados pelo `svelte-check`;
6. definir a lista mínima de diagnóstico exigida para M4;
7. registrar tempo útil em tarefas futuras para viabilizar M2;
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

| Versão | Data | Descrição | Autor(es) |
| :----- | :--- | :-------- | :-------- |
| 1.0 | 11/06/2026 | Registro inicial da execução da avaliação de Manutenibilidade | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.1 | 11/06/2026 | Cálculo da M1, evidências auxiliares e registro das métricas inviáveis | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.2 | 12/06/2026 | Cálculo da M5 por análise estática de dependências | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.3 | 12/06/2026 | Restrição da M5 ao backend TypeScript para garantir reprodutibilidade | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.4 | 12/06/2026 | Consolidação da execução e da inviabilidade de cálculo da M3 | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.5 | 12/06/2026 | Inclusão do Knip como análise estática complementar da M1 e registro de suas limitações | [Caio Duarte](https://github.com/caioduart3) e [Gabriel Flores](https://github.com/Gabrielfcoelho) |
| 1.6 | 12/06/2026 | Cálculo das métricas M2 e M4,registro das métricas e análise | [Gabriel Flores](https://github.com/Gabrielfcoelho) |
