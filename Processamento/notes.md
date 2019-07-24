# EMTF / ProcessamentoZ

Egbert&Eisel / Marcelo Banik

O objetivo do EMTF é fazer a estimativa robusta de funções transferência, neste caso os tensores de impedância.
O módulo utilizado para fazer a estimativa do tensor é o `tranmt`(para levantamento com estações simples) e `multmtrn` (para levantamentos multiplas estações).

Os módulos de estimativa do tensor pedem como parâmetros de entrada os coeficientes de Fourier (cf) que são os parâmetros de saída do programa `dnff`, responsável por cálcular os coeficientes para determinado janelamento de amostras. 

O `dnff`precisa que os dados estejam em um formato binário ou asc padrão do EMTF. Se os dados estiverem em outro formato é necessário que sejam feitas conversões.
O EMTF disponibiliza dois módulos de conversão: `rfemi` (para o sistema EMI-MT1) e `rfasc` (para arquivo ascii simples).
Além desses temos o `ats2asc`para arquivos .ats (ex. ADU) e lemi2egb para aquivos arquivo .t (ex. lemi).



## rfemi

Esse módulo reformata arquivos em formato EMI (MT1) para o binário padrão do EMTF.

>**Input**: arquivos.TS e arquivo.clk ([descrição](https://github.com/arturbenevides/Magnetotelurico/blob/master/Processamento/clock.md))
(é necessário ter os arquivos de calibração do equipamento)

>**Output**: arquivo.bin (binário) e arquivo.sp 

### Comandos
(O exevutável geralmente está na pasta bin) 
O comando é o **`rfemi`**. 
O executável irá solicitar:
Código com 3 caracteres para estação (Id da estação); Nome do arquivo TS; Nome do arquivo de saida BIN; Nome do arquivo CLK
E um pequeno header

>*Caso ainda não esteja instalado, tente: `make rfemi` -> `make install`--> `make clean`

## lemi2egb

Esse comand reformata arquivos em formato EMI (MT1) para o binário padrão do EMTF.

>**Input**: arquivos.TS e arquivo.clk ([descrição](https://github.com/arturbenevides/Magnetotelurico/blob/master/Processamento/clock.md))
(é necessário ter os arquivos de calibração do equipamento)

>**Output**: arquivo.bin (binário) e arquivo.sp 

### Comandos
(O exevutável geralmente está na pasta bin) 
O comando é o **`rfemi`**. 
O executável irá solicitar:
Código com 3 caracteres para estação (Id da estação); Nome do arquivo TS; Nome do arquivo de saida BIN; Nome do arquivo CLK
E um pequeno header

>*Caso ainda não esteja instalado, tente: `make rfemi` -> `make install`--> `make clean`



#
## dnff

Esse módulo faz os cálculos dos coeficientes de fourier para cada banda de frequência e inclui um esquema de decimação em cascata.

>**Input**: arquivos.bin  e arquivo.sp

>**Output**: CFs (coeficientes de fourier organizados por frequência) 

### Comandos
O comando é o **`dnff`**

>*Caso ainda não esteja instalado, tente: `make dnff`-> `make install` -> `make clean` 

#
## tranmt

Esse módulo faz a estimativa robusta do tensor de impedância.

>**Input**: CFs 

>**Output**: TFs (arquivo com as funções transferência) e cov (erro e covariancias)

### Comandos
O comando é **`tranmt`**

>*Caso ainda não esteja instalado, tente: `make tranmt` -> `make install` -> `make clean`

#
## ats2asc

Uma das vias mais comuns de processamento de daos magnetotelúrico utilizando o EMTF  é utilizando dados armazenados em arquivos em formato ats.
Apenas com o comando **`ats2asc`** podemos converter os dados para o formato asc e proceder diretamente para o dnff e tranmt.

Rotina de Marcelo Banik (INPE):

arquivos necessários: .asc, .clk, .sp, .txt

o arquivo .txt contém: ESTAÇÃO / JANELA-FREQUENCIA / Tipo de processamento (ss ou rr).

o comando para obter os tensores : **`processamentoZ *.txt`**







### Transformada de Fourier

Inicialmente, as séries temporais passarão por um processo de janelamento, em que os dados são divididos em pacotes com número definido de amostras. A transformada de Fourier é feita individualmente para cada um desses pacotes, ou janelas, de dados.
Alguns arquivos de entrada com parâmetros dos sensores e arquivos de controle do programa são necessários. Ao final dessa etapa são gerados os coeficientes de Fourier (FC - Fourier coefficients) ordenados por frequência para cada uma das *i* janelas de dado das *j* estações. Todo este processo é realizado utilizando o programa `dnff`.

Para calcular os coeficientes de Fourier utiliza-se uma mistura de decimação em cascata e transformada rápida de Fourier descrita em Egbert e Booker (1986). Inicialmente, usam-se janelas pequenas de dados para calcular os coeficientes de Fourier
da maior frequência desejada (decimação de nível 1). Para obter os coeficientes de Fourier para frequências mais baixas, de modo mais eficiente, os dados são submetidos à um filtro digital passa-baixa. Os dados filtrados são então divididos em novas janelas e a transformada de Fourier é novamente aplicada. Essa etapa é a decimação de nível 2. Esse processo de filtragem e janelamento pode ser repetido quantas vezes for desejado. No entanto, o tamanho da janela escolhida deve conter o mínimo de amostras necessárias para obter a resolução desejada no domínio da frequência, isto é, deve-se respeitar a frequência de Nyquist para amostragem do sinal.



#
As rotinas dos códigos utilizados são descritas em detalhes em Egbert e Booker (1986), Egbert
e Livelybrooks (1996) e Egbert (1997).


# ProcessamentoZ - ats files
Pasta Modelo 
* Descompactar 
1. tar xf ~/google Drive/modelo.tar.xz

* Mover o conteúdo da pasta modelo para pasta teste (Se preciso testar algo)
> mv -i modelo teste

*obs: não sei ainda o que significa o (i)*

2. Colocar os sensores na pasta SENSORS

3. Conversão de formato

> ats2asc --site-name \local\arquivo.ats

ou 

4. Processamento Z

Cria um arquivo para receber o nome das estações,  janela e se é ss ou rr

> echo '\*.512H.asc 1024 ss' > tmp.tmp  (arquivo temporário para ser usado no processamentoZ, entregrará todas os aquivos com final 512H)

> processamentoZ tmp.tmp

5. Egbert para TS (verificar as séries temporais e cortar trechos ruidosos)

> egb2tss file.asc

gera um --> file.sec no dietório DATA

> plotTS file.sec

Para eliminar trechos ruidosos deve se selecionar o trecho:

> cat file.sec 2004-04-10T09 2004-04010T09:30:00

Se quiser eliminar toda série a partir de um ponto:

> cat file.sec 2004-04-10T09 end

formato das horas:
yyyy-mm-dd-Thh:mm:ss

> sec2bad file.sec file.sel > file.bad

* Tem que criar a pasta BAD e guardar o file.bad

Na hora do processamento Z 

> echo 'file.asc; bd 128 ss' (no caso do EMI, tem que trocar a extensão asc por bin).

6. TOJONES (Permite selecionar melhores resultados entre diferentes run)
Um arquivo txt deve ser criado para infrormar os trechos que devem ser selecionado.

EX:
file1 [1 - 6] file2 [1 - 6] file3 [1 - 6]
file2 [1 - 8] file3

Nesse txt acima o tojones entenderá que você quer dos 6 primeiros pontos ([1 -6]) pegar informações das curvas (Zxx, Zxy e Tzx, Tzy) do arquivo file1 e informações das curvas (Zyx, Zyy) do file2.
O restante dos pontos da curva [1-8] ele irá utilizar todas as curvas do file2. 

*dica: digite >tojone para mais informações*

> echo "file1 [1 - 6] file2 [1 - 6] file3 [1 - 6]\nfile2 [1 - 8] file3" > selecao.txt

> tojone \local\selecao.txt > dado_selecionado.dat

dado_selecionado.dat -> aqruivo zss no formato jones


7. RHOPLUS

> Z2rhoplus file.dat cmp=xy ef=5 > PASTA/file.comp

* *obs: o file.dat vem do tojones, cmp é referente as componentes, o rhoplus só sabe lidar com XY e YX, e não com XX ou YY. talvez funcione com file.edi, não foi testado.

> rhoplus < arquivo

> plot-rhoplus arquivo.fsp

8. j2edi

> j2edi.py file.dat > file.edi


# ProcessamentoZbin - emi files

Pasta Modelo 

* Descompactar 

1. tar xf ~/google Drive/modelo.tar.xz

> emi2egb local\file.TS id time

ex:

> emi2egb MT001\04i001.TS 001 2004-09-06T10:56:24

Automaticamente cria um file.bin na pasta DATA, além de file.err e file.log
E cria um file.sp na pasta SP.

2. Processamento Z EMI

> echo 'file.bin 128 ss' > tmp.tmp

> processamentoZbin tmp.tmp

Se tiver problema de segmentação (core Dumped)

> echo 'file.bin 128 ss;bs4' > tmp.tmp

O sinal (;) permite usar o arquivo options00128bs4.cfg que é uma variação do options00128.cfg que contém até a quinta decimação, ou seja bs5.

3. Visualizar

> plot-cmp-tf file.zss

> plot-cmp-tf shift=180,0 file.zss  (para inverter a fase no gráfico).

#  Processamento EMTF padrão

> echo "file.asc 128 ss" > tmp.tmp

> proxessamentoZ tmp.tmp

1. transformação mais decimação 

> dnff00256  (gerar o processamentoZ primeiro para gerar o path.cfg abrir e alterar de asc para bin)

! Um problema pode acontecer devido a decimação, por exemplo - paa decimação 5 os dados estão falhando. Em options dentro de CF00128 ou outro CF00 qualquer tem escrito no arquivo a opção: bs5bla.cfg (referente a 5 decimações. Cada decimação é referente 4 períodos, bs4 = 16 períodos)

O output estará guardado em FC00256 OU FC00128 ou em outra, depende da janela (128, 256.. )

2. Transferfunction

> tranmt00256

pede o arquivo tranmt.bat

> tranmt.bat:

> arquivo.bin

> options.cfg

> 1

> 1  5

> file.f5

> n

# Comandos extras:

> cat file.txt (visulizar no terminal)

> mv -i file (transferir arquivo)
> mv -i pasta1 pasta2 (cópia conteudo de uma pasta para outra, a outra pasta deixa de existir.)

> cp -avr pasta1/* pasta2 (cópia todo conteudo de uma pasta para outra, inclusive pastas)
> cmp file1 file2 (Compara arquivos)

> plot-cmp-tf file1 file2 (plotar zss no gráfico, quantos arquivos quiser.

> less file (visualiza arquivo no terminal)

> emacs file (visualiza arquivo e permite edição)

> echo " frase a ser inserida no arquivo, (\n) serve para quebrar linhas" > tmp.tmp (cria um txt com nome tmp e com extensão qulquer para armazenar a frase enre aspas) - ( aspas simples o echo faz exatamente o que ta escrito, aspas duplas pode ser utilizada como o programa quiser).

> echo " nova frase para o aqruivo tmp" >> tmp.tmp (o sinal do >> permite adicionar informações no arquivo tmp.tmp sem sobreescrever)

> which transferfuncion  ( which busca, no caso, vai buscar transferfuncions)

> grep rsp SP/* ( grep busca string em arquivos, nesse caso, o grep vai buscar o string rsp nos arquivos na pasta SP)

> man make ( pode visualizar informações do manual sobre o make, pode-se tentar ls ou outros.)

> ctrl+shft+v (copiar)

> diff file1 file2 (diferencia informações e dois arquivos)

> cd (volta a pasta raíz)

> ls -1 PASTA/file (lista o arquivo nesta pasta, se ele estiver)

> ls -1 Pasta\*/\*TS4   (listar todos os arquivos que tenham terminação TS4 e estejam nas pasta que começam com MT)

> rm  (exclui arquivo)

> rm -r (exclui pasta)

> history | grep info (para buscar no histórico algo que tenha digitado e  que contenha a palavra );

> ls | w -lc (conta a quantidade de arquivos na pasta)



# INFOS

* Decimação: é uma reamostragem
Pode ser utilizada para alcancar períodos maiores no dado. (Observando sempre a minima frequência de amostragem, nyquist)

* Quanto maior a janela [128], [256], [1024] .. maior ou melhor é a resolução.

* Para frequencia de amostragem igual a 32 usou-se uma janela de 128
* Para frequência de amostragem igual a 512 usou-se uma janela de 1024

* trnmt00256 ou tranmt00128 etc.. são os comandos utilizados no processamentoZ, pois já estão configuradaos para os tamanhos das janelas. Se usar tranmt00256 é obrigatório usar também o dnff00256. Se não tiver utilizando o processamentoZ, ou seja, apenas o EMTF, pode ser utilizado o comando tranmt, mas deve se configurar as opções de janelamento.

* chopper on e off - opções utilizadas para aumento de ganho em baixas frequencias (abaixo de 512);

* Os dados zss deve ficar na pasta final

* O rhoplus serve para caso 2D

* é melhor deixar as barras de erros grandes, pois isso é melhor para inversão não prestar nesses pontos.

* O rhoplus é bom para recuperar ponots na resistividade se esses pontos na fase estiver de boa qualidade.

* O clock, sp e bin deve ter o mesmo nome para facilita o processamento

* Arquivo proc_sjk001a.log é uma colinha para o processamento com um passo a passo.

* Cada número de decimação são referentes a 4 períodods, 4 decimações é igual a 16 pontos de períodos na curva, por exemplo.

* Devido ao problema na inversão da fase. foi necessário editar os arquivos de parâmetros (file.sp) para que a impedância esteja correta. Para os eletrodos foi trocado o sinal nos ganhos. (primeira coluna do EX e do EY).

* É necessário inverter os eletrodos ou bobinas caso os valores de impedancia em Zyx não sejam negativos e os de Zxy não sejam positivos.

* O tipper não tem muita relação com a polaridade das bobinas e dos eletrodos. para verificar se tudo está em é aconselhado olhar as estações vizinhas, se tiver o mesmo comportamento, então está correto.

* Se o Zxx for o espelho Zyy , ou seja, se for o inverso a região é 2D.

* Soma dos traços da matriz XX com YY é constante. No 2D a componente xx=0 e como XX= - YY, XX+YY=0.



# Técnica do Rhoplus

ordem no aqrquivo:

periodo  resistividade  erro  fase  erro  0 1
periodo  resistividade  erro  fase  erro  0 1
periodo  resistividade  erro  fase  erro  0 1
periodo  resistividade  erro  fase  erro  0 1

0 significa que esse ponto não esta selecionado
1 significa que esse ponto está selecionado

O que ser faz é colocar 0 e pontos ruidosos para o rhoplus fazer a estimativa da curva sem esse ponto, se baseando nas infomações da fase.

#

## Arquivo .clk

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



