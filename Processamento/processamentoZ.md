# Campanha de Iguatu

**Diretórios:**
>* /raw_data : MTxxx         *(pastas contendo os dados brutos e os cloks)*
>* /DATA :  04I0xx_tsx.bin ; .err ; .log *(contém o binário reformatado e os arquivos com erro e o log)*
>* /SP : 04I0XX_TSX.sp       *(arquivos de parâmetros do sistema, referente ao equipamento de aquisição)*
>* /FC00128 : 04I0XX_TSX.f5   *(coeficientes de fourier)*
>* /MT0128 : 04I0XX_TSX.zss   *(resultados zss)*
>* /tojones : igxxx.dat; .png ; .ps *(tensores no formato jones); 

#
### Passos
#### ex:
**`emi2egb rawdata/MT001/04I001.TS4 001 2004-06-04T09:20:00`**
* *O comando permite que os dados vão para as pastas DATA e SP, mesmo os dados estando em uma subpasta em raw data.*

**`echo "04I001_TS4.bin janela ss" > tmp.tmp`**  
* *o comando echo cria um arquivo temporário que será usado pelo próximo comando.*
ou

**`echo "04I0XX_TSX.bin janela ss;bsX" > tmp.tmp`**
* *bsX permite usar outras níveis de decimação, quando chama outras arquivos options.cfg.*

**`processamentoZbin tmp.tmp`**
* *O processamento recebe o arquivo temp contendo o nome do arquivo e a janela*
#
### Planejamento

* Como alguns dados estão com inversão de polaridade, recomenda-se realizar o processamento Z para checar o comportamento da curva dos tensores Zxy e Zyx, que em teoria deve ser majoritariamente positivo e negativo, repectivamente.
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/Processamento/curvas%20by%20EMTF/ig001_pol_inv.png' width=500 >

* Após o processamento, se checado que o comportamento das curvas não estão consonantes com a teoria, deve-se verificar na caderneta se existe algum comentário referente aquela aquisição.

* Havendo ou não comentários no relatório de campo, proceda a mudança de polaridade nos **eletrodos**, modificando os sinais nos fatores de ganho do Ex e Ey nos arquivos .sp referente a banda. 

* Após avaliação das polaridade via modificação do sinal do eletrodo, é necessário veificar se o tipper tem o mesmo comportamento em estações vizinhas. A mudança de polaridade pode estar associada a problemas na bobina também.
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/Processamento/curvas%20by%20EMTF/ig001zss.png' width = 500 >

* Após acertada a polaridade, procederíamos fazer a análise das séries temporais, mas comando egb2tss só aceita arquivo.asc.
Por isso passamos para avaliação das melhores curvas selecionando os pontos por periodo.

* O tojone permite selecionar melhores resultados entre diferentes run (banda TS3, TS4...)
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/Processamento/tojones/ig001.png' width=500>

#
### Relatório do processamento

> 14/04/2018 ínicio (processamento das 5 primeiras estações e comentários iniciais sobre as curvas)

> 24/04/2018 update1 (processamento das demais estações e adição de comentários)

> 25/04/2018 update2 (melhorias da parte escrita do relatório)

> 02/05/2018 update3 (escolha de peíodos entre as curvas do ts3 e ts4)

> 03/05/2018 update4 (tojones para quase todas estações)

> 15/05/2018 update5 (processamento das últimas estações)

> 17/05/2018 update6 (tojones para todas as estações)
#
**Observações**
* As primeiras 5 estações apresentaram problemas na conversão da banda ts1 e uma estação apresentou problema com a banda ts3 (Estação MT004).

* Aparentemente todas as bandas ts1 não estão rodando. virificar o erro.
* Todas as estações possuem a parte inicial da curva da banda ts3 melhor do que a banda ts4 para mesma faixa. Exceto a estação 119.
* A seleção dos períodos utilizando o tojones seguiu para as estações a seguinte regra:

> Todas: TS4 [1-8] e TS3 [1-16] 
Exceto:
> ig 002 TS4 [1 14]
> ig119 : TS4 [1-9] e TS3 [2-15]
> ig115: TS4 [1-9] e TS3 [2-15]

- [x] rfemi todos TS3 e TS4
- [x] tojones nas estações.
- [ ] escolher o range
- [ ] rfemi todos TS1  
- [ ] rfemi TS3 MT004

#
### Estação 001
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
#
### Estação 002 
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
 obs:* A polaridade estava com uma inversão atípica, (ii)inicialmente: Ex + Ey -, (iii) Melhor resultado é com os dois positivos. A caderneta aponta que Ex é -Ex. 
 Escolhi manter o resultado com os dois positivos para continuar. MElhor checar estações próximas para ver o comportamento do tipper e avaliar as polaridades das bobinas. Nas cadernetas nada  dito em relação as bobinas.
#
### Estação 004
- [x] processamentoZ ts4
- [ ] processamentoZ ts3
  - [x] polaridade invertida
