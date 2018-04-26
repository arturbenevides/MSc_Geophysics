# Processamento Z

## Campanha iguatu

Conteúdo do diretório:

* raw_data > MT001         (pastas contendo os dados brutos e os cloks)
* DATA > 04i0xx_tsx.bin, .err e .log (conté o binário reformatado e os arquivos com erro e o log)
* SP > 04I0XX_TSX.sp       (arquivos de parâmetros do sistema, referente ao equipamento de aquisição)
* FC00128 > 04I0XX_TSX.f5  (coeficientes de fourier)
* MT0128 > 04I0XX_TSX.zss   (resultados)

> `emi2egb local\04I0XX.TSX 0XX 2004-06-04T09:20:00`
O comando permite que os dados vão para pasta DATA, mesmo os dados estando em uma subpasta em raw data.

> `echo "04I0XX_TSX.bin janela ss" > tmp.tmp`  
ou
> `echo "04I0XX_TSX.bin janela ss;bsX" >tmp.tmp`
esse comando tem que ser utilizado a cada banda de processamento, pois o nome do arquivo modifica.

> `processamentoZbin tmp.tmp`
O processamento recebe o arquivo temp contendo o nome do arquivo e a janela




# Planejamento

Como alguns dados estão com inversão de polaridade, recomenda-se processar para checar o comportamento da curva dos tensores xy (deve ser majoritariamente positivo) e yx (deve ser majoritariamente negativo).

Após o processamento Z, se checado e sendo positivo a mudança de polaridade, modificar os fatores de ganho nos arquivos .sp referente a banda. 

Para inversão de polaridade referente ao eletrodos (checar as curvas), em relação as bobinas (checar o tipper).

Após acertada a polaridade, procederíamos a análise das séries temporais, mas comando egb2tss só aceita arquivo.asc .
Por isso passamos para avaliação das melhores curvas selecionando os pontos por periodo.

O tojone permite selecionar melhores resultados entre diferentes run (banda TS3, TS4...). Um arquivo txt deve ser criado para informar os trechos que devem ser selecionado.

> tojones


# Relatório do processamento

14/04/2018

As primeiras 5 estações apresentaram problemas na conversão da banda ts1 e uma estação apresentou problema com a banda ts3 (Estação MT004).

Aparentemente todas as bandas ts1 não estão rodando. virificar o erro.

- [x] Rfemi todos TS3 e TS4

- [ ] Rfemi todos TS1 e TS3 estação 004

#

### Estação 001

- [x] processamentoZ ts4
  - [s] polaridade invertida 
  
- [x] processamentoZ ts3
  - [s] polaridade invertida (eletrodo)

- [x] tojones

8 períodos TS4
10 períodos TS3


### Estação 002

- [x] processamentoZ ts4
  - [s] polaridade invertida 
  
- [x] processamentoZ ts3
  - [ ] polaridade invertida 

 A polaridade estava com uma inversão atípica
 Inicialmente. Ex + Ey -
 Melhor resultado é com os dois positivos.
 A caderneta aponta que Ex é -Ex.
 
 Escolhi manter o resultado com os dois positivos para continuar. MElhor checar estaçes próximas para ver o comportamento do tipper e avaliar as polaridades das bobinas. Nas cadernetas nada  dito em relação as bobinas.
 
 
- [ ] tojones

### Estação 004

- [x] processamentoZ ts4
  - [s] polaridade invertida 
 
A plaridade estava invertida nos dois pontos do EX ( ambos estavam negativos nos campos elétricos). Na caderneta havia um apontamento para essa situação.
Corrigido (basear outras por essa).
 
**TS3 não passou no emi2egb**

- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 005

- [x] processamentoZ ts4
  - [s] polaridade invertida 
A caderneat apontava inversão de direção do eletrodo Ey; tentei inverter somente o Ey no sp, mas não resultou no resultado correto. Apenas invertendo o sinal dos dois.

- [x] processamentoZ ts3
  - [s] polaridade invertida 
Corrigida baseado na correção do ts4
- [ ] tojones

### Estação 008

- [x] processamentoZ ts4
  - [s] polaridade invertida 
  
Corrigido.
Apresenta um deslocamento estre as curvas de resitividade, aparentemente devido ao static shift.

- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones

### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones
### Estação 

- [ ] processamentoZ ts4
  - [ ] polaridade invertida 
  
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 

- [ ] tojones






