## Modelo 5
512 + 32 + 2 (Hz)
~38 períodos.
* sem topografia

* Resultado da inversão com x iterações. 

<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/ig5_10km.bmp' width=900>

Visuzalizando mais profundo:
* Resultado da inversão com  51 iterações.

<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/ig5.bmp' width=900>


Tentativa de resultado sem a utilização da topografia e com um grid mais refinado no eixo e Z e menos refinado nos eixos x e y.
A resistividade de inicial para o semi-espaço homegêneo foi de 1000 ohm.m.
O erro floor nos dados adotado foi de 5% para os eixos xy e yx e 10% para os eixos xx e yy.


#
MODELO 4
arquivos:
ig_m2.mod
ig.dat
ig.cov
igtop.mod
igsint.dat

__________________________________________________
Resultados: 
* diretório result1/
* resultado referente a 104 iterações na inversão NLCG
* rms=  13.17
__________________________________________________
Dados da bacia de Iguatu

Estações: 48
Períodos: 24

Shortest period: 0.0893
Longest period: 25.59967

## Parâmetros do modelo:

> Background resistivity: 100 ohm.m

> Min. skindepth: 0.472 km

> Máx. skindepth: 25298 km

## Parâmetros da inversão:

arq control.inv

Model and data output file name    : iguatu

Initial damping factor lambda      : 100.

To update lambda divide by         : 10.

Initial search step in model units : 1.

Restart when rms diff is less than : 2.0e-3

Exit search when rms is less than  : 1.05

Exit when lambda is less than      : 1.0e-4

Maximum number of iterations       : 400
