# Configuração do Azure Machine Learning Workspace

Para começar a utilizar o Azure Machine Learning, é necessário criar um espaço de trabalho do Azure Machine Learning na sua subscrição do Azure. Este guia irá orientá-lo através do processo de criação do espaço de trabalho e execução de um trabalho de aprendizado de máquina automatizado.

### Passo 1: Criar um Espaço de Trabalho

1. Acesse o portal do Azure em [https://portal.azure.com](https://portal.azure.com) utilizando suas credenciais da Microsoft.
2. Selecione "+ Criar um recurso" e pesquise por "Machine Learning".
3. Crie um novo recurso do Azure Machine Learning com as seguintes configurações:
   - **Assinatura**: Sua assinatura do Azure.
   - **Grupo de recursos**: Crie ou selecione um grupo de recursos.
   - **Nome**: Insira um nome exclusivo para seu espaço de trabalho.
   - **Região**: Selecione a região geográfica mais próxima.
   - **Conta de armazenamento**: Observe a nova conta de armazenamento padrão que será criada para seu espaço de trabalho.
   - **Cofre de chaves**: Observe o novo cofre de chaves padrão que será criado para seu espaço de trabalho.
   - **Insights de aplicativo**: Observe o novo recurso padrão de insights de aplicativo que será criado para seu espaço de trabalho.
   - **Registro de contêiner**: Nenhum (um será criado automaticamente na primeira vez que você implantar um modelo em um contêiner).
4. Selecione "Revisar + criar" e, em seguida, "Criar". Aguarde a criação do seu espaço de trabalho.
5. Após a criação, vá para o recurso implantado e selecione "Launch Studio" (ou abra uma nova guia do navegador e navegue até [https://ml.azure.com](https://ml.azure.com)) e entre no Azure Machine Learning Studio usando sua conta da Microsoft.

### Passo 2: Configurar Aprendizado de Máquina Automatizado

1. No Azure Machine Learning Studio, vá para a página "Automated ML" (em Authoring).
2. Crie um novo trabalho de ML automatizado com as seguintes configurações, usando "Next" conforme necessário para avançar pela interface do usuário.
   - **Configurações Básicas**:
     - **Nome do trabalho**: mslearn-bike-automl
     - **Novo nome do experimento**: mslearn-bike-rental
     - **Descrição**: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
     - **Marcadores**: Nenhum
   - **Tipo de Tarefa e Dados**:
### Passo Adicional: Configurar Conjunto de Dados

- **Selecione o tipo de tarefa**: Regressão
- **Selecionar conjunto de dados**: Crie um novo conjunto de dados com as seguintes configurações:
   - **Tipo de dados**:
     - **Nome**: aluguel de bicicletas
     - **Descrição**: dados históricos de aluguel de bicicletas
     - **Tipo**: Tabular
   - **Fonte de dados**:
     - Selecione "Dos arquivos da web"
     - **URL da Web**: [https://aka.ms/bike-rentals](https://aka.ms/bike-rentals)
     - Ignorar validação de dados: não selecionar
   - **Configurações**:
     - **Formato de arquivo**: Delimitado
     - **Delimitador**: Vírgula
     - **Codificação**: UTF-8
     - **Cabeçalhos de coluna**: apenas o primeiro arquivo possui cabeçalhos
     - **Pular linhas**: Nenhum
     - **O conjunto de dados contém dados multilinhas**: não selecione
   - **Esquema**:
     - Incluir todas as colunas exceto Caminho
     - Revise os tipos detectados automaticamente
3. Selecione "Criar". Após a criação do conjunto de dados, selecione o conjunto de dados de aluguel de bicicletas para continuar a enviar o trabalho de ML automatizado.


### Passo 3: Avaliar o Melhor Modelo

1. Na guia "Visão geral do trabalho automatizado de aprendizado de máquina", observe o melhor resumo do modelo.
2. Selecione o texto em "Nome do algoritmo" do melhor modelo para visualizar seus detalhes.
3. Selecione a guia "Métricas" e analise os gráficos residuais e predito_true.

### Passo 4: Implantar e Testar o Modelo

1. Na guia "Modelo" do melhor modelo treinado, selecione "Implantar" e use a opção de serviço Web para implantar o modelo com as configurações fornecidas.
2. Aguarde o início da implantação e certifique-se de que o status mude para "Succeeded".
3. Teste o serviço implantado conforme descrito nas instruções.

```json
{
  "Inputs": { 
    "data": [
      {
        "day": 9,
        "mnth": 4,   
        "year": 2024,
        "season": 2,
        "holiday": 0,
        "weekday": 1,
        "workingday": 1,
        "weathersit": 2, 
        "temp": 0.3, 
        "atemp": 0.3,
        "hum": 0.3,
        "windspeed": 0.3 
      }
    ]    
  },   
  "GlobalParameters": 1.0
}
```

```json
{
  "Results":[
    434.79053792809304
  ]
}
```

### Limpeza

Para evitar custos desnecessários, siga as instruções para excluir o serviço web e o espaço de trabalho do Azure Machine Learning após concluir suas atividades. Certifique-se de salvar quaisquer dados ou resultados importantes antes de prosseguir com a exclusão.

- Exclua o serviço web na guia "Endpoints" do Azure Machine Learning Studio.
- Para excluir o espaço de trabalho, acesse o portal Azure, vá para a página Grupos de Recursos, abra o grupo de recursos do seu espaço de trabalho e selecione "Excluir grupo de recursos".

Lembre-se de que a exclusão de recursos é irreversível e pode resultar na perda permanente de dados. Certifique-se de realizar backups, se necessário.
