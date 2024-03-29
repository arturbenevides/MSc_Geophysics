## Etapas propostas

- [x] Séries temporais [:mag_right:](https://github.com/arturbenevides/MSc_Geophysics/blob/master/Figs/time_series001.png)

- [x] Estimativa do tensor de impedância  e resistividade via winglink (pho, phase etc) (18/11/2017) [:mag_right:](https://github.com/arturbenevides/MSc_Geophysics/tree/master/Processamento/curvas%20by%20winglink)

- [x] Conversão das coordenadas utm>LL (18/11/2017) [:mag_right:](https://github.com/arturbenevides/MSc_Geophysics/blob/master/Notebooks/convert_utm_lat_long.ipynb)

- [x] Estimativa da impedância via [Egbert](http://www.complete-mt-solutions.com/mtnet/main/source.html#dec_codes) [:mag_right:](https://github.com/arturbenevides/MSc_Geophysics/tree/master/Processamento/curvas%20by%20EMTF) (25/04/2018)
  
   - [x] Montar [.clk](https://github.com/arturbenevides/MSc_Geophysics/blob/master/Processamento/clock.md)
   - [x] Usar o RFEMI / emi2egb
   - [x] processamentoZbin   (dnff e tranmt)
   - [x] tojones (Seleção de melhores curvas)

- [x] Colocar as coordenadas no header

- [x] Análise de dimensionalidade WALDIM [:mag_right:](https://github.com/arturbenevides/MSc_Geophysics/tree/master/An%C3%A1lise%20de%20Dimensionalidade)

- [x] Análise de dimensionalidade phase tensor [:mag_right:](https://github.com/arturbenevides/MSc_Geophysics/tree/master/An%C3%A1lise%20de%20Dimensionalidade)

- [x] Modelagem 3Dgrid

- [x] Inversão 3D usando o modEM [:mag_right:](https://github.com/arturbenevides/MSc_Geophysics/tree/master/ModEM)

#

## Estações


Frequências de sondagem

Extensão | Bandas de frequência 
---------|----------------------
TS4      | 512 Hz
TS3      |  32 Hz
TS2      |   5 Hz
TS1      |   2 Hz


`48 Sítios de aquisição`

- (1)  MT001
- (2)  MT002 `Sem ts1` 
- (3)  MT004
- (4)  MT005
- (5)  MT008
- (6)  MT009
- (7)  MT012
- (8)  MT014
- (9)  MT015
- (10) MT018
- (11) MT021
- (12) MT024
- (13) MT027
- (14) MT030
- (15) MT032
- (16) MT036
- (17) MT039
- (18) MT042 `sem ts4` 
- (19) MT046
- (20) MT048
- (21) MT049 
- (22) MT050
- (23) MT051
- (24) MT054
- (25) MT056
- (26) MT057
- (27) MT058
- (28) MT059 `sem ts1`
- (29) MT062 `sem ts1` 
- (30) MT063
- (31) MT065
- (32) MT068
- (33) MT071 
- (34) MT080
- (35) MT084
- (36) MT088 `sem ts1`
- (37) MT093
- (38) MT097
- (39) MT101
- (40) MT103
- (41) MT107
- (42) MT109
- (43) MT115
- (44) MT116
- (45) MT119
- (46) MT123
- (47) MT128
- (48) MT195 (*)
- (49) MTA01
#

Adicionais:
- (50) TESTE11
- (51) TESTE12
- (52) TESTE21
- (53) TESTE22
- (54) VARG1 `único que contem ts2`.
#
 
A estação MT195 pertencia ao perfil 4. Mas será removido devido a grande distância em que se encontra do ponto mais próximo.

