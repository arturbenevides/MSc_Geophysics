# EMTF

O objetivo do EMTF é fazer a estimativa robusta de funções transeferência, neste caso os tensores de impedância.
O módulo utilizado para fazer a estimativa do tensor é o `tranmt`(para levantamento com estações simples) e `multnmt` (para levantamentos multiplas estações).
Estes módulos tem como parâmetros de entrada os coeficientes de Fourier (cf) que são os parâmetros de saída do programa `dnff`, 
responsável por cálcular os coeficientes para determinado janelamento de amostras. 
Os dois módulos do EMTF citado acima precisam que os dados estejam em um formato binário padrão.Se os dados estiverem
em outro formato é necessário que seja feita uma conversão.
O EMTF disponibiliza dois módulos de conversão: `rfemi` (para o sistema EMI-MT1) e `rfasc` (para arquivo ascii simples).


A primeira etapa do processamento consiste em reformatar o dado de um padrão transformada dos dados do dom´ınio
do tempo para o dom´ınio da frequ^encia. No dom´ınio da frequ^encia, a Equa¸c~ao 3.1
´e solucionada para determinar as VTFs Tzx e Tzy complexas.

## rfemi

## 
