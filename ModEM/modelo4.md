## Modelo 4
512 + 32 + 2 (Hz)
~38 períodos.

### Com topografia

* Resultado da inversão com 81 iterações. 
RMS= 11.61

<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/ig4_it84_withtopo.bmp' width=900>


### Sem topografia
* Resultado da inversão com  x iterações.



#
MODELO 4
arquivos:
ig4nes.mod
ig4topo.mod
ig5topones.mod
ig4.dat
ig4.cov

__________________________________________________
Resultados: 
* diretório result with topography/
* resultado referente a inversão considerando a topografia
* diretório result without topography/
* resultado não considerando a topografia

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
