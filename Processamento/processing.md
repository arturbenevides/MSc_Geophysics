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

**`echo "04I001.asc janela rr;04I00Ref.asc" > tmp.tmp`**

* Concluído o processamento, são gerados arquivos mas pastas FC** e MT** (** diz respeito as janelas utilizadas no proessamento). Próximo passo é gerar as curvas para avaliação da qualidade do dado e possivel emprego de filtros pré-processamento.
* >  plot-cmp-tf stn01.zss ps=stn01.ps

## Miscelânia

### Séries temporais
Caso o processamento não tenha dado um bom resultado e o problema da estimativa esteja ligada a trechos ruins nas séries temporais, pode-se osbservar e remover trechos ruins da série.

**`egb2tss 04ig001.asc`**
* *gera um 04ig001.sec no dietório DATA, esse comando tem que ser dado a partir da pasta modelo mas, não requer endereçar o arquivo, pois ele subentende que o arquivo está na pasta DATA.*
* *Para verificar a série temoporal, dentro da pasta data:*

**`plot-ts file.sec`**
* *Para eliminar trechos ruidosos deve se selecionar o trecho:*

**`cat file.sec 2004-04-10T09 2004-04010T09:30:00 > file.sel`** 
* *Nesse caso estamos elimina 30 minutos de medida, entre 9:00 e 9:30 de um determinado dia.*
* *Se quiser eliminar toda série a partir de um ponto:*

**`cat file.sec 2004-04-10T09 end > file.sel`**

* *formato das horas: yyyy-mm-dd-Thh:mm:ss*

* *Para o processamento esse trecho selecionado é armazenado em um arquivo .bad que deve ter o mesmo nome do arquivo .asc ou .bin que será processado**

**`sec2bad file.sec file.sel > 04ig001.bad`**
* *Uma pasta chamada BAD tem que ser criada pra guardar o file.bad*
* *Na hora do processamento:* 

**`echo 'file.asc;bad 128 ss' > tmp.tmp`**

* O comando egb2tss só aceita arquivo.asc, portanto, não podemos verificar a série ainda para o caso dos equipamento EMI.

### Inversão de polaridade
* Como alguns dados apresentam inversão de polaridade, recomenda-se realizar o processamentoZ para checar o comportamento da curva dos tensores Zxy e Zyx, que em teoria deve ser majoritariamente positivo e negativo, repectivamente.
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/Processamento/curvas%20by%20EMTF/ig001_pol_inv.png' width=500 >

* Após o processamento, se checado que o comportamento das curvas não estão consonantes com a teoria, deve-se verificar na caderneta se existe algum comentário referente aquela aquisição.

* Havendo ou não comentários no relatório de campo, proceda a mudança de polaridade nos **eletrodos**, modificando os sinais nos fatores de ganho do Ex e Ey nos arquivos .sp referente a banda e estação. 

* Após avaliação das polaridades via modificação do sinal do eletrodo, é necessário veificar se o tipper tem o mesmo comportamento em estações vizinhas. A mudança de polaridade pode estar associada a problemas na bobina também.
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/Processamento/curvas%20by%20EMTF/ig001zss.png' width = 500 >

### TOJONES

* O tojone permite selecionar melhores resultados entre diferentes bandas (ex: TS3, TS4...), ou apenas excluir pontos:

<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/Processamento/tojones/ig001.png' width=500>

Exemplo selecao.txt:
file1 [1 - 6] file2 [1 - 6] file1 [1 - 6]
file2 [1 - 8] 

Nesse selecao.txt acima o tojones entenderá que você quer dos 6 primeiros pontos ([1 -6]) pegar informações das curvas (Zxx, Zxy e Tzx, Tzy) do arquivo file1 e informações das curvas (Zyx, Zyy) do file2.
O restante dos pontos da curva [1-8] ele irá utilizar todas as curvas do file2. 

*dica: digite >tojone para mais informações*

> echo "file1 [1 - 6] file2 [1 - 6] file3 [1 - 6]\nfile2 [1 - 8] file3" > selecao.txt

> tojone \local\selecao.txt > dado_selecionado.dat

dado_selecionado.dat -> aqruivo zss no formato jones



nohup processamentoZbin teste.txt > output.txt

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.
