# Evidência da CRF

## 1. Critério de Avaliação

Os requisitos foram obtidos do documento [`documentacao/planejamento/Requivitos/requisitos.md`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/documentacao/planejamento/Requivitos/requisitos.md), no commit [`ba6db878b9dfa36fb034916612c4cf58ddf43475`](https://github.com/unb-mds/2025-1-NoFluxoUNB/commit/ba6db878b9dfa36fb034916612c4cf58ddf43475). A avaliação abrange os 15 requisitos funcionais de primeiro nível. Requisitos com implementação parcial foram classificados como **ausentes/incorretos**, em conformidade com o método definido na Fase 3.

### 1.1 Atomicidade dos requisitos

Parte dos requisitos agrega mais de um comportamento verificável. Essa estrutura limita a objetividade da classificação binária, pois um mesmo requisito pode reunir capacidades implementadas e não implementadas.

| Requisito | Capacidades agregadas |
| :-------- | :-------------------- |
| RF05 | Mostrar o fluxograma, destacar disciplinas cursadas, apresentar equivalências e informar tentativas ou reprovações |
| RF07 | Calcular e exibir IRA e média ponderada |
| RF08 | Identificar e exibir horas complementares cumpridas e pendentes |
| RF11 | Armazenar dados do usuário e simulações anteriores |
| RF12 | Exibir semestres cursados e restantes com base no tempo máximo |
| RF13 | Identificar ocorrência, quantidade e períodos de trancamento |
| RF14 | Identificar mudança de curso, curso anterior, data e disciplinas aproveitadas |
| RF15 | Recomendar cursos e disciplinas com base em interesse, histórico e preferências |

<p align="center">Tabela 1 - Exemplos de requisitos funcionais não atômicos. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

O RF05 evidencia essa limitação: a apresentação do fluxograma, o destaque das disciplinas cursadas e a exibição das equivalências possuem evidências de implementação, enquanto a quantidade de tentativas ou reprovações permanece ausente. Como a unidade de contagem da CRF é o requisito completo, o RF05 foi classificado como **ausente/incorreto**.

O cálculo foi mantido sobre os 15 requisitos de primeiro nível para preservar a rastreabilidade com as Fases 2 e 3. A medida resultante representa, portanto, a proporção de requisitos integralmente atendidos. Uma medição baseada em capacidades atômicas exigiria a revisão prévia da especificação e produziria um denominador distinto.

---

## 2. Matriz de Rastreabilidade

| ID | Requisito resumido | Situação | Evidências principais | Justificativa |
| :- | :----------------- | :------- | :-------------------- | :------------ |
| RF01 | Login e salvamento de simulações | Implementado | [`auth.service.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/auth.service.ts); [`fluxograma.store.svelte.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/stores/fluxograma.store.svelte.ts); [`supabase-data.service.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/supabase-data.service.ts) | Há autenticação por senha e Google, além da persistência do fluxograma e do planejamento do usuário. |
| RF02 | Upload de histórico em PDF | Implementado | [`upload-historico/+page.svelte`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/routes/upload-historico/%2Bpage.svelte); [`FileDropzone.svelte`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/components/upload/FileDropzone.svelte); [`pdfParser.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/pdf/pdfParser.ts) | A interface aceita arquivos PDF, valida o formato e inicia seu processamento. |
| RF03 | Identificar disciplinas cursadas, aprovadas e reprovadas | Implementado | [`pdfDataExtractor.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/pdf/pdfDataExtractor.ts); [`pdfParser.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/pdf/pdfParser.ts); [`user.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/types/user.ts) | O parser extrai as disciplinas e preserva situações acadêmicas como `APR`, `CUMP`, `REP`, `REPF` e `REPMF`. |
| RF04 | Consultar fluxograma e equivalências no banco | Implementado | [`supabase-data.service.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/supabase-data.service.ts); [`upload.service.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/upload.service.ts); [`fluxograma.service.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/fluxograma.service.ts) | Há consultas ao Supabase para matrizes, componentes curriculares, pré-requisitos, equivalências e procedimentos de correspondência. |
| RF05 | Mostrar fluxograma, cursadas, equivalências e quantidade de tentativas/reprovações | Ausente/incorreto | [`SubjectCard.svelte`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/components/fluxograma/SubjectCard.svelte); [`SubjectDetailsModal.svelte`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/components/fluxograma/SubjectDetailsModal.svelte); [rotas `meu-fluxograma`](https://github.com/unb-mds/2025-1-NoFluxoUNB/tree/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/routes/meu-fluxograma) | O fluxograma, as situações acadêmicas e as equivalências são exibidos, mas não há contagem de tentativas ou reprovações. |
| RF06 | Calcular e exibir porcentagem de conclusão | Implementado | [`upload.service.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/upload.service.ts); [`ProgressSummarySection.svelte`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/components/fluxograma/ProgressSummarySection.svelte) | O percentual é calculado e apresentado no resumo de progresso. |
| RF07 | Calcular e exibir IRA e média ponderada | Implementado | [`pdfDataExtractor.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/pdf/pdfDataExtractor.ts); [`ProcessingResults.svelte`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/components/upload/ProcessingResults.svelte); [`ProgressSummarySection.svelte`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/components/fluxograma/ProgressSummarySection.svelte) | Os dois indicadores são extraídos e apresentados na interface. |
| RF08 | Exibir horas complementares cumpridas e pendentes | Implementado | [`integralizacao.service.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/integralizacao.service.ts); [`CargaHorariaDashboard.svelte`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/components/fluxograma/CargaHorariaDashboard.svelte) | A integralização distingue a carga horária realizada, exigida e pendente, incluindo a categoria complementar. |
| RF09 | Gerar PDF da simulação | Ausente/incorreto | [`screenshot.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/utils/screenshot.ts); [`FluxogramaHeader.svelte`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/components/fluxograma/FluxogramaHeader.svelte); [`ScreenshotChoiceModal.svelte`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/components/fluxograma/ScreenshotChoiceModal.svelte) | A funcionalidade disponível captura e exporta a simulação em PNG, e não em PDF. |
| RF10 | Simular troca de curso e aproveitamento | Implementado | [`MudancaCursoModal.svelte`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/components/fluxograma/MudancaCursoModal.svelte); [rota `meu-fluxograma/[courseName]`](https://github.com/unb-mds/2025-1-NoFluxoUNB/tree/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/routes/meu-fluxograma/%5BcourseName%5D); [`integralizacao.service.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/integralizacao.service.ts) | Há seleção do curso de destino e recálculo da integralização com base nas equivalências. |
| RF11 | Armazenar dados do usuário e simulações anteriores | Implementado | [`supabase-data.service.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/supabase-data.service.ts); [`latest_init_from_export.sql`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_backend/docs/supabase_migrations/latest_init_from_export.sql) | O estado atual é atualizado em `dados_users`, e cada envio pode ser registrado em `historicos_usuarios`. |
| RF12 | Exibir semestres cursados e restantes pelo tempo máximo | Ausente/incorreto | [`pdfDataExtractor.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/pdf/pdfDataExtractor.ts); [`ProgressSummarySection.svelte`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/components/fluxograma/ProgressSummarySection.svelte) | O semestre atual é extraído e exibido, mas não há cálculo dos semestres restantes nem utilização do prazo máximo do curso. |
| RF13 | Identificar e exibir trancamentos | Ausente/incorreto | [`pdfDataExtractor.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/pdf/pdfDataExtractor.ts); [`uploadStore.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/stores/uploadStore.ts); [`supabase-data.service.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/supabase-data.service.ts) | Os períodos de suspensão são extraídos e armazenados, porém não são apresentados ao usuário. |
| RF14 | Identificar mudança de curso ocorrida e aproveitamentos | Ausente/incorreto | [`user.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/types/user.ts); [`supabase-data.service.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/supabase-data.service.ts); [componentes de fluxograma](https://github.com/unb-mds/2025-1-NoFluxoUNB/tree/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/components/fluxograma) | Não foram identificados campos ou fluxo funcional para registrar o curso anterior, a data da mudança e os componentes aproveitados em uma mudança já ocorrida. |
| RF15 | Recomendação de cursos e disciplinas baseada em interesse, histórico e preferências | Ausente/incorreto | [`assistente/+page.svelte`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/routes/assistente/%2Bpage.svelte); [`assistente.service.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/assistente.service.ts); [`assistente-ui.service.ts`](https://github.com/unb-mds/2025-1-NoFluxoUNB/blob/ba6db878b9dfa36fb034916612c4cf58ddf43475/no_fluxo_frontend_svelte/src/lib/services/assistente-ui.service.ts) | O assistente recomenda disciplinas e recebe a mensagem e a matriz curricular, mas não contempla a recomendação de cursos nem o uso conjunto do histórico e de preferências persistidas. |

<p align="center">Tabela 2 - Matriz de rastreabilidade dos requisitos funcionais. Fonte: Caio Duarte e Gabriel Flores, 2026.</p>

---

## 3. Cálculo

| Classificação | Quantidade |
| :------------ | ---------: |
| Implementado | 9 |
| Ausente/incorreto | 6 |
| Total | 15 |

$$
CRF = \frac{15 - 6}{15} \times 100 = 60{,}00\%
$$

---

## 4. Limitações

A matriz registra a presença e a aderência estática das funcionalidades. A disponibilidade operacional dessas capacidades depende de validação ponta a ponta em ambiente integrado, com banco de dados e serviços externos devidamente configurados.

A presença de requisitos compostos reduz a precisão da CRF. A decomposição em requisitos atômicos, com identificadores e critérios de aceitação independentes, é necessária para distinguir atendimento integral, parcial e ausente com menor grau de subjetividade.

## Histórico de Versões

| Versão | Data | Descrição | Autor(es) |
| :----- | :--- | :-------- | :-------- |
| 1.0 | 11/06/2026 | Registro da matriz de rastreabilidade e cálculo da CRF | [Caio Duarte](https://github.com/caioduart3)|
| 1.1 | 11/06/2026 | Inclusão da análise de atomicidade dos requisitos funcionais | [Caio Duarte](https://github.com/caioduart3)  |

[Voltar para Adequação Funcional](../../adequacao_funcional.md)
