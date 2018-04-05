# Arquivo .clk

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
