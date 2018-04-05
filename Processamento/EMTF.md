# EMTF

O objetivo do EMTF é fazer a estimativa robusta de funções transeferência, neste caso os tensores de impedância.
O módulo utilizado para fazer a estimativa do tensor é o `tranmt`(para levantamento com estações simples) e `multmtrn` (para levantamentos multiplas estações).

Os módulos de estimativa do tensor pedem como parâmetros de entrada os coeficientes de Fourier (cf) que são os parâmetros de saída do programa `dnff`, responsável por cálcular os coeficientes para determinado janelamento de amostras. 

O `dnff`precisa que os dados estejam em um formato binário padrão. Se os dados estiverem em outro formato é necessário que seja feita uma conversão. O EMTF disponibiliza dois módulos de conversão: `rfemi` (para o sistema EMI-MT1) e `rfasc` (para arquivo ascii simples).



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


As rotinas dos códigos utilizados são descritas em detalhes em Egbert e Booker (1986), Egbert
e Livelybrooks (1996) e Egbert (1997).

### Transformada de Fourier

Inicialmente, as séries temporais passaram por um processo de janelamento, em que os dados s~ao divididos em pacotes com número definido de amostras. A transformada de Fourier é feita individualmente para cada um desses pacotes, ou janelas, de dados.
Alguns arquivos de entrada com parâmetros dos sensores e arquivos de controle do programa são necessários. Ao final dessa etapa são gerados os coeficientes de Fourier (FC - Fourier coefficients) ordenados por frequência para cada uma das i janelas de dados
das j estações. Todo este processo é realizado utilizando o programa `dnff`.

Para calcular os coeficientes de Fourier utiliza-se uma mistura de decimação em cascata e transformada rápida de Fourier descrita em Egbert e Booker (1986). Inicialmente, usam-se janelas pequenas de dados para calcular os coeficientes de Fourier
da maior frequência desejada (decimação de nível 1). Para obter os coeficientes de Fourier para frequências mais baixas, de modo mais eficiente, os dados são submetidos à um filtro digital passa-baixa. Os dados filtrados são então divididos em novas janelas e a transformada de Fourier é novamente aplicada. Essa etapa é a decimação de nível 2. Esse processo de filtragem e janelamento pode ser repetido quantas vezes for desejado. No entanto, o tamanho da janela escolhida deve conter o mínimo de amostras necessárias para obter a resolução desejada no domínio da frequência, isto é, deve-se respeitar a frequência de Nyquist para amostragem do sinal.
