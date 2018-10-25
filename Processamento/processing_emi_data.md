# Processamento de dados MT (ADU/EMI/LEMI)
@Benevides


**Etapas para processamento robusto dos dados MT (adquiridos com o equipamento da EMI) utilizando o pacote EMTF (Egbert e Eisel, 1998) e as otimizações propostas pelo pacote processamentoZ (Marcelo Banik).**


## Diretórios pasta modelo:
>* /raw_data/MTxxx: 04Ixx.TSx; 04IxxTSX.clk  *(pastas contendo os dados brutos .TS, .T ou .ATS e os arquivos cloks .clk)*
>* /sensor:   *(Pastas contendo os arquivos de sensores do equipamento)*
>* /DATA :  04I0xx_tsx.bin ; .err ; .log *(contém o binário reformatado e os arquivos com erro e o log)*
>* /SP : 04I0XX_TSX.sp        *(arquivos de parâmetros do sistema, referente ao equipamento de aquisição)*
>* /FCXXXX : 04I0XX_TSX.f5   *(armazenam os coeficientes de fourier por janelas, ex: FC00128)*
>* /MTXXXX : 04I0XX_TSX.zss  *(armazenam as funções de transferência .zss por jannelas, ex: MT00128)*
>* /tojones : igxxx.dat; .png ; .ps *(armazenam as funções de transferência no no formato jones); 

## Conversão de dados:

#### Conversão .ts -> .bin (EMI)
**`emi2egb rawdata/STN001/04I001.TS4 001 2004-06-04T09:20:00`**
* *Esse comando permite a conversão do dado do formato .TS para .bin (padrão para o EMTF), os dados convertidos são alocados para as pastas DATA e SP, mesmo os dados estando em uma subpasta em raw data.*
* *001 é a pasta onde contém os arquivos da estação 001.*
* *2004-06-04T09:20:00 é a data e o horário definido para primeira estação*. Esse horário pode ser atribuído para todas as estações, mesmo que tenha sido definido um horário de aquisição para cada banda nos arquivos clock. Essa metodologia é utilizada para single station. Para referência remota o procedimento é diferente.*

#### Conversão .t -> .asc (lemi)
**`lemi-check-time *.txx > time.log`**
* *Esse comando permite a verificação do tempo de cada arquivo .txx (ex 04ig001a.t59, 04ig001b.t59).* 

**`lemi-check-runs time.log > runs.log`**
* *O comando acima agrupa os arquivos .t que pertencem a mesma contagem. O agrupamento permite verificar qual a maior série.*
* *A maior sequencia deve ser copiada e concatenada em um único arquivo, como mostrado abaixo:*

**`cat 04ig001a.t 04ig001b.t 05ig001h.t 04ig001p.t > 04ig001.t`**
* *Os arquivos estão prontos para fazer a conversão. Dentro da pasta modelo procedemos com o comando de conversão `lemi2egb`.*

**`lemi2egb rawdata/STN001/04IG001.t`**
* *O arquivo convertido (.asc) será direcionado a pasta DATA e o arquivo dos parâmetros para a pasta SP.*

#### Conversão .ats -> .asc (ADU)

**`ats2asc rawdata/STN001/04IG001.ats`**

* *Esse comando deve ser dado dentro da pasta modelo apontando a pasta que contem os arquivos ats. Os arquivos .asc convertidos serão armazenados na pasta DATA.*


## Processamento 
Uma vez que todos os arquivos estejam na pasta DATA e os arquivos de parâmetro na pasta SP, eles podem ser processados utilizando o comando **`processamentoZ`**, exceto os arquivos .bin (Emi) que utilizam o comando **`processamentoZbin`**. O processamento pode ser feito como single station ou com referência remota. 

### Single station (ss)

**`echo "04I001.asc janela ss" > tmp.tmp`**
* *o comando echo "--"> .temp cria um arquivo temporário que será usado pelo comando de processamento.*
* *em vez de preencher o arquivo tmp.tmp com cada estação e janela, podemos preenche-la diretamente com todos as estações e janelas de processamento. O preenchimento pode ser feito criando um arquivo de texto ou usando echo " -- " >> e acrescentando linha a linha.*
* *As janelas disponíveis são: 128, 256, 1024, 2048, 4096, 8192, 16384, 32768, 65536.

**`processamentoZ tmp.tmp`**
* *O processamento recebe o arquivo temp contendo o nome do arquivo, a janela e a opção ss que significa single station*
* *Como resultado, temos o armazenamento dos coeficientes de fourier nas pastas FCXXXXX e das funções de transferência na pasta MTXXXX;*

