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
[](img= src'https://github.com/arturbenevides/Magnetotelurico/blob/master/Figs/funcao_penalty.png', width =200)
