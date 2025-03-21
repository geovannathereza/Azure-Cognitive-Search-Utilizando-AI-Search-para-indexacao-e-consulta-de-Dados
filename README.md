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

### 5. Configuração do Índice e indexação dos documentos
#### Após armazenar os documentos, você pode utilizar o Azure AI Search para obter insights deles. O portal do Azure oferece um assistente para importar dados. Com esse assistente, é possível criar automaticamente um índice e indexador para fontes de dados compatíveis. Você usará esse assistente para criar o índice e transferir seus documentos de pesquisa do armazenamento para o índice do Azure AI Search.
- No portal do Azure, navegue até seu recurso do Azure AI Search. Na página Visão geral, selecione **Import data**.
- Na página Conectar aos seus dados, na lista Fonte de dados, selecione **Azure Blob Storage**. Preencha os detalhes do armazenamento de dados com os seguintes valores:
  - Fonte de dados (Azure Blob Storage);
  - Nome da fonte de dados;
  - Dados para extrair;
  - Modo de análise;
  - Sequência de conexão (Opte por **Choose an existing connection**. Selecione sua conta de armazenamento, selecione o contêiner que criou e clique em **Select**);
  - Autenticação de identidade gerenciada;
  - Nome do contêiner;
  - Pasta Blob;
  - Descrição;
- Selecione **Next: Add cognitive skills (Optional)**.
- Na seção **Attach AI Services**, selecione seu recurso de serviços de IA do Azure.
- Na seção **Add enrichments**:
  - Altere o nome do conjunto de habilidades.
  - Marque a caixa **Enable OCR** e mescle todo o texto no campo **merged_content**.
  - **Nota**: É importante habilitar o **Enable OCR** para ver todas as opções de campos enriquecidos.
  - Defina o campo **Source data** como **merged_content**.
  - Altere o nível de granularidade do aprimoramento para **Pages** (blocos de 5000 caracteres).
  - Não selecione **Enable incremental enrichment**.
  - Selecione os seguintes campos enriquecidos:\
     **Extrair nomes de localizações → "locations"\
     Extrair frases-chave → "keyphrases"\
     Detectar sentimento → "sentiment"\
     Gerar tags a partir de imagens → "imageTags"\
     Gerar legendas a partir de imagens → "imageCaption"**
- Em **Save enrichments to a knowledge store**, selecione:
   - Projeções de imagem
   - Documentos
   - Páginas
   - Frases-chave
   - Entidades
   - Detalhes da imagem
   - Referências de imagem
- Escolha **Choose an existing connection**: Selecione a conexão já criada e o armazenamento de dados que você criou anteriormente.
- Clique em **+ Container**, crie um container chamado **knowledge-store** e defina o nível de privacidade como **Private**. Em seguida, clique em **Create**.
- Selecione o container **knowledge-store** e clique em **Select**.
- Selecione **Azure blob projections: Document**. O nome do container será preenchido automaticamente. Não altere o nome do container.
- Clique em **Next: Customize target index** e altere o nome do índice para **coffee-index**.
- Defina o **Key** como **metadata_storage_path** e deixe o **Suggester name** em branco.
- Marque a opção **filterable** para os campos: content, locations, keyphrases, sentiment, merged_content, text, layoutText, imageTags, imageCaption.
- Clique em **Next: Create an indexer**, altere o nome e mantenha o **Schedule** como **Once**.
- Expanda as **Advanced options** e marque a opção **Base-64 Encode Keys**.
- Clique em **Submit** para criar o recurso, skillset, índice e indexador. O indexador será executado automaticamente.
- Na página do recurso Azure AI Search, vá até **Search Management** e selecione **Indexers**. Clique no indexer criado e, logo depois, clique em **Refresh** até o status indicar sucesso.
- Clique no nome do indexador para ver mais detalhes.



