# Projeto de Previsão de Vendas

## Descrição do Projeto

Este projeto visa prever as vendas futuras para otimização de estoque e logística. Utilizamos dados históricos de vendas para criar modelos de previsão que ajudam na gestão do inventário e melhoram a eficiência operacional.

## Coleta de Dados

A coleta de dados é realizada a partir de um arquivo CSV contendo informações sobre vendas, temperatura, e eventos especiais. O arquivo CSV inclui as seguintes colunas:

- **Store**: Identificador da loja
- **Dept**: Identificador do departamento
- **Date**: Data da venda
- **Weekly_Sales**: Vendas semanais
- **IsHoliday**: Indica se é um feriado
- **Temperature**: Temperatura
- **Fuel_Price**: Preço do combustível
- **MarkDown1 a MarkDown5**: Descontos
- **CPI**: Índice de preços ao consumidor
- **Population**: População
- **Unemployment**: Taxa de desemprego
- **Type**: Tipo de loja
- **Size**: Tamanho da loja
- **Super_Bowl**: Indicador do Super Bowl
- **Labor_Day**: Indicador do Dia do Trabalho
- **Thanksgiving**: Indicador do Dia de Ação de Graças
- **Christmas**: Indicador do Natal

Os dados são carregados e preparados para análise e modelagem.

## Modelagem

### 1. Preparação dos Dados

Os dados são carregados e renomeados para facilitar o manuseio. Colunas irrelevantes, como 'preço do combustível', 'população', e 'cpi', são excluídas. A coluna 'vendas semanais' é convertida para 'vendas em mil' para simplificar a análise.

### 2. Visualização de Dados

- **Vendas Mensais**: Gráficos de linha e heatmaps são usados para visualizar a evolução das vendas ao longo do tempo.
- **Correlação Entre Vendas e Temperatura**: Gráficos de dispersão mostram a relação entre vendas e temperatura.
- **Comparação de Vendas em Dias de Evento**: Gráficos de barras comparam vendas em dias de eventos especiais e dias normais.

### 3. Regressão Linear

Um modelo de regressão linear é treinado para prever vendas futuras com base em variáveis preditoras como temperatura e eventos especiais. O desempenho do modelo é avaliado utilizando métricas como RMSE.

```python
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import mean_squared_error
import numpy as np

# Preparação dos dados
X = data_reduzida.drop(columns='vendas_em_mil')
y = data_reduzida['vendas_em_mil']

# Divisão dos dados
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Treinamento do modelo
modelo = LinearRegression()
modelo.fit(X_train_scaled, y_train)

# Previsões e avaliação
y_pred = modelo.predict(X_test_scaled)
mse = mean_squared_error(y_test, y_pred)
rmse = np.sqrt(mse)
print("RMSE:", rmse)
