## Modelo 1
512 + 32 (Hz)
24 períodos.
* Com topografia
* Resultado da inversão com apenas 3 iterações. 
* Background resistivity: 100 ohm.m
rms=**********
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/mod1_3iteracoes.bmp' width=900>

* Resultado da inversão com apenas 59 iterações.
rms= 41
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/m1_59it.png' width=900>




#
MODELO 1
arquivos:
ig_m1.mod
igm1.dat
ig_m1.cov
ig_m1nested.mod
ig_m1sint.dat

__________________________________________________
Resultados: 
diretório res1/
resultado referente a 3 iterações na inversão NLCG
diretório res2/
*mesmo modelo
resultado referente a 59 iterações na inversão NLCG
rms=  41.285254
__________________________________________________
Dados da bacia de Iguatu

Estações: 48
Períodos: 24

Shortest period: 0.0893
Longest period: 25.59967

Parâmetros do modelo:
Background resistivity: 100 ohm.m
Min. skindepth: 0.472 km
Máx. skindepth: 25298 km

___________________________________________________
Parâmetros da inversão:
arq control.inv
Model and data output file name    : iguatu
Initial damping factor lambda      : 100.
To update lambda divide by         : 10.
Initial search step in model units : 1.
Restart when rms diff is less than : 2.0e-3
Exit search when rms is less than  : 1.05
Exit when lambda is less than      : 1.0e-4
Maximum number of iterations       : 400
