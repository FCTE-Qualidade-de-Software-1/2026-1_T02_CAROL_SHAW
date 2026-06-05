# Propósito da Avaliação e Uso Pretendido

A avaliação do software NoFluxoUNB (versão 2.3.0) tem como objetivo central diagnosticar a maturidade do produto sob duas perspectivas críticas: a Adequação Funcional, para garantir que o sistema entregue todas as funcionalidades planejadas de forma correta, e a Manutenibilidade, para assegurar que o código permita manutenções e evoluções futuras sem alto custo ou risco de regressão.

Os resultados obtidos poderão ser utilizados pela equipe de desenvolvimento para fundamentar as seguintes decisões:

- Priorização do Backlog: Identificar quais módulos apresentam métricas críticas para direcionar esforços imediatos de refatoração e correção de bugs.

- Gestão de Débito Técnico: Avaliar se a versão atual possui estabilidade e manutenibilidade suficientes para a integração de novas funcionalidades ou se o ciclo de desenvolvimento deve focar exclusivamente em melhorias estruturais.

Dessa forma, a avaliação deixa de ser um processo passivo e passa a atuar como uma ferramenta de governança, garantindo que o software desempenhe suas funcionalidades conforme os requisitos de projeto.

# Escopo

A avaliação da versão 2.3.0 do NoFluxoUNB foca na integridade técnica do núcleo do sistema e na conformidade com o planejamento ágil documentado.

## 1. Objetos de Avaliação e Profundidade

O escopo está dividido em dois eixos principais:

Documentação (Foco em Adequação Funcional): Serão analisados o StoryMap, o documento de elicitação de requisitos, o diagrama de arquitetura, o Backlog e o Product Backlog Building (PBB).

- Profundidade: Comparação direta entre esses documentos e o software pronto para verificar se todas as funcionalidades planejadas foram realmente implementadas.

Análise Técnica de Código (Manutenibilidade): O objeto de análise é o código-fonte hospedado no GitHub.

- Profundidade: Análise da organização do código (modularidade) e da existência de testes (cobertura) para garantir que o sistema seja fácil de corrigir e evoluir.

## 2. O que fica de fora?

Interface e Performance: Não serão avaliados o design visual (UI) nem a velocidade de resposta do sistema.
O objetivo atual é garantir que o software funcione conforme os requisitos e que o código seja sólido. Aspectos visuais e de desempenho não serão tratados nesta avaliação.

## 3. Limites de Validade e Plano de Cobertura Progressiva

Limites de Validade: Os resultados obtidos refletem exclusivamente o estado do repositório no commit final da versão 2.3.0. Alterações posteriores na estrutura do PBB ou refatorações de código invalidam as métricas coletadas nesta rodada.

# Referências

> 1. SOARES RAMOS, Cristiane. Processo de Avaliação de Qualidade de Software. Brasília: UnB, 2026. Material de aula (slides). Acesso em: 12/05/2026

# Histórico de Versões

| Versão | Data       | Descrição                      | Autor(es)                                                     | Revisor(es) | Data de Revisão | Alterações Realizadas |
| ------ | ---------- | ------------------------------ | ------------------------------------------------------------- | ----------- | --------------- | --------------------- |
| 1.0    | 12/05/2026 | Escrita da página | [Gabriel Flores](https://github.com/Gabrielfcoelho) |             |                 |                       |