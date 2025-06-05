# Consultor de Riscos de Empresas - Fluxo n8n

Este repositório contém um fluxo de trabalho (workflow) do n8n projetado para automatizar a análise e definição do risco de empresas. O sistema utiliza informações obtidas através de web scraping e processamento por inteligência artificial para classificar o risco empresarial.

## 🎯 Objetivo do Fluxo

O principal objetivo deste fluxo é fornecer uma avaliação automatizada do nível de risco de uma empresa. Isso é alcançado através da coleta de dados relevantes de fontes online, processamento dessas informações e, em seguida, utilizando um modelo de IA para determinar um perfil de risco. Os resultados são armazenados para referência futura e análise.

## ✨ Como Funciona

O fluxo é orquestrado no n8n e segue as seguintes etapas principais:

1.  **Disparo (Trigger):** O fluxo é iniciado por um `ChatTrigger`
2.  **Coleta de Dados Inicial:**
    * **Entrada Manual/Configuração:** Dados iniciais sobre a empresa podem ser inseridos ou configurados (`Edit Fields`).
    * **Pesquisa Web (SerpApi):** Utiliza o nó `SerpApi` para realizar buscas no Google (google_light) e coletar informações públicas iniciais sobre a empresa.
3.  **Processamento e Coleta Adicional de Dados:**
    * **Divisão de Dados (`SplitOut`):** Os dados coletados podem ser divididos para processamento individual.
    * **Requisições HTTP (`HttpRequest`):** Realiza requisições HTTP utilizando a **API Google Custom Search JSON** para fazer o scraping de informações detalhadas de sites específicos ou para interagir com outras APIs.
4.  **Análise com Inteligência Artificial:**
    * **Modelo de Chat OpenAI (`OpenAIChat` / `AI Agent2`):** As informações consolidadas são enviadas para um modelo de linguagem da OpenAI (GPT) para análise. O modelo é instruído (via prompt) a avaliar o risco da empresa com base nos dados fornecidos.
5.  **Manipulação e Armazenamento de Resultados:**
    * **Edição de Campos (`Edit Fields`):** Os resultados da IA são formatados ou campos adicionais são criados.
    * **Armazenamento em Banco de Dados (Supabase):** O resultado final da análise de risco e os dados relevantes são armazenados em uma tabela no Supabase (`supabase.create_row`).

## 🛠️ Tecnologias Utilizadas

* **n8n.io:** Plataforma de automação de fluxo de trabalho (Workflow Automation).
* **SerpApi:** API para extrair resultados de motores de busca.
* **Google Custom Search JSON API:** Utilizada através do nó `HTTP Request` para scraping de informações específicas de websites.
* **HTTP Request Node (n8n):** Para realizar chamadas a APIs genéricas.
* **OpenAI API:** Para acessar modelos de linguagem avançados (GPT) para análise e interpretação de dados.
* **Supabase:** Plataforma open-source que oferece banco de dados PostgreSQL, autenticação, armazenamento, e APIs.
* **Node.js (ambiente de execução do n8n).**
* **JSON:** Formato de dados para o fluxo n8n e para a troca de informações entre os nós.

## 🚀 Como Usar

1.  **Instância n8n:** Certifique-se de ter uma instância do n8n em execução.
2.  **Importar o Fluxo:**
    * Faça o download do arquivo `Consultor_de_Riscos_de_Empresas.json` deste repositório.
    * No seu painel do n8n, vá para "Workflows" e clique em "Import from File".
    * Selecione o arquivo JSON baixado.
3.  **Configurar Credenciais:**
    * **SerpApi:** Configure as credenciais da API do SerpApi no nó correspondente.
    * **Google Custom Search JSON API:** No nó `HTTP Request` configurado para esta API, certifique-se de que sua chave de API e o ID do mecanismo de pesquisa personalizado (CX) estão corretamente configurados nos parâmetros da URL ou cabeçalhos.
    * **OpenAI:** Configure sua chave de API da OpenAI no nó "AI Agent2" ou "OpenAI Chat Model2".
    * **Supabase:** Configure as credenciais de acesso ao seu projeto Supabase no nó "Supabase".
    * Verifique outros nós que possam requerer configurações específicas.
4.  **Testar e Executar:**
    * Execute o fluxo manualmente para testar cada etapa.
    * Ajuste os prompts do modelo OpenAI e os parâmetros dos nós conforme necessário para otimizar os resultados.

## 📋 Pré-requisitos

* Acesso a uma instância n8n.
* Conta e chave de API válida para SerpApi.
* Conta e chave de API válida para Google Cloud Platform (com a Custom Search JSON API habilitada).
* ID do Mecanismo de Pesquisa Personalizado (CX) do Google.
* Conta e chave de API válida para OpenAI.
* Projeto configurado no Supabase com as tabelas necessárias.
* Conhecimento básico sobre como o n8n funciona e como configurar credenciais e APIs.

## 📄 Licença

Este projeto está licenciado sob a Licença MIT. 
