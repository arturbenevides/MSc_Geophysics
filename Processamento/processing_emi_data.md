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

* O tojone permite selecionar melhores resultados entre diferentes run (banda TS3, TS4...)
<img src='https://github.com/arturbenevides/MSc_Geophysics/blob/master/Processamento/tojones/ig001.png' width=500>
