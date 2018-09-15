# Inversões 


* Bacia do Iguatu:
* 48 estações.
* Ts1,2 e 3.

 - [ ] ig1 100 ohm.m/malha1/xy,yx 7%/xx,yy=15%/ curvas pós processamento = [1]
 - [ ] ig2 100 ohm.m/malha1/xy,yx 7%/xx,yy=15%/ [1] + com interp. e suav =[2]
 - [ ] ig3 100 ohm.m/malha1/xy,yx 7%/xx,yy=15%/ [2] + com correção static shift =[3]
 - [ ] ig4 1000 ohm.m/malha1/xy,yx 7%/xx,yy=15%/ [3]
 - [ ] ig4 500 ohm.m/malha1/xy,yx 7%/xx,yy=15%/ [3]
 - [ ] ig5 250 ohm.m/malha1/xy,yx 7%/xx,yy=15%/ [3]
 - [ ] ig6 50 ohm.m/malha1/xy,yx 7%/xx,yy=15%/ [3]
 - [ ] ig7 1 ohm.m/malha1/xy,yx 7%/xx,yy=15%/ [3]
 - [ ] ig8 100 ohm.m/malha1/xy,yx 7%/xx,yy=15%/ [3] (apenas para o MT1)



## Modelo 1
512 + 32 (Hz)
24 períodos.
* Com topografia
* Background resistivity: 100 ohm.m
* 59 iterações.
* rms= 41
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/ig1_59it.png' width=900>

## Modelo 1.2
512 + 32 (Hz)
24 períodos.
*  Sem topografia
* Background resistivity: 100 ohm.m
* iterações:
* rms= 


## Modelo 2
512 + 32 + 2 (Hz)
~38 períodos.
* Com topografia
* 104 iterações
* rms=13
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/ig2_104it.bmp' width=900>

## Modelo 3
512 + 32 + 2 (Hz)
~38 períodos.
* sem topografia
* grid refinado
* 42 iterações
* rms=17
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/ig3_159it.png' width=900>

## Modelo 4
512 + 32 + 2 (Hz)
~38 períodos.
* sem topografia
* grid combinado
*  iterações
* rms=
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/ig4_it84_withtopo.bmp' width=900>

## Modelo 5
512 + 32 + 2 (Hz)
~38 períodos.
* sem topografia
* grid combinado
*  iterações
* rms= 18
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/ig5_69it.bmp' width=900>

## Modelo 6
512 + 32 + 2 (Hz)
~38 períodos.
* sem topografia
* grid combinado
* iterações:
* rms= 
