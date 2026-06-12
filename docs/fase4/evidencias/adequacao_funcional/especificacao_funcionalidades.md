# Especificação de Funcionalidades e Backlog — NoFluxoUnB

Este documento apresenta o levantamento completo das funcionalidades, requisitos e tarefas técnicas do projeto **NoFluxoUnB**, consolidando as informações contidas no documento de requisitos (`requisitos.md`) e nos artefatos visuais do repositório (StoryMap, Product Backlog Building - PBB, e notas de atribuição de tarefas).

---

## 1. Mapeamento de Funcionalidades (Visão do Usuário / Histórias de Usuário)

As funcionalidades do sistema estão divididas de acordo com as grandes épicas/temas identificados no StoryMap do projeto:

### 1.1. Módulo: Acesso ao Sistema
Este módulo compreende a porta de entrada do usuário, os mecanismos de autenticação e as políticas de retenção de dados.
* **Home Page & Institucional ("Sobre nós"):**
    * Apresentar ao aluno o propósito do projeto NoFluxoUnB.
    * Fornecer diretrizes de como contribuir com o projeto e apresentar a trajetória de desenvolvimento.
* **Autenticação e Registro:**
    * Permitir que o aluno crie uma conta (registro) e realize o login de forma segura.
* **Acesso Anônimo (Modo Convidado):**
    * Permitir que o usuário acesse e consulte a estrutura curricular geral do curso sem a necessidade de autenticação, sob a premissa/aviso explícito de que nenhuma alteração ou simulação será salva.
* **Armazenamento de Dados Residente:**
    * Garantir que, para usuários autenticados (logados), o sistema armazene de forma persistente o histórico acadêmico enviado e todas as simulações de grade realizadas anteriormente.

### 1.2. Módulo: Envio e Processamento do Histórico Acadêmico
Módulo responsável pela ingestão de dados do aluno e extração de informações consolidadas.
* **Guia de Suporte ao Usuário:**
    * Oferecer auxílio/passo a passo detalhado orientando o aluno sobre como emitir e obter seu arquivo de histórico acadêmico oficial em formato PDF junto à instituição.
* **Upload de Documento:**
    * Disponibilizar interface para upload do arquivo de histórico acadêmico em formato PDF.
* **Leitura Automática e Parsing:**
    * Processar o PDF do histórico para extrair de forma automatizada as disciplinas e classificá-las em: *cursadas*, *aprovadas*, *reprovadas* e *trancadas*.
* **Fluxo Alternativo Sem Histórico:**
    * Garantir a opção de prosseguir no sistema sem efetuar o envio do histórico acadêmico, aplicando restrições automáticas de acesso a ferramentas que dependem exclusivamente desses dados.

### 1.3. Módulo: Consulta e Customização da Estrutura Curricular
Responsável pela renderização interativa do fluxo do curso.
* **Sincronização com Base de Dados:**
    * Consultar a base do curso para obter a árvore de disciplinas, fluxograma oficial e regras de equivalência.
* **Exibição de Fluxograma Personalizado:**
    * Renderizar visualmente o fluxograma de disciplinas do aluno, destacando graficamente o status de cada matéria (cursada, pendente, etc.).
    * Exibir o número de vezes que o aluno cursou ou reprovou em determinada disciplina.
    * Exibir informações de equivalência de disciplinas ao passar o mouse (hover) ou clicar na matéria.
* **Visualização de Grade Geral:**
    * Permitir visualizar e navegar pela estrutura do curso mesmo sem o upload do histórico (permitindo simulações puramente manuais).
* **Alertas de Dependências e Criticidade:**
    * Emitir alertas visuais automáticos sobre disciplinas consideradas "críticas" ou que possuam uma cadeia extensa de pré-requisitos (gargalos).
* **Inclusão de Matérias Optativas:**
    * Oferecer a funcionalidade de pesquisar e adicionar matérias optativas diretamente ao fluxograma visual do aluno.

### 1.4. Módulo: Ferramentas de Progresso e Análise Acadêmica (Analytics)
Conjunto de calculadoras e métricas consolidadas sobre a evolução do estudante.
* **Cálculo de Índices Acadêmicos:**
    * Calcular e exibir em tempo real o IRA (Índice de Rendimento Acadêmico).
    * Calcular e exibir a Média Ponderada do aluno.
* **Módulo de Integralização:**
    * Calcular e exibir a porcentagem exata de conclusão do curso.
    * Contabilizar as horas complementares cumpridas e exibir o saldo de horas faltantes.
    * Exibir a contagem de semestres já cursados e a estimativa de semestres restantes com base no tempo máximo de jubilação do curso.
* **Simulador de Mudança de Curso (Troca de Fluxo):**
    * Permitir que o aluno selecione outro curso da instituição e simule o aproveitamento automático de disciplinas já cursadas, calculando o impacto no novo fluxo.
* **Auditoria de Histórico Oculto:**
    * Identificar e expor o histórico de trancamentos (se o aluno já trancou períodos, a quantidade de vezes e os respectivos semestres).
    * Identificar e expor migrações anteriores de curso (qual era o curso anterior, quando ocorreu a mudança e quais disciplinas foram herdadas/aproveitadas).
