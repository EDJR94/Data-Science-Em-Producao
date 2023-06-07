# Rossmann Store Sales Prediction
![rossmann](https://github.com/EDJR94/Data-Science-Em-Producao/assets/128603807/982bd982-b6d6-4174-8f87-93063fd96acf)

## 01. Problema de Negócio

A Rossmann opera mais de 3.000 lojas de drogarias em 7 países europeus. As vendas da loja são influenciadas por muitos fatores, incluindo promoções, concorrência, feriados escolares e estaduais, sazonalidade e localização. Atualmente, os gerentes de loja da Rossmann têm a tarefa de prever suas vendas diárias com até seis semanas de antecedência. Com milhares de gerentes individuais prevendo vendas com base em suas circunstâncias únicas, a precisão dos resultados pode ser bastante variada.

Como Cientista de Dados, fui encarregado de, através da Análise da Dados e modelos de Machine Learning, a ajudar a prever essas vendas diárias com 6 semanas de antecedência e reportar o resultado ao CFO através de um Bot no Telegram.

## 02. Premissas

- O conjunto de dados contém as vendas realizadas entre 01/01/2013 e 31/07/2015.
- As variáveis/atributos originais (e seus significados) do conjunto de dados são:

| Atributos | Significado |
| --- | --- |
| store | id único para cada loja |
| day_of_week | dia da semana (1 a 7) |
| date | data |
| sales | o volume financeiro de vendas no dia |
| customers | o número de clientes no dia |
| open | indicador se a loja estava aberta ou não (0 = fechada, 1 = aberta) |
| promo | indica se a loja estava com alguma promoção no dia |
| state_holiday | indica se era feriado estadual/nacional no dia (a = feriado público, b = Páscoa, c = Natal, 0 = nenhum) |
| school_holiday | indica se a loja no dia foi afetada pelo fechamento das escolas públicas |
| store_type | indica o tipo da loja (4 tipos: a, b, c, d) |
| assortment | descreve o nível de mix de produtos (a = básico, b = extra, c = extenso) |
| competition_distance | distância em metros para a loja do concorrente mais próxima |
| competition_open_since_month | mês que a loja do concorrente mais próxima foi aberta |
| competition_open_since_year | ano que a loja do concorrente mais próxima foi aberta |
| promo2 | promoção contínua e consecutiva para algumas lojas (0 = loja não participou, 1 = loja participou) |
| promo2_since_week | indica a semana do ano que a loja começou a participar da promo2 |
| promo2_since_year | indica o ano que a loja começou a participar da promo2 (complementar à promo2_since_week) |
| promo_interval | descreve os intervalos consecutivos que a promo2 começou, indicando os meses que a promoção começou novamente (Ex.: "Feb,May,Aug,Nov" significa que cada intervalo começou em Fevereiro, Maio, Agosto e Novembro em determinado ano para determinada loja) |

## 03. Estratégias de Solução

A estratégia utilizada foi o método CRISP, dividido em 10 partes:

![crisp](https://github.com/EDJR94/pa004_health_insurance/assets/128603807/67b3ae4f-ea88-42e9-9cb4-43eee51cec4a)

1. Questão de Negócio apresentada pelo CFO.
2. Entendimento do Negócio da Rossmann.
3. Coleta de Dados.
4. Limpeza de Dados.
5. Exploração de Dados.
6. Modelagem dos Dados.
7. Utilização de Modelos de Machine Learning.
8. Avaliação do Algoritmo de Machine Learning.
9. Deploy do Modelo em Produção.
10. Bot no Telegram.

## 04. Melhores Insights do Negócio

Foram levantadas as seguintes hipóteses de negócio de acordo com como funcionava o negócio da Rossmann:

1. Lojas com maior sortimentos deveriam vender mais.
2. Lojas com competidores mais próximos deveriam vender menos.
3. Lojas com competidores à mais tempo deveriam vendem mais.
4. Lojas com promoções ativas por mais tempo deveriam vender mais.
5. Lojas com mais promoções consecutivas deveriam vender mais.
6. Lojas abertas durante o feriado de Natal deveriam vender mais.
7.  Lojas deveriam vender mais ao longo dos anos.
8.  Lojas deveriam vender mais no segundo semestre do ano.
9.  Lojas deveriam vender mais depois do dia 10 de cada mês.
10.  Lojas deveriam vender menos aos finais de semana.
11.  Lojas deveriam vender menos durante os feriados escolares.

Dentre as 11 hitóteses, as mais imporantes consideradas por mim foram:

1.  Lojas com competidores a mais tempo deveriam vender mais.

![h1 hipotese](https://github.com/EDJR94/Data-Science-Em-Producao/assets/128603807/100e4719-8fc2-4ed4-8c03-db42674916c6)

Pelo gráfico podemos ver que quanto mais perto da data atual(2015) a loja competidora abre,
mais as lojas das Rossmann vendem. Isso também pode ser visto com a correlação positiva.

2.  Lojas deveriam vender no segundo semestre

![download (2)](https://github.com/EDJR94/Data-Science-Em-Producao/assets/128603807/c6d47e45-684d-48a7-a153-354f68748eb7)

Pelo gráfico podemos ver que as vendas caem significativamente após o mês 6 e com uma correação bem negativa.

3.  Lojas deveriam vender mais depois do dia 10 de cada mês.

![download (3)](https://github.com/EDJR94/Data-Science-Em-Producao/assets/128603807/e68b99ae-b9f4-42d5-ad6b-f775a148f38c)

Pelo gráfico observamos que as lojas vendem de uma forma lateral ao longo dos dias do mês. Não há uma correlação forte entre o dia 
do mês e as vendas.

4.  Vendas deveriam ser menor nos feriados escolares.

![download (4)](https://github.com/EDJR94/Data-Science-Em-Producao/assets/128603807/efeb5c56-7f38-4584-b57c-a70980965fda)

Realmente as vendas são menores nos feriados escolares, porém há um detalhe no mês 7 e 8 que  as vendas se igualam e são maiores.
Provalvemente por causa das férias escolares.

## 05. Machine Learning

Foram usados os seguintes modelos de Machine Learning para analisar a previsão das vendas:

- *Average Model*
- *Linear Regression*
- *Linear Regression Regularized*
- *Random Forest Regressor*
- *XGBoost Regressor*

Após analisar os erros(MAE, MAPE e RMSE) abaixo optei por seguir com o *XGBoost Regressor*. Embora o *Random Forest* tenha apresentado
um valor de erro um pouco melhor, ele tem um tamanho muito maior que o *XGBoost Regressor*.
| Model Name | MAE | MAPE | RMSE |
| --- | --- | --- | --- |
| Random Forest Regressor | 680.854054 | 0.100115 | 1012.687130 |
| XGB Regressor | 868.958205 | 0.130309 | 1238.550843 |
| Average Model | 1354.800353 | 0.206400 | 1835.135542 |
| Linear Regression | 1867.089774 | 0.292694 | 2671.049215 |
| Linear Regression - Lasso | 1891.704881 | 0.289106 | 2744.451741 |

Após aplicar o Cross-Validation, podemos observar na tabela abaixo que os erros estão próximos aos erros aplicados ao dataset de treino acima,
confirmando que o modelo está com uma boa capacidade de generalização.

| Model Name | MAE CV | MAPE CV | RMSE CV |
| --- | --- | --- | --- |
| Random Forest Regressor | 836.83 +/- 217.3 | 0.12 +/- 0.02 | 1255.04 +/- 316.89 |
| XGBoost Regressor | 1060.51 +/- 178.41 | 0.15 +/- 0.02 | 1512.59 +/- 241.37 |
| Linear Regressoion | 2081.73 +/- 295.63 | 0.3 +/- 0.02 | 2952.52 +/- 468.37 |
| Linear Regression - Lasso | 2116.38 +/- 341.5 | 0.29 +/- 0.01 | 3057.75 +/- 504.26 |

Por fim, o modelo final, após ajustado os hiperparâmetros, foi o seguinte:

| Model Name | MAE | MAPE | RMSE |
| --- | --- | --- | --- |
| XGBoost Regressor | 695.985642 | 0.102112 | 1007.379751 |

## 06. Tradução do Modelo para o Negócio
A partir das previsões feitas pelo modelo, podemos traduzir os valores de erro encontrados em valor estimado para o negócio.
Na tabela abaixo estão as previsões feitas pelo modelo considerando o pior e melhor cenário em valor financeiro.

| Scenarios | Values |
| --- | --- |
| prediction | R$ 284,718,336.00 |
| worst_scenario | R$ 283,938,442.77 |
| best_scenario | R$ 285,498,228.15 |

## 07. Bot no Telegram

Após enviar o modelo para produção, fiz um bot no telegram que busca em tempo real a previsão de vendas para a loja desejada:

![rossmann bot](https://user-images.githubusercontent.com/128603807/236702453-dae91759-bd2e-44be-8079-3de5cf56be14.jpg)


## 08. Produto Final e Conclusão

O produto final foi o bot no telegram que pode ser acessado pelo CFO de qualquer dispositivo que possua o Telegram conectado à internet, facilitando a definição do orçamento para a reforma de cada loja, além disso as próprias hipóteses analisadas geraram Insights que podem ser utilizados por ele para aumentar as vendas 

## 09. Próximos Passos

Realizar mais Ciclos do CRISP focando em:

- Testar outros modelos de Machine Learning.
- Preencher os dados faltantes de outra formar.
- Testar outras formas de lidar com os Outliers.
- Utilizas outras estratégias para definir os Hyperparâmetros do modelo.
- Mais opções de consulta no Bot do Telegram.

## Referências

Conjunto de dados: [https://www.kaggle.com/competitions/rossmann-store-sales](https://www.kaggle.com/competitions/rossmann-store-sales)
