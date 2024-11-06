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


- **Limpeza de Dados**:
Boa parte da análise se deu por meio do primeiro dataset mencionado em conjunto com os dados do yfinance. Foi feita uma análise de comparação usando o dataset disponível em Kaggle - Public Company ESG Ratings Dataset e a biblioteca yfinance do Python, permitindo analisar e comparar o crescimento do preço na bolsa de valores e os níveis ESG de duas empresas diferentes com base em seus tickers

Enfrentamos diversos desafios ao tentar realizar a fusão entre os dados da biblioteca yfinance e o conjunto de dados ESG. O formato distinto de cada uma das fontes impediu a combinação adequada dos tickers, que representam as siglas das empresas. Além disso, a presença de dados faltantes limitou nossa capacidade de realizar análises abrangentes para todas as empresas que possuem níveis de ESG registrados. 

Como resultado, optamos por utilizar um outro conjunto de dados, o S&P 500 ESG and Stocks Data 2023-24, que ofereceu uma fonte financeira mais completa e coerente, permitindo a fusão das duas bases sem complicações. Apesar dessa mudança, decidimos preservar algumas análises gráficas realizadas com as informações anteriores, uma vez que elas forneceram visualizações valiosas sobre a relação entre os níveis de ESG e os preços das ações no mercado para as empresas analisadas.

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
- **Análise Crítica dos Resultados**:

Mean Squared Error (MSE):

O valor obtido de MSE = 217122.46 indica que, em média, as previsões do modelo de preço estão a uma distância de aproximadamente 467.78 (que é a raiz quadrada do MSE) do valor real. Essa métrica sugere que há uma discrepância significativa entre os preços preditos pelo modelo e os preços reais das ações. Um MSE elevado geralmente aponta que o modelo pode não estar capturando a relação entre as variáveis de entrada (no seu caso, as pontuações ESG) e a variável de saída (o preço das ações) de maneira eficaz.
R-squared (R²):

O valor de R² = 0.0056 indica que apenas cerca de 0.56% da variabilidade nos preços das ações é explicada pelo modelo. Esse valor é extremamente baixo, sugerindo que o modelo não é capaz de explicar a variação dos preços das ações com base nas variáveis selecionadas. Em outras palavras, as pontuações ESG (environmentScore, socialScore, governanceScore e totalEsg) não parecem ter uma relação linear significativa com os preços das ações.

A partir do gráfico de correlação, observamos que realmente, a relação entre essas variáveis de nível ESG e o preço das ações de uma empresa na bolsa ainda não podem ser relacionados - pelo menos sem levar em conta outros tantos fatores.
Com base nos resultados obtidos e obsservando a eficácia do modelo construído, que não apresentou um desempenho satisfatório, como evidenciado pelo MSE elevado e pelo R² baixo: as variáveis utilizadas podem não ser adequadas para prever os preços das ações ou que a relação entre elas não é linear.

Isso mostra a necessidade de explorar outras fontes ou outras variáveis no contexto ESG-finanças no geral, e também evidencia a falta de pesquisas e fontes de dados em torno desse assunto em uma escala maior. Esse tipo de pesquisa sobre os níveis de ESG pode ter grande potencial quando combinado com indicadores financeiros, fatores macroeconômicos ou métricas de desempenho das empresas.
Apesar das várias tentativas de melhoria, o modelo não atingiu um desempenho satisfatório. A baixa capacidade preditiva pode ser atribuída à escolha das variáveis, à natureza dos dados ou à necessidade de modelos mais complexos.
  
Além disso, a análise realizada ao longo deste projeto destacou a dificuldade em obter dados suficientemente aprofundados sobre as ações ESG das empresas, bem como a falta de domínio no campo do mercado financeiro, o que limitou nossa capacidade de conduzir uma análise mais robusta. Os resultados do modelo preditivo indicaram que, apesar dos esforços para ajustar e normalizar os dados, a relação entre as variáveis ESG e os preços das ações não foi suficientemente elucidativa. Essa experiência ressalta a importância de continuar a pesquisa em busca de fontes de dados mais abrangentes e confiáveis, que permitam uma compreensão mais profunda das dinâmicas entre os desempenhos ESG e o comportamento do mercado financeiro..

## Inferimentos
Reflexões, aprendizados e ideias para a continuidade do projeto:

**1. Incluir Variáveis Financeiras Complementares**
  
Acrescentar dados financeiros e operacionais além do preço das ações, como EBITDA, dívida líquida, fluxo de caixa e lucro por ação (EPS), que podem ter uma correlação mais forte com o valor das ações e dar ao modelo uma base mais ampla para capturar relações.
Incluir métricas de volatilidade, liquidez e volume de negociação, que oferecem um panorama mais robusto sobre o comportamento de uma ação no mercado.

**2. Enriquecer as Variáveis ESG com Subcategorias e Dados de Impacto Regional**

Incorporar subcategorias mais específicas dentro de cada pilar ESG (ambiental, social e governança) para observar o impacto de fatores granulares, como “emissões de carbono” ou “diversidade no conselho administrativo”.
Trazer dados de impacto regional ou local, especialmente para empresas globais, já que questões ambientais e sociais podem variar muito entre as regiões em que uma empresa opera.

**3. Análise Temporal e Projeções de ESG**

Analisar a evolução dos scores ESG ao longo dos anos para entender como mudanças nesses índices influenciam o preço da ação em diferentes períodos. Essa abordagem permitiria observar não apenas o score ESG atual, mas também como uma melhoria ou piora no score pode impactar o mercado.
Implementar uma modelagem de séries temporais para previsão de ESG e impacto no preço das ações, utilizando modelos de Long Short-Term Memory (LSTM) ou Prophet, por exemplo.

**4. Explorar Interações com Eventos Externos e Setoriais**

Incluir dados sobre eventos de mercado e setoriais (por exemplo, regulamentações ambientais, crises de reputação, desastres ambientais) para modelar o impacto desses eventos em empresas com diferentes níveis de ESG.
Analisar também os efeitos de padrões e normas de ESG para cada setor, o que pode ajudar a entender o que “bom desempenho ESG” representa em indústrias específicas.

**5. Desenvolvimento de uma Base de Dados ESG Proprietária**

Coleta e Pesquisa de Dados Primários: Realizar pesquisas que coletam dados primários diretamente das empresas, incluindo detalhes mais específicos sobre práticas de ESG que não estão em datasets públicos. Por exemplo, informações sobre práticas de sustentabilidade em cadeias de fornecimento, políticas internas de bem-estar, ações concretas de diversidade e inclusão, e iniciativas de inovação ecológica.
Feedback do Consumidor e de Stakeholders: 

Criar uma base de dados que inclua não só a visão da empresa sobre suas práticas ESG, mas também percepções do público e de stakeholders. Isso poderia ser feito por meio de pesquisas, questionários de satisfação e plataformas de feedback.

Integração com Dados Públicos e Governamentais: Consolidar dados abertos e de políticas ESG de fontes governamentais e reguladoras em um formato padronizado, permitindo cruzamento com dados financeiros e operacionais.


## Conclusão
A longo prazo, a criação de uma base de dados mais detalhada e com coleta ativa, complementada por dados financeiros avançados, forneceria uma base sólida para análises ESG profundas e predições precisas. Além de tornar a modelagem mais robusta, essa base de dados poderia se tornar uma fonte confiável para acadêmicos, investidores e stakeholders interessados em ESG, contribuindo para a conscientização e transformação das práticas de mercado.