* **Exportação de Dados:**
    * Gerar um relatório em PDF contendo o layout limpo e padronizado da simulação atual do fluxograma do aluno.

### 1.5. Módulo: Agente de Inteligência Artificial e Chatbot
Camada inteligente de apoio à decisão do estudante.
* **Recomendação Personalizada de Disciplinas:**
    * Agente de IA integrado que analisa o histórico do aluno, áreas de interesse declaradas e preferências pessoais para sugerir quais disciplinas cursar no próximo período.
* **Interface Direta com o Fluxograma:**
    * Disponibilizar um botão/opção nas recomendações da IA para que o aluno adicione a matéria sugerida diretamente à sua grade simulada com um clique.

---

## 2. Requisitos Não Funcionais (Critérios de Qualidade)

Para garantir o correto funcionamento das funções descritas, o sistema deve obedecer aos seguintes parâmetros técnicos:

* **Responsividade:** Interface adaptável para funcionamento pleno em desktops e dispositivos móveis (smartphones/tablets).
* **Tempo de Resposta (Performance):** Resposta inferior a **5 segundos** para as principais operações: geração da simulação de grade, exibição do fluxograma interactivo, e upload com parsing do histórico.
* **Performance do Parser:** A extração total de dados de arquivos PDF de até 10 páginas deve ocorrer em no máximo **5 segundos**.
* **Acurácia de Dados:** Taxa mínima de precisão de **95%** na extração automatizada de informações textuais do PDF do histórico acadêmico.
* **Segurança e Privacidade:** Autenticação robusta para usuários cadastrados e armazenamento criptografado de dados sensíveis (pessoais e acadêmicos).
* **Compatibilidade:** Operação homologada no navegador Google Chrome.
* **Usabilidade:** Foco em interface limpa, intuitiva e puramente visual, priorizando a organização de fluxogramas complexos.
* **Identidade Visual de Exportação:** Os PDFs gerados pelo sistema devem obrigatoriamente seguir um padrão visual corporativo e limpo, alinhado à identidade do NoFluxoUnB.

---

## 3. Backlog Técnico e Atribuições de Engenharia

Com base nas reuniões de planejamento técnico registradas nos quadros de notas, as seguintes tarefas de infraestrutura, arquitetura e desenvolvimento foram mapeadas e distribuídas entre os membros da equipe:

### ⚙️ Engenharia de Dados e Backend
* **Scraping Automatizado (Arthur):** Implementação de scripts de raspagem de dados para extração de matérias, árvores de equivalência, regras de troca de curso e estruturas curriculares vigentes da UnB.
* **Desenvolvimento do Parser de PDF (Arthur):** Construção das regras de negócio e tratamento de exceções/erros para leitura de PDFs de históricos de alunos, convertendo-os em estruturas limpas de dados (JSON).
* **Modelagem e Estruturação de Banco de Dados (Felipe Pedrosa & Erick):** Desenho do esquema do banco de dados para suportar dados de scraping, usuários e histórico.
* **Automação e Carga de Dados:** Desenvolvimento do pipeline de carga automática de dados (Scraping + Banco) para popular os bancos de dados do **Supabase** e da estrutura do **RAGFlow**.

### 🤖 Inteligência Artificial (Módulo de IA)
* **Modelagem do AI-Agent (Choeiri / Choueri):** Estudos focados na estruturação do agente de IA encarregado de realizar as consultas inteligentes aos Large Language Models (LLMs).
* **Integração RAGFlow & Ollama (Choueri):** Implementação das chamadas de API do RAGFlow dentro da base de código do sistema. Configuração do ecossistema para que o RAGFlow consulte o LLM local/remoto utilizando pesos da IA e infraestrutura baseada em Ollama quando um usuário buscar informações sobre matérias.

### 🎨 Frontend e Prototipagem
* **Prototipagem de Interfaces:** Criação de telas de baixa e alta fidelidade utilizando ferramentas como Figma e Canva.
* **Página de Autenticação:** Construção do Frontend da tela de login do sistema.
* **Página de Fluxograma Interativo (Vitor Trancoso):** Desenvolvimento da tela principal do fluxograma, incluindo a funcionalidade de importação de arquivos.
* **Menu Lateral e Componentes Calculadores (Vini & Gusmão):** Implementação do menu de navegação lateral contendo os cards calculadores de IRA, média ponderada, barra visual de integração do curso, entre outros componentes.

### 🚀 DevOps, Arquitetura e Qualidade
* **Integração Contínua e Deploy (CI/CD):** Configuração automatizada de pipelines de build, teste e deploy através do **GitHub Actions**.
* **Refatoração Arquitetural (Erick):** Simplificação e atualização da arquitetura global do sistema, incluindo o mapeamento e desenho do fluxograma do chatbot.
* **Gestão de Código e Integração (Erick):** Auditoria de ramificações (*branches*), fechamento de frentes de trabalho maduras e conversão destas em *Issues* para integração segura na ramificação principal (`main`).
* **Arquitetura de Software e Documentação (Ramalho):** Estudo e confecção do Diagrama de Pacotes estrutural do software, atualização contínua do arquivo `README.md` com o guia passo a passo de configuração e requisitos para execução do projeto localmente, e atualização dos links dos protótipos de Figma na documentação oficial.
