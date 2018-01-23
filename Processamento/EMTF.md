# EMTF

O objetivo do EMTF é fazer a estimativa robusta de funções transeferência, neste caso os tensores de impedância.
O módulo utilizado para fazer a estimativa do tensor é o `tranmt`(para levantamento com estações simples) e `multmtrn` (para levantamentos multiplas estações).

Os módulos de estimativa do tensor pedem como parâmetros de entrada os coeficientes de Fourier (cf) que são os parâmetros de saída do programa `dnff`, responsável por cálcular os coeficientes para determinado janelamento de amostras. 

O `dnff`precisa que os dados estejam em um formato binário padrão. Se os dados estiverem em outro formato é necessário que seja feita uma conversão. O EMTF disponibiliza dois módulos de conversão: `rfemi` (para o sistema EMI-MT1) e `rfasc` (para arquivo ascii simples).



## rfemi

Esse módulo reformata arquivos em formato EMI (MT1) para o binário padrão do EMTF.

>**Input**: arquivos.TS e arquivo.clk ([descrição](https://github.com/arturbenevides/Magnetotelurico/blob/master/Processamento/clock.md))
(é necessário ter os arquivos de calibração do equipamento)

>**Output**: arquivo.bin (binário) e arquivo.sp 

## dnff

Esse módulo faz os cálculos dos coeficientes de fourier para cada banda de frequência e inclui um esquema de decimação em cascata.

>**Input**: arquivos.bin  e arquivo.sp

>**Output**: CFs (coeficientes de fourier organizados por frequência) 

## tranmt

Esse módulo faz a estimativa robusta do tensor de impedância.

>**Input**: CFs 

>**Output**: TFs (arquivo com as funções transferência) e cov (erro e covariancias)

