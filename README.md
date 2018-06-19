# Wine Quality Modeling

Respostas às perguntas propostas:

#### a. Como foi a definição da sua estratégia de modelagem?

1. Foi feito um pré processamento dados no pandas garantindo consistência na leitura do csv. Após examinar as distribuições das variáveis individualmente e em conjunto, foi feita uma inputação de missings para o campo 'alcohol' utilizando uma regressão. Também foi feita uma correção no campo 'density'. Finalmente, após a normalização dos campos, os dados pré processados foram armazenados em um pkl.

2. Para obter um baseline de performance, foi feito uma  regressão teste (sem otimização). Analisando a distribuição dos erros de acordo com a resposta "quality", nota-se que devido ao pouco volume de amostras para os valores 3, 4, 8 e 9. O erro da regressão era muito mais alto nos extremos do que nos valores próximos da média. De fato, no gráfico de ordenação por nota: realizado x previsto de 'quality' vê-se claramente que o estimador joga as previsões para a média.

3. Para lidar com o baixo volume de amostras nos extremos de 'quality', foi feita uma reamostragem, na amostra de treino, sendo que na amostra final, todos os valores de 'quality' têm o mesmo número de ocorrências.

4. Foram introduzidas features polinomiais para que no modelo houvesse interações entre features.

5. Foram testadas algumas técnicas (Gradient Boosting, Lasso, KNN...) e foi feita uma validação cruzada, com amostras extratificadas pelo campo resposta, para uma melhor aferição de qual seria a performance em "produção" ou novas amostras de previsão.

#### b. Como foi definida a função de custo utilizada?

A função de custo depende da técnica utilizada.

Na regressão simples = mínimos quadrados
No caso do Lasso = mínimos quadrados + regularização l1
Gradient Boosting = soma dos erros absolutos (robusta a outliers)

Vale ressaltar, que caso não fosse feito balanceamento da amostra, seria necessário incluir um peso na função de custo, privilegiando instâncias cuja variável resposta é menos frequente.

#### c. Qual foi o critério utilizado na seleção do modelo final?

R^2, RMSE e média por classe do RMSE. Sendo esse último o fator de decisão entre os modelos, dado que garante que diferente do modelo baseline, a regressão acerta fora da média de 'quality'.

#### d. Qual foi o critério utilizado para validação do modelo? Por que escolheu utilizar este método?

K-fold Stratified Cross Validation. Para garantir que o modelo é robusto 
a variações da amostra e aproveitar o máximo de amostras para treinamento.

#### e. Quais evidências você possui de que seu modelo é suficientemente bom?

Temos um modelo bom dentro do possível, diante do desbalanceamento da amostra. Foi corrigido o bias da amostra que tende a levar as estimativas para a média, produzindo uma ordenação mais interessante (ver no gráfico do notebook) e também um menor na média por categoria ('quality') do erro quadrático médio de 1.39 para 1.19. Sendo que no erro quadrático médio, sem quebrar por categoria, a queda foi de 0.56 (baseline) para 0.41 no modelo final, aprox 27% de incremento de performance.

Mostra-se que há uma ordenação dos resultados (predito x resposta), no entanto claramente há um erro maior para os valores extremos de quality em validação, onde haviam poucas instâncias de treino. Minha recomendação é que o modelo seja utilizado para ordenar e que um trabalho com mais amostras nos extremos seja feito para melhorar a qualidade da previsão dos valores absolutos de quality.
