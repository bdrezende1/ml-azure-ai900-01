# ml-azure-ai900-01
# Aplicar implementações e soluções escaláveis de aprendizado de máquina na nuvem da Microsoft.

------------------------------------------------------------------------------------------------

```markdown
## Passo a Passo do Laboratório de Aprendizado de Máquina do Azure

### 1. Introdução ao Laboratório

Vou criar, treinar e implantar um modelo de aprendizado de máquina usando o Azure Machine Learning. Este laboratório me guiará em cada etapa do processo, desde a configuração do ambiente até a geração de previsões.

### 2. Configurando o Ambiente de Trabalho

#### 2.1 Criar uma Conta no Azure
- Primeiro, criei uma conta no [site do Azure](https://azure.microsoft.com/). Foi necessário completar o processo de inscrição e usar um cartão de crédito para verificação.

#### 2.2 Acessar o Portal do Azure
- Acessei o [Portal do Azure](https://portal.azure.com/) para gerenciar todos os recursos necessários. Familiarizei-me com a interface para facilitar o uso dos serviços.

#### 2.3 Criar um Workspace do Azure Machine Learning
- No Portal do Azure, cliquei em "Criar um recurso" e procurei por "Machine Learning".
- Selecionei "Machine Learning" e cliquei em "Criar".
- Preenchi as informações necessárias, como Nome, Região, Grupo de Recursos e Detalhes de Instância.
- Finalmente, cliquei em "Revisar + Criar" e depois em "Criar" para provisionar meu workspace.

### 3. Preparando os Dados

#### 3.1 Carregar Dados para o Workspace
- Naveguei até a seção "Datastores" no meu workspace e cliquei em "Criar".
- Adicionei um nome e selecionei o tipo de armazenamento, usando o Azure Blob Storage.
- Carreguei o arquivo de dados para o Datastore.

#### 3.2 Registrar o Conjunto de Dados
- No menu lateral, fui para "Datasets" e cliquei em "Novo Dataset".
- Selecionei "From datastore" e escolhi o arquivo que carreguei.
- Preenchi as informações do dataset e cliquei em "Registrar".

### 4. Criando e Treinando o Modelo

#### 4.1 Criar um Experimento
- No workspace, fui para a seção "Experiments" e cliquei em "Novo Experimento".
- Dei um nome ao experimento e selecionei o script que usei para treinamento.

#### 4.2 Escrever o Script de Treinamento
- No editor de scripts, escrevi o código para treinar meu modelo. Usei Python e a biblioteca Scikit-learn para criar um modelo de regressão linear.

```python
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error
import pandas as pd

# Carregar dados
data = pd.read_csv('path_to_your_dataset.csv')
X = data.drop('target_column', axis=1)
y = data['target_column']

# Dividir dados em treino e teste
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Treinar modelo
model = LinearRegression()
model.fit(X_train, y_train)

# Avaliar modelo
predictions = model.predict(X_test)
mse = mean_squared_error(y_test, predictions)
print(f'Mean Squared Error: {mse}')
```

#### 4.3 Executar o Experimento
- Subi o script para o workspace e executei o experimento.
- Acompanhei a execução no portal do Azure Machine Learning, observando logs e métricas sendo atualizados em tempo real.

### 5. Implantando o Modelo

#### 5.1 Criar um Serviço de Inferência
- Após treinar e avaliar meu modelo, o próximo passo foi implantá-lo para previsões.
- No workspace, fui para a seção "Endpoints" e cliquei em "Novo Endpoint".
- Selecionei "Real-time endpoint" e segui os passos para criar e configurar o serviço.

#### 5.2 Implementar o Modelo para o Endpoint
- Conectei o modelo treinado ao endpoint.
- Configurei as dependências e o script de entrada para garantir que o endpoint pudesse receber e processar dados de entrada corretamente.

### 6. Fazendo Previsões com o Modelo Implantado

#### 6.1 Testar o Endpoint
- Usei o endpoint configurado para enviar dados de teste e receber previsões.
- No portal do Azure Machine Learning, testei o endpoint manualmente e também programaticamente usando um script Python.

```python
import requests
import json

# URL do endpoint
url = "https://your-endpoint-url"

# Dados de teste
data = {"data": [{"feature1": value1, "feature2": value2}]}

# Cabeçalhos da solicitação
headers = {"Content-Type": "application/json"}

# Enviar solicitação POST
response = requests.post(url, data=json.dumps(data), headers=headers)

# Exibir previsões
print(response.json())
```
