## Observatório Nacional
@Benevides

#
##Etapas para processamento robusto dos dados MT (adquiridos com o equipamento da EMI) utilizando o pacote EMTF (Egbert e Eisel, 1998) e as otimizações propostas pelo pacote processamentoZ (Banik).


**Na pasta modelo encontramos os diretórios:**
>* /raw_data/MTxxx: 04Ixx.TSx; 04IxxTSX.clk  *(pastas contendo os dados brutos .TS e os arquivos cloks .clk)*
>* /sensor:   *(Pastas contendo os arquivos de sensores do equipamento)*
>* /DATA :  04I0xx_tsx.bin ; .err ; .log *(contém o binário reformatado e os arquivos com erro e o log)*
>* /SP : 04I0XX_TSX.sp        *(arquivos de parâmetros do sistema, referente ao equipamento de aquisição)*
>* /FC00128 : 04I0XX_TSX.f5   *(coeficientes de fourier para janela 128)*
>* /MT0128 : 04I0XX_TSX.zss   *(funções de transferência .zss utilizando janela 128)*
>* /tojones : igxxx.dat; .png ; .ps *(funções de transferênciano no formato jones - com pontos escolhidos); 

## Procedimentos:

#### ex:
**`emi2egb rawdata/MT001/04I001.TS4 001 2004-06-04T09:20:00`**
* *Esse comando permite a conversão do dado do formato .TS para .bin (padrão para o EMTF), os dados convertidos são alocados para as pastas DATA e SP, mesmo os dados estando em uma subpasta em raw data.*

**`echo "04I001_TS4.bin janela ss" > tmp.tmp`**  
* *o comando echo cria um arquivo temporário que será usado pelo próximo comando.*
ou

**`echo "04I0XX_TSX.bin janela ss;bsX" > tmp.tmp`**
* *bsX permite usar outras níveis de decimação, quando chama outras arquivos options.cfg.*

**`processamentoZbin tmp.tmp`**
* *O processamento recebe o arquivo temp contendo o nome do arquivo e a janela*
