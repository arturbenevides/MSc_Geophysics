# Processamento de dados MT (EMI)
@Benevides


**Etapas para processamento robusto dos dados MT (adquiridos com o equipamento da EMI) utilizando o pacote EMTF (Egbert e Eisel, 1998) e as otimizações propostas pelo pacote processamentoZ (Marcelo Banik).**


## Diretórios pasta modelo:
>* /raw_data/MTxxx: 04Ixx.TSx; 04IxxTSX.clk  *(pastas contendo os dados brutos .TS e os arquivos cloks .clk)*
>* /sensor:   *(Pastas contendo os arquivos de sensores do equipamento)*
>* /DATA :  04I0xx_tsx.bin ; .err ; .log *(contém o binário reformatado e os arquivos com erro e o log)*
>* /SP : 04I0XX_TSX.sp        *(arquivos de parâmetros do sistema, referente ao equipamento de aquisição)*
>* /FC00128 : 04I0XX_TSX.f5   *(coeficientes de fourier para janela 128)*
>* /MT0128 : 04I0XX_TSX.zss   *(funções de transferência .zss utilizando janela 128)*
>* /tojones : igxxx.dat; .png ; .ps *(funções de transferênciano no formato jones - com pontos escolhidos); 

## Procedimentos:

#### Conversão TS - BIN
**`emi2egb rawdata/MT001/04I001.TS4 001 2004-06-04T09:20:00`**
* *Esse comando permite a conversão do dado do formato .TS para .bin (padrão para o EMTF), os dados convertidos são alocados para as pastas DATA e SP, mesmo os dados estando em uma subpasta em raw data.*
* *001 é a pasta onde contém os arquivos da estação 001.*
* *2004-06-04T09:20:00 é a data e o horário definido para primeira estação*. Esse horário pode ser atribuído para todas as estações, mesmo que tenha sido definido um horário de aquisição para cada banda nos arquivos clock. Essa metodologia é utilizada para single station. Para referência remota o procedimento é diferente.*

### Processamento
**`echo "04I001_TS4.bin janela ss" > tmp.tmp`**  

ou

**`echo "04I0XX_TSX.bin janela ss;bsX" > tmp.tmp`**
* *o comando echo "--"> .temp cria um arquivo temporário que é usado pelo próximo comando.*
* *bsX permite usar outras níveis de decimação, quando chama outros arquivos options.cfg.*

**`processamentoZbin tmp.tmp`**
* *O processamento recebe o arquivo temp contendo o nome do arquivo e a janela*

O comando **`processamentoZbin`** engloba os comandos **`dnff`** e **`tranmt`**. Os produtos são as funções de transferência armazenadas na pasta MTXXX. 



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