- [x] tojones
A plaridade estava invertida nos dois pontos do EX (ambos estavam negativos nos campos elétricos). Na caderneta havia um apontamento para essa situação. **Corrigido (basear outras por essa)**
 obs:*TS3 não passou no emi2egb e tem um único run.*
#
### Estação 005
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida (A caderneta aponta inversão de direção do eletrodo Ey; tentei inverter somente o Ey no sp, mas não resultou no resultado correto. Apenas invertendo o sinal dos dois. (ii) Polaridade do TS3 corrigido baseado na correção do ts4
- [x] tojones
#
### Estação 008
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
> Apresenta um deslocamento estre as curvas de resitividade, aparentemente devido ao static shift.
- [x] tojones
#
### Estação 9
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
#
### Estação 12
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
* Não tem diferença entre os sinais dos campos elétricos e magnéticos no sp do TS4 e do TS3, a caderneta informa que os resultados estavam saindo ruin, pois não estavam conseguindo dar ganhos nos eletrodos que ja estavam saturados.
* As ultimas medidas não tem anotaçes, talvez o erro não tenha persistido, mas qualquer um que existir poderá ser explicado pela saturação. 
- [x] tojones
#
### Estação 14
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
#
### Estação 15
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [ ] polaridade invertida 
* A banda TS4 estava com inversão de polaridade, enquanto a banda ts3 não. Na caderneta nada estava falando sobre isso.
- [x] tojones
#
### Estação 18
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones*
obs: * Aparentemente, ao plotar as duas curvas sem mudar nada, uma das curvas parece fazer sentido. Quando mudamos uma que não faz sentido, a outra passa a não fazer sentido também.
#
### Estação 21
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
obs:*Problema na decimação. só vai até o terceiro nível, Banik encaminhou o arquivo para melhorar a decimação,o dado está com algum problema desconhecido, verificar. Optou-se por utilizar um outro run para mesma banda. o dado está com boa resolução.

#
### Estação 24
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones
#
### Estação 27
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones
#
### Estação 30
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
#
### Estação 32
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones
#
### Estação 36
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones
#
### Estação 39
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [ ] tojones
#
### Estação 42 
- [x] processamentoZ ts3
  - [x] polaridade invertida
- [x] tojones **n feito**
Obs: *Estação sem o TS4 e está muito ruidosa.s
### Estação 46

- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
#
### Estação 48
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
* dado fora do range
- [x] tojones
#
### Estação 49
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
#
### Estação 50
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
* Comporatmento do tipper muito estranho. Observar com outras estações.
* Dado muito ruidoso
* Nenhum comentário na caderneta.
- [x] tojones
#
### Estação 51
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
#
### Estação 54
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
* Dado ruidoso, tipper estranho
- [x] tojones
#
### Estação 56
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
#
### Estação 57
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
#
### Estação 58 
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
#
### Estação 59 
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
* Verificar o TS3. muito ruidoso.
- [x] tojones
#
### Estação 62 X fazer inversão de polaridade para TS3 (tentar + -)
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [ ] polaridade invertida 
* **Verificar se a polaridade de TS3 realmente estava invertida, os resultados estam estranhos.**
- [ ] tojones
#
### Estação 63
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
* **boa estação**
- [ ] tojones
#
### Estação 65
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
#
### Estação 68
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
* Tipper estático, instabilidade nos ultimos períodos de TS3, chega até a inverter a polaridade.
- [x] tojones
#
### Estação 71 
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
obs:*TS4 só roda com dois níveis de decimação, iria pedir ao banik ou montar um options01024bs2.cfg, bs2.bla,bs2.bl., não foi preciso, utilizei outro run da mesma banda e o resultado foi de boa qualidade.*
#
### Estação 80
- [x] processamentoZ ts4
- [x] processamentoZ ts3
  - [x] polaridade invertida 
* Tipper do TS4 muito ruim.
* ultimos periodos do TS4 ruim
- [x] tojones
#
### Estação 84
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
obs: *As curvas tem um aspecto um pouco estranho. Existe um sérido deslocamento nas curvas* 

#
### Estação 88 
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
obs:*As curvas não casavam em Zxy E Zxx e na fase.*
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
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida
- [x] tojones
obs:*Resultado muito ruim, semelhante ao problema da estação 97.*
#
### Estação 103 
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
obs:*Curvas não batia;*
**problema de range**
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
- [X] tojones
#
### Estação 115
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
obs:*As curvas estão com um aparente deslocamento entre elas, mas seguem a mesma tendencia, foi feito todo processamento, mas será mostrado a sergio para ver se pode-ser feito algo diferente.
#
### Estação 116
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida
- [x] tojones
obs: *estação ruidosa
#
### Estação 119
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
#
### Estação 123
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
#
### Estação 128
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
#
### Estação A01
- [x] processamentoZ ts4 
- [x] processamentoZ ts3
  - [x] polaridade invertida 
- [x] tojones
