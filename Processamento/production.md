# Campanha de Iguatu

**Diretórios:**
>* /raw_data : MTxxx         *(pastas contendo os dados brutos e os cloks)*
>* /DATA :  04I0xx_tsx.bin ; .err ; .log *(contém o binário reformatado e os arquivos com erro e o log)*
>* /SP : 04I0XX_TSX.sp       *(arquivos de parâmetros do sistema, referente ao equipamento de aquisição)*
>* /FC00128 : 04I0XX_TSX.f5   *(coeficientes de fourier)*
>* /MT0128 : 04I0XX_TSX.zss   *(resultados)*

#
### Passos

**`emi2egb rawdata/MTXXX/04I0XX.TSX 0XX 2004-06-04T09:20:00`**
* *O comando permite que os dados vão para pasta DATA, mesmo os dados estando em uma subpasta em raw data.*

**`echo "04I0XX_TSX.bin janela ss" > tmp.tmp`**  
* *o comando echo cria um arquivo temporário que será usado pelo próximo comando.*
ou

**`echo "04I0XX_TSX.bin janela ss;bsX" > tmp.tmp`**
* *bsX permite usar outras níveis de decimação, quando chama outras arquivos options.cfg.*

**`processamentoZbin tmp.tmp`**
* *O processamento recebe o arquivo temp contendo o nome do arquivo e a janela*
#
### Planejamento

* Como alguns dados estão com inversão de polaridade, recomenda-se realizar o processamento Z para checar o comportamento da curva dos tensores Zxy e Zyx, que em teoria deve ser majoritariamente positivo e negativo, repectivamente.

* Após o processamento, se checado que o comportamento das curvas não estão consonantes com a teoria, deve-se verificar na caderneta se existe algum comentário referente aquela aquisição.

* Havendo ou não comentários no relatório de campo, proceda a mudança de polaridade nos **eletrodos**, modificando os sinais nos fatores de ganho do Ex e Ey nos arquivos .sp referente a banda. 

* Após avaliação das polaridade via modificação do sinal do eletrodo, é necessário veificar se o tipper tem o mesmo comportamento em estações vizinhas. A mudança de polaridade pode estar associada a problemas na bobina também.

* Após acertada a polaridade, procederíamos a análise das séries temporais, mas comando egb2tss só aceita arquivo.asc .
Por isso passamos para avaliação das melhores curvas selecionando os pontos por periodo.

* O tojone permite selecionar melhores resultados entre diferentes run (banda TS3, TS4...)
#
# Relatório do processamento

14/04/2018

As primeiras 5 estações apresentaram problemas na conversão da banda ts1 e uma estação apresentou problema com a banda ts3 (Estação MT004).

Aparentemente todas as bandas ts1 não estão rodando. virificar o erro.

- [x] Rfemi todos TS3 e TS4

- [ ] Rfemi todos TS1 e TS3 estação 004

#

### Estação 001
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones (8 períodos TS4, 10 períodos TS3)
#
### Estação 002
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
 (i)A polaridade estava com uma inversão atípica, (ii)inicialmente: Ex + Ey -, (iii) Melhor resultado é com os dois positivos. A caderneta aponta que Ex é -Ex. 
 Escolhi manter o resultado com os dois positivos para continuar. MElhor checar estações próximas para ver o comportamento do tipper e avaliar as polaridades das bobinas. Nas cadernetas nada  dito em relação as bobinas.
- [ ] tojones
#
### Estação 004
- [x] processamentoZ ts4
A plaridade estava invertida nos dois pontos do EX ( ambos estavam negativos nos campos elétricos). Na caderneta havia um apontamento para essa situação. **Corrigido (basear outras por essa)**
 **TS3 não passou no emi2egb**
- [ ] processamentoZ ts3
  - [x] polaridade invertida (ts4 por enquanto)
