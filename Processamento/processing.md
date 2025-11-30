# Processamento de dados MT (ADU/EMI/LEMI)
Benevides, 2018.

**Etapas para processamento robusto dos dados MT u tilizando o pacote EMTF (Egbert e Eisel, 1998) e as otimizações propostas pelo pacote processamentoZ (Marcelo Banik).**


## Diretórios pasta modelo:
>* /raw_data/MTxxx: stn1.ats; stn1.clk  *(pastas contendo os dados brutos .TS, .T ou .ATS e os arquivos cloks .clk)*
>* /sensor:   *(Pastas contendo os arquivos de sensores do equipamento)*
>* /DATA :  stn1 (.asc, .bin) ; .err ; .log *(contém os dados em asc ou em binário reformatado, além dos arquivos com erro e o log)*
>* /SP : stn1.sp        *(arquivos de parâmetros do sistema, referente ao equipamento de aquisição)*
>* /FCXXXX : stn1.f5   *(armazenam os coeficientes de fourier por janelas, ex: FC00128)*
>* /MTXXXX : stn1.zss  *(armazenam as funções de transferência .zss por jannelas, ex: MT00128)*
>* /tojones : stn1.dat; .png ; .ps *(armazenam as funções de transferência no no formato jones); 

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

**`ats2asc --site-name *nome* rawdata/STN001/`**

* *Esse comando deve ser dado dentro da pasta modelo apontando a pasta que contem os arquivos ats. Os arquivos .asc convertidos serão armazenados na pasta DATA.*
* nome: deve ser substituido por um nome referente a estação


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

**`echo "04I001.asc janela ss;bsX" > tmp.tmp`**
* *bsX permite usar outras níveis de decimação, quando chama outros arquivos options.cfg.*

