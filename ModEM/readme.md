# Inversões 


* Bacia do Iguatu:
* 48 estações.
* Ts1,2 e 3.

 - [x] TS4 + TS3 (Rough grid)
 
 - [ ] TS4 + TS3 (Finer grid)
 
 - [x] TS4 + TS3 + TS1 (Rough grid)
 
 - [ ] TS4 + TS3 + TS1 (Finer grid)
 
 - [ ] TS4 + TS3 + TS1 (with prior model)
 
 
Controle de testes
## Modelo 1
512 + 32 (Hz)
24 períodos.
* Com topografia
* Resultado da inversão com apenas 3 iterações. 
rms=**********
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/mod1_3iteracoes.bmp' width=900>

* Resultado da inversão com apenas 59 iterações.
rms= 41
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/m1_59it.png' width=900>


## Modelo 2
512 + 32 + 2 (Hz)
~38 períodos.
* Com topografia

* Resultado da inversão com 21 iterações. 

<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/m2_21it.png' width=900>

* Resultado da inversão com  51 iterações.

<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/m2_51it.png' width=900>

* Resultado da inversão com  104 iterações. (**última**)
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/mod2_104it.bmp' width=900>

## Modelo 3
512 + 32 + 2 (Hz)
~38 períodos.
* sem topografia
* grid refinado

<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/m3_42it.png' width=900>
