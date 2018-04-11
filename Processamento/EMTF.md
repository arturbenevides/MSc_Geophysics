# EMTF / ProcessamentoZ

Gary Egbert

Marcelo Banik

O objetivo do EMTF é fazer a estimativa robusta de funções transferência, neste caso os tensores de impedância.
O módulo utilizado para fazer a estimativa do tensor é o `tranmt`(para levantamento com estações simples) e `multmtrn` (para levantamentos multiplas estações).

Os módulos de estimativa do tensor pedem como parâmetros de entrada os coeficientes de Fourier (cf) que são os parâmetros de saída do programa `dnff`, responsável por cálcular os coeficientes para determinado janelamento de amostras. 

O `dnff`precisa que os dados estejam em um formato binário padrão. Se os dados estiverem em outro formato é necessário que seja feita uma conversão. O EMTF disponibiliza dois módulos de conversão: `rfemi` (para o sistema EMI-MT1) e `rfasc` (para arquivo ascii simples) e `ats2asc`(para arquivos ats).



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


# SEQUÊNCIA ATS2ASC
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


5. TOJONES (Permite selecionar melhores resultados entre diferentes run)
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


6. RHOPLUS

> rhoplus < arquivo

> plot-rhoplus arquivo.fsp




#  Processamento sem o ProcZ automático


1. transformação mais decimação 

> dnff00256  (gerar o processamentoZ primeiro paa gerar o path.cfg e outras arquivos de opções)
! Um problema pode acontecer devido a decimação, por exemplo - paa decimação 5 os dados estão falhando. Em options dentro de CF00128 ou outro CF00 qualquer tem escrito no arquivo a opção: bs5bla.cfg (referente a 5 decimações. Cada decimação é referente 4 períodos, bs4 = 16 períodos)

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
> mv -i pasta1 pasta2 (cópia conteudo de uma pasta para outra)

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

>





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
