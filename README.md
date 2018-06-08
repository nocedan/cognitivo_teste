# Wine Quality Modeling

Respostas às perguntas propostas:

a. Como foi a definição da sua estratégia de modelagem?

1. Fiz um pré processamento dados: subir os dados para um dataframe, garantindo consistência. Após olhar as distribuições das variáveis individualmente e em conjunto, decidi fazer uma inputação de missings para o campo 'alcohol' utilizando uma regressão. Também foi feita uma correção no campo 'density'. Finalmente, fiz uma normalização dos campos e guardei os dados pré processados em um pkl.

2. Para obter um baseline de performance, testei de maneira rápida (sem otimização) uma regressão simples e verifiquei um r2 de 0.31.

3. Na tentativa de melhorar a performace, fiz uma "feature engeneering" para criar uma quantidade substancial de novas features.

4. Finalmente, testei diversas técnicas e procurei fazer uma otimização de performance através da variação dos hiperparametros.

b. Como foi definida a função de custo utilizada?

A função de custo depende da técnica utilizada. No caso do Lasso, não é necessário se preocupar com multicolinearidade, poque isso é feito na otimização da função de custo. Para a regressão simples, é necessário fazer uma seleção de features não correlacionadas.

c. Qual foi o critério utilizado na seleção do modelo final?

Os critérios foram maior performance, e menor complexidade, nessa ordem.

d. Qual foi o critério utilizado para validação do modelo? Por que escolheu utilizar
este método?

K-fold. Cross validation. Para garantir que o modelo é robusto a variações da amostra.

e. Quais evidências você possui de que seu modelo é suficientemente bom?

O prórprio processo de análise e pré-processamento, a metodologia para criação e seleção de features e as técnicas utilizadas de forma consistente garantem que possíveis incrementos de performance além do que temos, serão marginais. Além disso, no processo de otimização da performance baseline conseguiu-se x% de incremento no r2.