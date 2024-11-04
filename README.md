# Documentação do Projeto de Previsão de Preço de Ações com Base em Dados ESG

## Introdução
Este projeto tem como objetivo criar um modelo preditivo para estimar o preço das ações de empresas, utilizando variáveis relacionadas ao desempenho ambiental, social e de governança (ESG). O modelo foi desenvolvido a partir de um conjunto de dados que inclui pontuações ESG e informações financeiras de diversas empresas.

## Etapas do Projeto

### 1. Coleta e Preparação de Dados
- **Datasets Utilizados**:
- Public Company ESG Ratings Dataset
ESG ratings for over 700 mid / large-cap companies across various industries
(dataset https://www.kaggle.com/datasets/alistairking/public-company-esg-ratings-dataset),
contendo: 'data.csv'

-biblioteca yfinance do Python: permite a extração de dados financeiros de várias fontes, como Yahoo Finance

- S&P 500 ESG and Stocks Data 2023-24
The ESG and Stocks data of S&P 500 Constituent Companies
(https://www.kaggle.com/datasets/rikinzala/s-and-p-500-esg-and-stocks-data-2023-24/data?select=sp500_esg_data.csv),
contendo: 'sp500_esg_data.csv' e 'sp500_price_data.csv'

, que contém registros de várias empresas, representadas pela coluna `Symbol`, junto com suas respectivas pontuações ESG e preços de ações. Adicionalmente, foi feita uma análise de comparação usando o dataset disponível em Kaggle - Public Company ESG Ratings Dataset e a biblioteca yfinance do Python, permitindo analisar e comparar o crescimento do preço na bolsa de valores e os níveis ESG de duas empresas diferentes com base em seus tickers.


- **Limpeza de Dados**:
Boa parte da análise de deu por meio do primeiro dataset mencionado em relação aos dados do yfinance. Após tentativas de normalizar os os dados de ambas as fontes,  mantendo apenas um registro por empresa, selecionando aquele com o valor máximo na coluna `Price`.

Enfrentamos diversos desafios ao tentar realizar a fusão entre os dados da biblioteca yfinance e o conjunto de dados ESG. O formato distinto de cada uma das fontes impediu a combinação adequada dos tickers, que representam as siglas das empresas. Além disso, a presença de dados faltantes limitou nossa capacidade de realizar análises abrangentes para todas as empresas que possuem níveis de ESG registrados. 

Como resultado, optamos por utilizar um outro conjunto de dados, que ofereceu uma fonte financeira mais completa e coerente, permitindo a fusão das duas bases sem complicações. Apesar dessa mudança, decidimos preservar algumas análises gráficas realizadas com as informações anteriores, uma vez que elas forneceram visualizações valiosas sobre a relação entre os níveis de ESG e os preços das ações no mercado para as empresas analisadas.

### 2. Análise Inicial
**Primeiras Análises**
-Exploração de Dados: valore nulos, duplicados, formato de ambas as fontes de dados

- Gráfico de Correlação:
Investimento: Para investidores, entender a correlação pode ajudar na diversificação da carteira. Se as ações são altamente correlacionadas, adicionar ambas à carteira pode não reduzir o risco, pois elas tendem a se mover juntas.
Análise de Risco: Se uma dessas empresas está exposta a um risco específico (por exemplo, mudanças na regulamentação de entretenimento), a outra pode ser afetada também, dado que elas têm uma correlação positiva.
Estratégias de Trading: Traders podem usar a correlação para identificar pares de ações que se comportam de maneira semelhante e podem ser negociados em conjunto, aproveitando as variações de preços relativas.

- Comparação entre duas empresas:
Analisando os níveis ESG de duas empresas por meio de seus ticker em input e tentando estabelecer relações entre os índices ESG em gráfico de barras
e o crescimento do preço das ações em gráfico de linhas

**Segunda Análise**:
- Exploração de dados: Foi realizada uma análise exploratória para entender a distribuição das variáveis e suas correlações. Observou-se que as variáveis ESG estavam em escalas diferentes do preço das ações (`Price`), levando a uma investigação sobre a normalização e padronização dos dados.
- Matriz de Correlação Geral: Para identificar a relação entre todas as variáveis no dataset de ESG, ajudando a entender quais variáveis poderiam ter uma correlação mais forte com o preço das ações.

### 3. Modelagem Preditiva
- **Modelos Utilizados**: O modelo inicial foi uma regressão linear simples com `totalScore` como variável independente. O desempenho deste modelo resultou em um R² de aproximadamente -0.01, indicando que a regressão não era capaz de explicar a variabilidade do preço.

#### 3.1. Desempenho do Modelo
- **Resultado da Regressão Linear**:
  - Mean Squared Error (MSE): 2.694795355710738
  - R-squared (R²): -0.013862603555042874

- **Análise do Desempenho**:
O modelo demonstrou um desempenho insatisfatório, com um MSE elevado e um R² negativo, sugerindo que a relação entre as variáveis não era linear ou que outras variáveis poderiam ser necessárias.

### 4. Inclusão de Variáveis Adicionais
- **Extensão do Modelo**:
O modelo foi reavaliado com a inclusão das variáveis `environmentScore`, `socialScore` e `governanceScore`. No entanto, os resultados continuaram a mostrar um R² baixo, com um MSE de 220272.06604748874 e um R² de -0.008781657556710343.

### 5. Ajuste dos Dados
- **Normalização dos Dados**:
Como os preços estavam em uma escala significativamente maior que as pontuações ESG, foram realizadas transformações nos dados para trazer as variáveis para escalas mais proporcionais. **Essa etapa foi crítica para melhorar a capacidade preditiva do modelo.**

### 6. Avaliação Final do Modelo
- **Modelo com Variáveis Ajustadas**:
Após a normalização e inclusão das quatro variáveis ESG, o modelo foi reavaliado. O resultado foi um MSE de 217122.45860766654 e um R² de 0.005642623609798503, indicando leve melhoria, mas ainda insuficiente para um modelo preditivo eficaz.

## Conclusões e Próximos Passos
- **Análise Crítica**:
Apesar das várias tentativas de melhoria, o modelo não atingiu um desempenho satisfatório. A baixa capacidade preditiva pode ser atribuída à escolha das variáveis, à natureza dos dados ou à necessidade de modelos mais complexos.
  
Além disso, a análise realizada ao longo deste projeto destacou a dificuldade em obter dados suficientemente aprofundados sobre as ações ESG das empresas, bem como a falta de domínio no campo do mercado financeiro, o que limitou nossa capacidade de conduzir uma análise mais robusta. Os resultados do modelo preditivo indicaram que, apesar dos esforços para ajustar e normalizar os dados, a relação entre as variáveis ESG e os preços das ações não foi suficientemente elucidativa. Essa experiência ressalta a importância de continuar a pesquisa em busca de fontes de dados mais abrangentes e confiáveis, que permitam uma compreensão mais profunda das dinâmicas entre os desempenhos ESG e o comportamento do mercado financeiro. O conhecimento adquirido neste projeto servirá como base para futuras investigações, visando aprimorar as análises e a interpretação dos impactos ESG no valor das ações.