* *Em alguns casos as séries temporais não suportam todos os níveis de decimação (5), para viabilizar o processamento é utilizado nívies menores de decimação. Isso pode ser feito modificando alguns arquivos de controle: options.cfg e bsX.bl. Além disso, o comando é altereado para inclusão de um termo bsX, em que X representa o nível de decimação utilizado.

**`echo "04I0XX_TSX.asc janela ss;bsX" > tmp.tmp`**
* *bsX permite usar outras níveis de decimação, quando chama outros arquivos options.cfg.*

* *O processamento para os arquivos (.bin) da EMI utiliza o comando `processamentoZbin`, mas segue as mesmas regras do processamento convencional.* 
**`processamentoZbin tmp.tmp`**

Os comandos **`processamentoZ`** e **`processamentoZbin`** englobam e automatizam os comandos **`dnff`** e **`tranmt`**. 


### Outras informações

* Como alguns dados apresentam inversão de polaridade, recomenda-se realizar o processamento Z para checar o comportamento da curva dos tensores Zxy e Zyx, que em teoria deve ser majoritariamente positivo e negativo, repectivamente.
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/Processamento/curvas%20by%20EMTF/ig001_pol_inv.png' width=500 >

* Após o processamento, se checado que o comportamento das curvas não estão consonantes com a teoria, deve-se verificar na caderneta se existe algum comentário referente aquela aquisição.

* Havendo ou não comentários no relatório de campo, proceda a mudança de polaridade nos **eletrodos**, modificando os sinais nos fatores de ganho do Ex e Ey nos arquivos .sp referente a banda. 

* Após avaliação das polaridades via modificação do sinal do eletrodo, é necessário veificar se o tipper tem o mesmo comportamento em estações vizinhas. A mudança de polaridade pode estar associada a problemas na bobina também.
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/Processamento/curvas%20by%20EMTF/ig001zss.png' width = 500 >

* Após acertada a polaridade, procederíamos fazer a análise das séries temporais, mas comando egb2tss só aceita arquivo.asc, essa parte fica não pode ser realizada.
Por isso passamos para avaliação das melhores curvas selecionando os pontos por periodo.

* O tojone permite selecionar melhores resultados entre diferentes bandas (ex: TS3, TS4...)
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/Processamento/tojones/ig001.png' width=500>


### Arquivo .clk

Os programas do Egbert (dnff, tranmt, rfemi rfasc) exigem um arquivo clock. 
Caso não seja gerado automaticamente, tal arquivo pode ser criado dando as seguintes informações:

+ **.5              --> taxa de amostragem em segundos [1]**
+ **04 9 7 12 57 56 --> tempo de inicio da contagem    [2]**
+ **04 9 7 12 57 56 --> Tempo de ínicio da medição do primeiro arquivo [3]**


Como retirar essas informações do header:

### Exemplo de Header

- DATA FILE:04I0051.TS4 
- VERSIONID: MTACQ 2.00
- DATE TIME: _*20040907*_ _*12:57:56*_ --> **[2]**
+ SURVEY ID:BRAZIL                        
- SURVEY CO:OSS                            
- CLIENT CO:OSS                            
- OPERATOR :ARTUR             
- AREA     :BAHIA                  
- REMOTE   :NAO                           
- WEATHER  :GOOD                           
- COMMENT 1: ALUVIUM 
- COMMENT 2:                    
- NO OF SI : 1 
- NO OF CH : 5 
- EXT CLOCK:OFF (HERE IS THE PROBLEM, WE NEED THIS INFORMATION, EXT CLOCK SHOULD BE **ON**)
- POWERLINE: 60
- SITE    1:SITE 1                 
- CHANEL  1:Ex-1 EF-9010X 0     (928823,453092,260   )60dB23
- CHAEXT  1: 99     30dB LF OUT 190R -9.8 
- CHANEL  2:Ey-1 EF-9010Y 90    (0     ,0     ,0     )60dB23
- CHAEXT  2: -49    30dB LF OUT 410R -7.7 
- CHANEL  3:Hx-1 BF4-0479 0     (0     ,0     ,0     )40dB 7
- CHANEL  4:Hy-1 BF4-9923 90    (0     ,0     ,0     )50dB15
- CHANEL  5:Hz-1 BF7-9010 0     (0     ,0     ,0     )50dB15
- DATA TYPE:TSTS (2i10,3f10.5,i10) (i2)
- PARAMETER:        10        10    1.0000   94.0000  _512.0000_  **[1]**     512
- DATA VALUE

A informação **[3]** é referente ao inicio da aquisição, deve ser levado em consderação o inicio da aquisição, ou seja, **[3]** é a data e o horário da primeira sondagem.


Importante para a reformatação usando o rfemi.


nohup processamentoZbin teste.txt > output.txt
