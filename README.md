# Rossmann Store Sales Prediction

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

1. Lojas deveriam vender mais ao longo dos anos.
2.  Lojas deveriam vender mais no segundo semestre do ano.
3.  Lojas deveriam vender mais depois do dia 10 de cada mês.
4.  Lojas deveriam vender menos aos finais de semana.

## 05. Machine Learning

Foram usados os seguintes modelos de Machine Learning para analisar a previsão das vendas:

- *Average Model*
- *Linear Regression*
- *Linear Regression Regularized*
- *Random Forest Regressor*
- *XGBoost Regressor*

Após analisar os erros(MAE, MAPE e RMSE) optei por seguir com o *XGBoost Regressor.* Ao ajustar os hyperparâmetros e traduzir o erro em resultado para o negócio, os resultados financeiros total para todas as lojas nas próximas 6 semanas foram os seguintes:

| Cenário | Valores |
| --- | --- |
| Predição | R$ 284,718,336.00 |
| Pior Cenário | R$ 283,938,442.77 |
| Melhor Cenário | R$ 285,498,228.15 |

## 06. Bot no Telegram

Após enviar o modelo para produção, fiz um bot no telegram que busca em tempo real a previsão de vendas para a loja desejada:

![rossmann bot.jpg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e0818c53-27d9-4a10-874b-22e3913f0a0f/rossmann_bot.jpg)

## 07. Produto Final e Conclusão

O produto final foi o bot no telegram que pode ser acessado pelo CFO de qualquer dispositivo que possua o Telegram conectado à internet, facilitando a definição do orçamento para a reforma de cada loja, além disso as próprias hipóteses analisadas geraram Insights que podem ser utilizados por ele para aumentar as vendas 

## 08. Próximos Passos

Realizar mais Ciclos do CRISP focando em:

- Testar outros modelos de Machine Learning.
- Preencher os dados faltantes de outra formar.
- Testar outras formas de lidar com os Outliers.
- Utilizas outras estratégias para definir os Hyperparâmetros do modelo.
- Mais opções de consulta no Bot do Telegram.

## Referências

Conjunto de dados: [https://www.kaggle.com/competitions/rossmann-store-sales](https://www.kaggle.com/competitions/rossmann-store-sales)
