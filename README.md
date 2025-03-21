# Azure Cognitive Search: Utilizando AI Search para indexação e consulta de Dados



## Configuração de uma Pesquisa Inteligente com Azure AI Search

Este guia documenta o passo a passo para configurar uma pesquisa inteligente usando o **Azure AI Search**, capaz de extrair, indexar e buscar informações em um repositório de documentos não estruturados, além de apresentar os insights, ferramentas complementares e aprendizados adquiridos durante o processo.

## Passo a Passo da Configuração

### 1. **Criar um Recurso Azure AI Search**
- Acesse o portal do [Azure](https://portal.azure.com/);
- Pesquise por **Azure AI Search**;
- Clique em **Create a resource**;
- Configure:
  - Assinatura;
  - Grupo de recursos;
  - Nome do serviço;
  - Região;
  - Pricing Tier (Básico);
- Finalize clicando em **Review + Create**.
- Após finalizar a criação do recurso, selecione **Ir para o recurso**. Na página de visão geral do Azure AI Search, você pode importar dados, adicionar índices, pesquisar índices criados.

### 2. **Criar um recurso Azure AI services**
- Volte para à página inicial do portal do Azure. Clique no botão **Create a resource** e busque por serviços de IA do Azure. Ao Selecione criar um plano de serviços de IA do Azure você será redirecionado a uma página para criar o recurso.
- Configure:
  - Assinatura;
  - Grupo de recursos;
  - Região;
  - Nome;
  - Pricing Tier (Standard S0);
  - Ao marcar esta caixa, reconheço que li e compreendi todos os termos abaixo;
- Finalize clicando em **Review + Create**.

### 3. **Criar um storage account**
- Retorne à página inicial do Azure e selecione o botão **Create a resource**.
- Pesquise por conta de armazenamento e crie um recurso de conta de armazenamento.
- Configure:
  - Assinatura;
  - Grupo de recursos;
  - Nome da conta de armazenamento;
  - Localização;
  - Desempenho (Standard);
  - Redundância Locally (redundant storage - LRS);
- Finalize clicando em **Review + Create**.
---
### 4. **Preparar e Carregar os Documentos**
- Acesse o **Azure Storage Account**;
- Crie um **Container** público ou com permissões adequadas;
- Faça **Upload** dos arquivos (PDFs, DOCs, TXTs) que serão indexados;
- **Dica:** Estruture bem os documentos para facilitar o reconhecimento de conteúdo.
---
\
\
\
\
\
\
\
\
\
\

### 3. **Configurar o Data Source (Fonte de Dados)**
- No serviço Azure AI Search, acesse **Data Sources**;
- Clique em **+ Add Data Source**;
- Selecione o Blob Storage e a conexão criada;
- Defina o container de documentos;
- Escolha a opção de usar o **Cognitive Skills (AI Enrichment)** se desejar enriquecer os dados com IA (extração de texto, imagens, tradução, etc.).

---

### 4. **Criar o Indexador**
- Vá para **Indexers** e clique em **+ Add Indexer**;
- Configure a periodicidade de indexação;
- Defina o campo `key` (identificador único de cada documento);
- Execute o indexador e monitore o status.

---

### 5. **Definir o Índice de Busca**
- Acesse **Indexes** e clique em **+ Add Index**;
- Estruture os campos extraídos do conteúdo;
- Defina quais campos são:
  - **Searchable** (pesquisáveis);
  - **Retrievable** (retornáveis nas respostas);
  - **Filterable / Sortable / Facetable** (para filtros e organização).

---

### 6. **Executar as Consultas**
- Utilize o portal ou a API REST para fazer buscas;
- Exemplo de query REST:
  ```
  GET https://<search-service-name>.search.windows.net/indexes/<index-name>/docs?search=termo&api-version=2021-04-30-Preview
  ```
- Analise os resultados retornados.

---

## 🔍 Insights e Possibilidades

### 💡 **O que é possível construir com AI Search**
- Buscadores de documentos corporativos;
- Pesquisa semântica em bases jurídicas;
- FAQs dinâmicas automatizadas;
- Ferramentas de suporte ao cliente com recuperação de respostas;
- Análise de dados não estruturados.

### 🧠 **Principais Aprendizados**
- A importância de um bom design de indexação;
- Como a IA pode ser aplicada para extrair e enriquecer dados;
- O poder da pesquisa semântica versus a tradicional por palavra-chave;
- Integração de diversos serviços Azure (Storage, Cognitive Services e Search).

---

## 🧰 Ferramentas que se beneficiam da integração
- **Power BI**: Conectando a uma Search API para criar dashboards inteligentes;
- **Chatbots (Azure Bot Service / Power Virtual Agents)**: Buscando respostas diretamente do índice;
- **Aplicações Web**: Enriquecendo sistemas internos com busca avançada;
- **Sistemas Jurídicos, Saúde e Educação**: Onde o volume de documentos exige pesquisa eficiente.

---

## ✅ Conclusão
O Azure AI Search é uma solução robusta para transformar grandes volumes de dados não estruturados em insights acessíveis. Ao final do processo, foi possível entender desde a preparação dos dados até a realização de consultas otimizadas, percebendo o potencial de combinar IA com mecanismos de busca.

