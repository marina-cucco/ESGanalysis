# Documentação do Projeto de Previsão de Preço de Ações com Base em Dados ESG

## Introdução
Este projeto tem como objetivo criar um modelo preditivo para estimar o preço das ações de empresas, utilizando variáveis relacionadas ao desempenho ambiental, social e de governança (ESG). O modelo foi desenvolvido a partir de um conjunto de dados que inclui pontuações ESG e informações financeiras de diversas empresas.

## Etapas do Projeto

### 1. Coleta e Preparação de Dados
- **Datasets Utilizados**: Os dados foram combinados em um DataFrame chamado `merged_df`, que contém registros de várias empresas, representadas pela coluna `Symbol`, junto com suas respectivas pontuações ESG e preços de ações. Adicionalmente, foi feita uma análise de comparação usando o dataset disponível em Kaggle - Public Company ESG Ratings Dataset e a biblioteca yfinance do Python, permitindo analisar e comparar o crescimento do preço na bolsa de valores e os níveis ESG de duas empresas diferentes com base em seus tickers.
- **Limpeza de Dados**: Durante a análise, foram identificados e tratados problemas como valores nulos e duplicados. O DataFrame foi reduzido para `merged_df_unique`, mantendo apenas um registro por empresa, selecionando aquele com o valor máximo na coluna `Price`.

### 2. Análise Inicial
- **Exploração de Dados**: Foi realizada uma análise exploratória para entender a distribuição das variáveis e suas correlações. Observou-se que as variáveis ESG estavam em escalas diferentes do preço das ações (`Price`), levando a uma investigação sobre a normalização e padronização dos dados.
- **Análise de Matriz de Correlação**: Foi feita uma análise de matriz de correlação para identificar a relação entre as variáveis no dataset, ajudando a entender quais variáveis poderiam ter uma correlação mais forte com o preço das ações.

### 3. Modelagem Preditiva
- **Modelos Utilizados**: O modelo inicial foi uma regressão linear simples com `total_score` como variável independente. O desempenho deste modelo resultou em um R² de aproximadamente -0.01, indicando que a regressão não era capaz de explicar a variabilidade do preço.

#### 3.1. Desempenho do Modelo
- **Resultado da Regressão Linear**:
  - Mean Squared Error (MSE): 2.694795355710738
  - R-squared (R²): -0.013862603555042874
- **Análise do Desempenho**: O modelo demonstrou um desempenho insatisfatório, com um MSE elevado e um R² negativo, sugerindo que a relação entre as variáveis não era linear ou que outras variáveis poderiam ser necessárias.

### 4. Inclusão de Variáveis Adicionais
- **Extensão do Modelo**: O modelo foi reavaliado com a inclusão das variáveis `environmentScore`, `socialScore` e `governanceScore`. No entanto, os resultados continuaram a mostrar um R² baixo, com um MSE de 220272.06604748874 e um R² de -0.008781657556710343.

### 5. Ajuste dos Dados
- **Normalização dos Dados**: Como os preços estavam em uma escala significativamente maior que as pontuações ESG, foram realizadas transformações nos dados para trazer as variáveis para escalas mais proporcionais. Essa etapa foi crítica para melhorar a capacidade preditiva do modelo.

### 6. Avaliação Final do Modelo
- **Modelo com Variáveis Ajustadas**: Após a normalização e inclusão das quatro variáveis ESG, o modelo foi reavaliado. O resultado foi um MSE de 217122.45860766654 e um R² de 0.005642623609798503, indicando leve melhoria, mas ainda insuficiente para um modelo preditivo eficaz.

## Conclusões e Próximos Passos
- **Análise Crítica**: Apesar das várias tentativas de melhoria, o modelo não atingiu um desempenho satisfatório. A baixa capacidade preditiva pode ser atribuída à escolha das variáveis, à natureza dos dados ou à necessidade de modelos mais complexos.

### Recomendações:
- Considerar a utilização de modelos mais avançados, como regressão de árvore de decisão, florestas aleatórias ou redes neurais, que podem capturar melhor a complexidade dos dados.
- Explorar a inclusão de variáveis adicionais que possam impactar o preço das ações, como indicadores financeiros e de mercado.
- Realizar uma análise de correlação mais aprofundada para identificar quais variáveis têm mais impacto no preço.
