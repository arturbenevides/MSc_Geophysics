# Inversões 


* Bacia do Iguatu:
* 48 estações.
* Ts1,2 e 3.

 - [x] ig1 (TS4 + TS3) (Rough grid1) - (Meio Homogêneo - 100 ohm) / erro do dado
 - [x] ig2 (Rough grid2) - (Meio Homogêneo - 100 ohm) / erro do dado
 - [x] ig3 (Finer grid) - (Meio Homogêneo - 100 ohm) / erro do dado
 - [x] ig4 (combined grid) - (topo) (Meio Homogêneo - 100 ohm) / error floor (10 xx e yy, 5 xy e yx)
 - [x] ig4 (combined grid) - (Meio Homogêneo - 100 ohm) / error floor (10 xx e yy, 5 xy e yx)
 - [x] ig5 (combined grid) - (Meio Homogêneo - 1000 ohm) / error floor (10 xx e yy, 5 xy e yx)
 - [x] ig6 (combined grid) - (Meio Homogêneo - 500 ohm)  / error floor (10 xx e yy, 5 xy e yx)
 - [ ] ig7 (combined grid) - (Meio Homogêneo - 200 ohm)  / error floor (10 xx e yy, 5 xy e yx)
 - [ ] ig8 (combined grid) - (Meio Homogêneo - 50 ohm)   / error floor (10 xx e yy, 5 xy e yx)
 - [ ] ig9 (combined grid) - (Meio Homogêneo - 10 ohm)   / error floor (10 xx e yy, 5 xy e yx)
 - [ ] ig10 (combined grid) - (with prior model)

# 
### Rough grid 1

Item \ direction  |     X       |   y        |     Z
------------------|:-----------:|:----------:|:----------:
N of cell         |   57        |  64        |   35         
Cell dimension    |   750       |  750       |   50         
N of padding cells|   11        |      11    |            
increasing Factor |   1.2       |   1.2      |   1.2          

### Rough grid 2

Item \ direction  |     X       |   y        |     Z
------------------|:-----------:|:----------:|:----------:
N of cell         |   70        |  70        |   20         
Cell dimension    |   500       |  500       |   50         
N of padding cells|   18        |     18     |            
increasing Factor |   1.2       |   1.2      |   1.2          

### finer grid

Item \ direction  |     X       |   y        |     Z
------------------|:-----------:|:----------:|:----------:
N of cell         |   100       |  95        |   67         
Cell dimension    |   300       |  300       |   5         
N of padding cells|   25        |   25       |            
increasing Factor |   1.2       |   1.2      |   1.2     

### Combined grid

Item \ direction  |     X       |   y        |     Z
------------------|:-----------:|:----------:|:----------:
N of cell         |   70        |  70        |   30 *         
Cell dimension    |   500       |  500       |   5          
N of padding cells|   11        |   11       |            
increasing Factor |   1.2       |   1.2      |   1.2   

* Colocar um número de células para alcancar no máximo 100 km.
#

## Modelo 1
512 + 32 (Hz)
24 períodos.
* Com topografia
* Background resistivity: 100 ohm.m
* 59 iterações.
* rms= 41
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/ModEM/ig1_59it.png' width=900>


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

