# ModEM

É evidente que os modelos 3D são os que podem representar mais adequadamente as características do interior da Terra. 
Idealmente, a inversão 3D seria a opção mais prática de modelagem, pois pode ser aplicada diretamente após o processamento dos dados, 
enquanto uma série de análises de dimensionalidade e hipóteses (já que estruturas puramente 2D praticamente não existem na natureza) 
precisam ser feitas antes de se aplicar a inversão 2D. Porém, o grande empecilho dos métodos de inversão 3D é o custo computacional
consideravelmente alto (impraticáveis até alguns anos). Contudo, o desenvolvimento de novos métodos e algoritmos na última década trouxeram 
significativo avanço da técnica, tornado a mesma possível ainda com certo custo computacional (Antunes, 2012).

## Método de Inversão

A inversão de dados EM é um método automatizado para determinar um modelo de condutividade elétrica que melhor represente a Terra
e que seja aceitável em termos geológicos. Para solucionar o problema, duas condições devem ser respeitadas simultaneamente: 
o modelo deve gerar dados (através do cálculo direto) que se ajustem aos dados medidos dentro de um nível de erro aceitável; 
e o modelo deve ser suave com a menor norma possível. Para isso, os programas de inversão buscam minimizar uma função de penalidade
(também chamada função objetivo ou unconstrained functional). Para o algoritmo usado nesse estudo, a função de penalidade tem a forma:
<img src='https://github.com/arturbenevides/Magnetotelurico/blob/master/Figs/funcao_penalty.png' width =600>

onde **m** é o vetor de dimensão *m* de parâmetros do modelo de condutividade da Terra, **d** é o vetor de dados com dimensão n, **C**d ´r a covariância do erro dos dados, **f(m)** é o resultado do cálculo direto de **m**, **m0** é o modelo inicial, **C**m (ou mais
apropriadamente *ν*−1**C**m) é a covariância do modelo ou termo de regularização e *ν* é um multiplicador Lagrangiano (parâmetro de amortecimento). O primeiro termo da Equção acima representa o ajuste dos dados medidos **d** com a resposta do cálculo direto para o modelo **m**. O segundo termo representa a norma do modelo, que reflete a suavidade do mesmo. Para um valor baixo de *ν* a inversão irá priorizar o ajuste dos dados medidos (**d**) com os modelados (**f(m)**). Para *ν* alto, o desajuste nos dados é menos importante e a suavidade do modelo é priorizada. Logo, o peso entre a suavidade do modelo e o ajuste dos dados é dado por *ν*, que devido a isso pode ser
chamado de parâmetro de amortecimento.

Alguns métodos matemáticos têm sido aplicados em diferentes algoritmos de inversão, tais como: Occam clássico, Occam no espaço dos dados, método de GaussNewton (GN), método de Gauss-Newton com gradiente conjugado (GN-CG), quasiNewton (QG), método de gradientes conjugados não lineares (NLCG), entre outros.
Uma revisão geral desses métodos é apresentada em Siripunvaraporn (2011). A minimização de uma função de penalidade para qualquer dos métodos mencionados é resolvida de modo iterativo. Por exemplo, no método de Gauss-Newton em que a linearização dessa equação nas vizinhanças do modelo **m**k (referente a k-ésima iteração) para uma pequena perturbação do modelo **δ**m leva a um sistema de mxm
equações definidas por:
<img src='https://github.com/arturbenevides/Magnetotelurico/blob/master/Figs/minimizacao.png' width=600>

onde **r = d − f(m)** k é o resíduo dos dados. Solucionando a equação (2) para **δ**m é possível encontrar um novo modelo dado
por **m**k+1 = **m**k + **δ**m.

Uma peça fundamental dos métodos de inversão é encontrar a matriz Jacobiana, ou matriz de sensibilidade **J** com dimensões
n × m. Essa matriz define as derivadas de **f** em relação ao modelo **m**, tal que J = Drond**f**/Dronde**m** e os elementos da matriz são dados por Jij = Drond *f*i/Drond *m*j. Obter **J** é um dos grandes empecilhos dos métodos clássicos de inversão devido a sua grande dimensão e dificuldades para ser calculada e armazenada. No entanto, métodos alternativos como o NLCG podem minimizar a função
objetivo sem a necessidade de calcular a Jacobiana completa para o modelo de cada iteração.

