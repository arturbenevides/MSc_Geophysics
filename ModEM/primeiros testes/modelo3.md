## Modelo 3
512 + 32 + 2 (Hz)
~38 períodos.
Com topografia

Grid refinado
* Resultado da inversão com 38 iterações. 

<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/ig3_42it.png' width=900>



* Resultado da inversão com  159 iterações.
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/ig3_159it.png' width=900>





#
MODELO 3
arquivos:
ig_m3.mod (con topografia)
ig.dat
igcov
igsint.dat

__________________________________________________
Resultados: 
* diretório resultados/
* resultado referente a 159 iterações na inversão NLCG
* rms=  11.85
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