* *O processamento para os arquivos (.bin) da EMI utiliza o comando `processamentoZbin`, mas segue as mesmas regras do processamento convencional.* 
**`echo "04I001_TSX.bin janela ss;bsX" > tmp.tmp`**
**`processamentoZbin tmp.tmp`**
[Mais detalhes](https://github.com/arturbenevides/MSc_Geophysics/blob/master/Processamento/campanha_iguatu_relat%C3%B3rio_de_processamento.md)

Os comandos **`processamentoZ`** e **`processamentoZbin`** englobam e automatizam os comandos **`dnff`** e **`tranmt`**. 

### Referência remota (rr)
* *Na referência remota dois parâmetros são modificados/incluidos, o ss passa ser rr e devemos informar qual estação será utilizada como referência remota.*

Na pasta DATA/RR localmente executar o comando:

**`./make-clk-log ../*128H.clk > files_128rr.log`**
* Esse comando vai gerar um log com os tempos de aquisição de cada estação.
* O comando abaixo permite visualizar a superposição temporal das estações

**`./plot-clock files_128rr.log`**

* O comando a seguir refaz o clock para as outras estações permitindo o uso na referencia remota.
* novos arquivos clk (clock) referentes aos arquivos antigos que tem superposição.
* 
**`./make-clk-rr files_128rr.log`**

#### novamente na pasta principal, o esquema de processamento com referência remota pode ser aplicado.

**`echo "04I001.asc janela rr;04I00Ref.asc" > tmp.tmp`**

* Concluído o processamento, são gerados arquivos mas pastas FC** e MT** (** diz respeito as janelas utilizadas no proessamento). Próximo passo é gerar as curvas para avaliação da qualidade do dado e possivel emprego de filtros pré-processamento.
* >  plot-cmp-tf stn01.zss ps=stn01.ps


### Conversão para edi:
Necessário criar um arquivo de seleção dos períodos existentes em cada janela processada. No caso de um único arquivo como no processamento de LP, todos os pontos podem ser considerados.

Exemplo selecao.txt arquivo com apenas uma janela de processaento:
     Zfile1 [1 - 24] #line 1

Exemplo de seleção de arquivo com mais de uma janela de processamento
      Zfile  [1-10] # line 1
      ZxFile [1-6] ZyFile [11-16] TipperFile [1-6] # line 2
  - line 1 seleciona os primeiros 10 períodos of de todo tensor e tipper do arquivo Zfile
  - line 2 seleciona os primeiros 6 períodos do aqrquio Z1File e TipperFile e 11 até o 16
  do arquivo ZyFile

**`echo "file1 [1 - 24]" > stn.sel`**

**`toedi \local\stn.sel`**
Um arquivo edi será gerado automaticamente com o nome do arquivo de seleção "stn" com a extensão edi.

## Miscelânia
# Controle de qualidade das séries temporais
### Visualizar séries temporais
Caso o processamento não tenha dado um bom resultado e o problema da estimativa esteja ligada a trechos ruins nas séries temporais, pode-se osbservar e remover trechos ruins da série.

**`egb2tss 04ig001.asc`**
* *gera um 04ig001.sec no dietório DATA, note que para versões antigas esse comando precisa ser dado a partir da pasta modelo mas, não requer endereçar o arquivo, pois ele subentende que o arquivo está na pasta DATA.*
* *Para verificar a série temoporal, dentro da pasta data:*

**`plot-ts file.sec`**
* *opçoes  de plots seguem usando apenas `plot-ts`.
* *Para eliminar trechos ruidosos deve se selecionar o trecho da seguinte forma:*

**`echo '2022-07-08T22:00 2022-07-09T22:00'   > file.sel`** 
* *Nesse caso, estamos selecionando 30 minutos de medida, entre 9:00 e 9:30 de um determinado dia e encaminando isso para um arquivo qualquer, varios trechos podem ser selcionados e armazenados sempre em duas colunas*
  
* *Se quiser eliminar toda série a partir de um ponto:*

**`echo '2004-04-10T09:00:00 end' > file.sel`**

* *Ou se precisar desconsiderar a parte inicial até determinado ponto:*
  
**`echo 'begin 2004-04-10T09:00' > file.sel`**

* *formato da data e hora: yyyy-mm-dd-Thh:mm:ss*
* obs: se não funcionar a remoção pode ter relação com a presença dos segundos, remover e deixar só minutos. 

* *Para o processamento, esse trecho selecionado deve ser armazenado em um arquivo .bad a partir do arquivo .sec, o mesmo .bad deve ter o mesmo nome do seu .asc ou .bin que será processado. O comando sec2bad faz a extração na série temporal do trecho selecionado** 

**`sec2bad file.sec file.sel > 04ig001.bad`**

* *Uma pasta chamada /BAD deve ser criada dentro da pasta central (Modelo) pra guardar o file.bad*
* *Na hora do processamento deve se alterar os termos de entrada na seguinte forma:* 

**`echo 'file.asc;bad 128 ss' > tmp.tmp`**

* O comando egb2tss só aceita arquivo.asc, portanto, não podemos verificar a série ainda para o caso dos equipamento EMI.

* Verficação de superposição:
*   Dentro da pasta /DATA/RR

**`./make-clk /*128H.clk > files.log`**
* Esse comando vai gerar um arquivo contendo os tempos em que as estaçõe estiveram funcionando.
* O comando abaixo permite visualizar a superposição temporal das estações
**`./plot-clock file.log`**

### Inversão de polaridade
* Como alguns dados apresentam inversão de polaridade, recomenda-se realizar o processamentoZ para checar o comportamento da curva dos tensores Zxy e Zyx, que em teoria deve ser majoritariamente positivo e negativo, repectivamente.

* Após o processamento, observando que o comportamento das curvas não estão consonantes com a teoria, deve-se verificar na caderneta se existe algum comentário referente aquela aquisição.

* Havendo ou não comentários no relatório de campo, proceda a mudança de polaridade nos **eletrodos**, modificando os sinais nos fatores de ganho do Ex e Ey nos arquivos .sp referente a banda e estação. 

* Após avaliação das polaridades via modificação do sinal dos canais, é necessário verificar se o Tipper tem o mesmo comportamento em estações vizinhas. A mudança de polaridade pode estar associada a problemas na bobina também.


### TOJONES

* O tojone permite selecionar melhores resultados entre diferentes bandas (ex: TS3, TS4...), ou apenas excluir pontos:

Exemplo selecao.txt:
file1 [1 - 6] file2 [1 - 6] file1 [1 - 6]
file2 [1 - 8] 

Nesse selecao.txt acima o tojones entenderá que você quer dos 6 primeiros pontos ([1 -6]) pegar informações das curvas (Zxx, Zxy e Tzx, Tzy) do arquivo file1 e informações das curvas (Zyx, Zyy) do file2.
O restante dos pontos da curva [1-8] ele irá utilizar todas as curvas do file2. 

*dica: digite >tojone para mais informações*

**`echo "file1 [1 - 6] file2 [1 - 6] file3 [1 - 6]\nfile2 [1 - 8] file3" > selecao.txt`**

**`tojone \local\selecao.txt > dado_selecionado.dat`**

dado_selecionado.dat -> aqruivo zss no formato jones

#### RhoPlus

* O rhoplus ajuda a verificar a coerencia entre a amplitude da resistividade aparaente e fase usando o qui2

1. step

**`Z2rhoplus file.dat cmp=xy ef=5 > fileoutxy.dat`**

**`Z2rhoplus file.dat cmp=yx ef=5 > fileoutyx.dat`**

É necessário fazer para as componentes xy e yx separadamente.
ef é o erro tolerável. 

file.dat deve estar no formato jones.

2. step

**`rhoplus < fileoutxy.dat`**

arquivos de saida xy_fileoutxy.rsp e xy_fileoutxy.rsp

**`plot-rhoplus xy_fileoutxy.rsp`**

* Na figura os pontos preenchidos estão sendo considerados para o cálculo da curva teórica, no arquivo fileoutyx é possivel controlar os pontos que são considerados. A penultima coluna é da resistividade e a ultima é referente a fase.

3. step/

**`rsp2Zjones file_original.dat xy.rsp yx.rsp > file_out_R+.dat`**

a ordem xy.rsp e yx.rsp deve ser mantida.
#

#### Conversão para EDI

*`j2edi.py stn01.dat > stn01.edi`*

nohup processamentoZbin teste.txt > output.txt

########### tips
Segmentation fault no processamento pode indicar que algum canal tem um valor espúrio muito fora de escala que esteja atrapalhando o processamento.

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.
