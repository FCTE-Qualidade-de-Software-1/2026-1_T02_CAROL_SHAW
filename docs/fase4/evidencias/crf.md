# Evidência da CRF

## 1. Critério de Avaliação

Os requisitos foram obtidos de `documentacao/planejamento/Requivitos/requisitos.md`, no commit `ba6db878b9dfa36fb034916612c4cf58ddf43475`. A avaliação considera os 15 requisitos funcionais de primeiro nível. Requisitos com implementação parcial são classificados como **ausentes/incorretos**.

### 1.1 Atomicidade dos requisitos

Parte dos requisitos reúne mais de um comportamento verificável. Essa estrutura impede uma classificação binária totalmente imparcial, pois um mesmo requisito pode conter capacidades implementadas e não implementadas.

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

<p align="center">Tabela 1 - Exemplos de requisitos funcionais não atômicos. Fonte: Equipe Carol Shaw, 2026.</p>

O RF05 evidencia o problema: fluxograma, destaque de disciplinas e equivalências estão implementados, mas a quantidade de tentativas ou reprovações não está. A unidade de contagem definida para a CRF exige que o requisito completo seja classificado como **ausente/incorreto**.

O cálculo foi mantido sobre os 15 requisitos de primeiro nível para preservar a rastreabilidade com as Fases 2 e 3. A medida resultante representa requisitos integralmente atendidos. Uma nova medição baseada em capacidades atômicas exigiria a revisão prévia da especificação e produziria um denominador diferente.

---

## 2. Matriz de Rastreabilidade

| ID | Requisito resumido | Situação | Evidências principais | Justificativa |
| :- | :----------------- | :------- | :-------------------- | :------------ |
| RF01 | Login e salvamento de simulações | Implementado | `src/lib/services/auth.service.ts`; `src/lib/stores/fluxograma.store.svelte.ts`; `src/lib/services/supabase-data.service.ts` | Há autenticação por senha/Google e persistência do fluxograma e planejamento do usuário. |
| RF02 | Upload de histórico em PDF | Implementado | `src/routes/upload-historico/+page.svelte`; `src/lib/components/upload/FileDropzone.svelte`; `src/lib/services/pdf/pdfParser.ts` | A interface aceita PDF, valida o arquivo e inicia o processamento. |
| RF03 | Identificar disciplinas cursadas, aprovadas e reprovadas | Implementado | `src/lib/services/pdf/pdfDataExtractor.ts`; `src/lib/services/pdf/pdfParser.ts`; `src/lib/types/user.ts` | O parser extrai disciplinas e preserva estados como APR, CUMP, REP, REPF e REPMF. |
| RF04 | Consultar fluxograma e equivalências no banco | Implementado | `src/lib/services/supabase-data.service.ts`; `src/lib/services/upload.service.ts`; `src/lib/services/fluxograma.service.ts` | Há consultas ao Supabase para matrizes, matérias, pré-requisitos, equivalências e RPC de casamento. |
| RF05 | Mostrar fluxograma, cursadas, equivalências e quantidade de tentativas/reprovações | Ausente/incorreto | `src/lib/components/fluxograma/SubjectCard.svelte`; `SubjectDetailsModal.svelte`; rotas `meu-fluxograma` | Fluxograma, estados e equivalências são exibidos, mas não há contagem de tentativas ou reprovações. |
| RF06 | Calcular e exibir porcentagem de conclusão | Implementado | `src/lib/services/upload.service.ts`; `src/lib/components/fluxograma/ProgressSummarySection.svelte` | O percentual é calculado e exibido no resumo de progresso. |
| RF07 | Calcular e exibir IRA e média ponderada | Implementado | `src/lib/services/pdf/pdfDataExtractor.ts`; `ProcessingResults.svelte`; `ProgressSummarySection.svelte` | Os dois indicadores são extraídos e apresentados na interface. |
| RF08 | Exibir horas complementares cumpridas e pendentes | Implementado | `src/lib/services/integralizacao.service.ts`; `CargaHorariaDashboard.svelte` | A integralização separa carga realizada, exigida e pendente, incluindo a categoria complementar. |
| RF09 | Gerar PDF da simulação | Ausente/incorreto | `src/lib/utils/screenshot.ts`; `FluxogramaHeader.svelte`; `ScreenshotChoiceModal.svelte` | A funcionalidade encontrada captura e baixa PNG, não PDF. |
| RF10 | Simular troca de curso e aproveitamento | Implementado | `MudancaCursoModal.svelte`; rota `meu-fluxograma/[courseName]`; `integralizacao.service.ts` | Há seleção de curso-alvo e recálculo da integralização com equivalências. |
| RF11 | Armazenar dados do usuário e simulações anteriores | Implementado | `src/lib/services/supabase-data.service.ts`; migrations de `historicos_usuarios` | O estado atual é atualizado em `dados_users` e cada envio pode ser inserido em `historicos_usuarios`. |
| RF12 | Exibir semestres cursados e restantes pelo tempo máximo | Ausente/incorreto | `pdfDataExtractor.ts`; `ProgressSummarySection.svelte` | O semestre atual é extraído e exibido, mas não há cálculo dos restantes nem uso do prazo máximo do curso. |
| RF13 | Identificar e exibir trancamentos | Ausente/incorreto | `pdfDataExtractor.ts`; `uploadStore.ts`; `supabase-data.service.ts` | Suspensões são extraídas e armazenadas, porém não são exibidas ao usuário. |
| RF14 | Identificar mudança de curso ocorrida e aproveitamentos | Ausente/incorreto | Modelos, serviços e componentes relacionados ao histórico | Não há campos ou fluxo para curso anterior, data da mudança e disciplinas aproveitadas de uma mudança passada. |
| RF15 | IA para cursos e disciplinas baseada em interesse, histórico e preferências | Ausente/incorreto | `src/routes/assistente/+page.svelte`; `assistente.service.ts`; `assistente-ui.service.ts` | O assistente recomenda disciplinas e recebe mensagem e matriz, mas não contempla recomendação de cursos nem o uso conjunto do histórico e de preferências persistidas. |

<p align="center">Tabela 2 - Matriz de rastreabilidade dos requisitos funcionais. Fonte: Equipe Carol Shaw, 2026.</p>

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

A matriz registra a presença e a aderência estática das funcionalidades. A disponibilidade operacional depende de validação ponta a ponta com banco de dados e serviços externos configurados.

A presença de requisitos compostos reduz a precisão da CRF. A decomposição em requisitos atômicos, com identificadores e critérios de aceitação independentes, é necessária para distinguir cobertura total, parcial e ausente sem introduzir subjetividade.

[Voltar para Adequação Funcional](../adequacao_funcional.md)