- [ ] tojones
#
### Estação 005
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida (A caderneta aponta inversão de direção do eletrodo Ey; tentei inverter somente o Ey no sp, mas não resultou no resultado correto. Apenas invertendo o sinal dos dois. (ii) Polaridade do TS3 corrigido baseado na correção do ts4
- [ ] tojones
#
### Estação 008
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [s] polaridade invertida 
> Apresenta um deslocamento estre as curvas de resitividade, aparentemente devido ao static shift.
- [ ] tojones
#
### Estação 9

- [x] processamentoZ ts4
  - [s] polaridade invertida 
  
- [x] processamentoZ ts3
  - [s] polaridade invertida 

- [ ] tojones

### Estação 12

- [x] processamentoZ ts4
  - [s] polaridade invertida 
  
- [x] processamentoZ ts3
  - [s] polaridade invertida 

Não tem diferença entre os sinais dos campos elétricos e magnéticos no sp do TS4 e do TS3. A caderneta informa que os resultados estavam saindo ruim, pois não estavam conseguindo dar ganhos nos eletrodos que ja estavam saturados.
As ultimas medidas não tem anotaçes, talvez o erro não tenha pesistido, mas qualquer um que existir poderá ser explicado pela saturação. 



- [ ] tojones

### Estação 14

- [x] processamentoZ ts4
  - [s] polaridade invertida 
  
- [x] processamentoZ ts3
  - [s] polaridade invertida 

- [ ] tojones

### Estação 15

- [x] processamentoZ ts4
  - [s] polaridade invertida 
  
- [x] processamentoZ ts3
  - [n] polaridade invertida 

A banda TS4 estava com inversão de polaridade, enquanto a banda ts3 não. Na caderneta nada estava falando sobre isso.

- [ ] tojones
### Estação 18

- [x] processamentoZ ts4
  - [s] polaridade invertida 
  
- [x] processamentoZ ts3
  - [s] polaridade invertida 

- [ ] tojones

Aparentemente, ao plotar as duas curvas sem mudar nada, uma das curvas parece fazer sentido. Quando mudamos uma que não faz sentido, a outra passa a não fazer sentido também.

### Estação 21

- [x] processamentoZ ts4
  - [s] polaridade invertida 
 
 
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 
**Problema na decimação. só vai até o terceiro nível** 
 * Banik encaminhou o arquivo para melhorar a decimação, mas o dado est com algum problema. verificar.

- [ ] tojones

### Estação 24

- [x] processamentoZ ts4
  - [s] polaridade invertida 
  
- [x] processamentoZ ts3
  - [s] polaridade invertida 

- [ ] tojones

### Estação 27

- [x] processamentoZ ts4
  - [s] polaridade invertida 
  
- [x] processamentoZ ts3
  - [s] polaridade invertida 

- [ ] tojones

### Estação 30
**Processamento feito, entretanto o dado ta muito ruidoso; checar a cardenetas que aponta um problema com a bobina e refeazer o processamento, checar vizinhas**

- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 

- [ ] tojones

### Estação 32

- [x] processamentoZ ts4
  - [s] polaridade invertida 
  
- [x] processamentoZ ts3
  - [s] polaridade invertida 

- [ ] tojones
### Estação 36

- [x] processamentoZ ts4
  - [s] polaridade invertida 
  
- [x] processamentoZ ts3
  - [s] polaridade invertida 

- [ ] tojones

### Estação 39

- [x] processamentoZ ts4
  - [s] polaridade invertida 
  
- [x] processamentoZ ts3
  - [s] polaridade invertida 

- [ ] tojones

### Estação 42
**Não tem TS4**  
- [x] processamentoZ ts3
  - [x] polaridade invertida 

- [ ] tojones

### Estação 46

- [x] processamentoZ ts4
- [x] processamentoZ ts3
- [x] polaridade invertida 

- [ ] tojones

### Estação 48

- [x] processamentoZ ts4
- [x] processamentoZ ts3
- [x] polaridade invertida 

* Mudar range
- [ ] tojones

### Estação 49

- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [s] polaridade invertida 
- [ ] tojones

### Estação 50

- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
* Comporatmento do tipper muito estranho. Observar com outras estações.
* RUidoso
* Nenhum comentário na caderneta.

- [ ] tojones

### Estação 51

- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [s] polaridade invertida 

- [ ] tojones

### Estação 54

- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
* Dado ruidoso, tipper estranho
- [ ] tojones

#
### Estação 56
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones
#
### Estação 57

- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 

- [ ] tojones
### Estação 58 

- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones

### Estação 59 
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
* Verificar o TS3. muito ruidoso.
- [ ] tojones
#
### Estação 62
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [ ] polaridade invertida 
* Verificar se a polaridade de TS3 realmente estava ionvertida, os resultados estam estranhos.
- [ ] tojones
#
### Estação 63
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones
boa estação;
#
### Estação 65
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones
#
### Estação 68

- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
* Tipper estático, instabilidade nos ultimos períodos de TS3, chega at inverter a polaridade.
- [ ] tojones
#
### Estação 71
- [ ] processamentoZ ts4
- [x] processamentoZ ts3
  - [ ] polaridade invertida 
* **TS4 só roda com dois níveis de decimação.**
* Tiper estático.
- [ ] tojones
#
### Estação 80
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
* Tipper do TS4 muito ruim.
* ultimos periodos do TS4 ruim
- [ ] tojones
#
### Estação 84
- [ ] processamentoZ ts4 
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 
* As Curvas não estão casando.  
- [ ] tojones
#
### Estação 88
- [ ] processamentoZ ts4 
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 
* As curvas não casam em Zxy E Zxx e na fase. 
- [ ] tojones
#
### Estação 93
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
  * as curvas estão ruidosa nos ultimos períodos;
- [ ] tojones
#
### Estação 97
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
* infomações boas nos gráficos dos tensores e ruim no grafico da resistividade. (Modificar apenas o TS3 para checar mudancas).
- [ ] tojones
#
### Estação 101
_ Resultado muito ruim, semelhante ao problema da estação 97.
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [ ] polaridade invertida 
- [ ] tojones
#
### Estação 103
* problema de range
* curvas não batem em Zyx E Zyy 
* REFAZERC
- [ ] processamentoZ ts4 
- [ ] processamentoZ ts3
  - [ ] polaridade invertida 
- [ ] tojones
#
### Estação 107
* Problemas semelhantes as estaçes acima.
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones
#
### Estação 109
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones
#
### Estação 115
* As curvas estão ocm um aparente deslocamento entre elas, mas seuem a mesma tendencia. 
* Reprocessar
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [ ] polaridade invertida 
- [ ] tojones
#
### Estação 116
* Ruim.. não estão cansando.
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [ ] polaridade invertida 
- [ ] tojones
#
### Estação 119
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones
#
### Estação 123
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones
#
### Estação 128
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones
#
### Estação A01
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones
