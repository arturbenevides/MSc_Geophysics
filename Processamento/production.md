# Processamento Z

## Campanha iguatu

Conteúdo do diretório:

* raw_data > MT001         (pastas contendo os dados brutos e os cloks)
* DATA > 04i0xx_tsx.bin, .err e .log (conté o binário reformatado e os arquivos com erro e o log)
* SP > 04I0XX_TSX.sp       (arquivos de parâmetros do sistema, referente ao equipamento de aquisição)
* FC00128 > 04I0XX_TSX.f5  (coeficientes de fourier)
* MT0128 > 04I0XX_TSX.zss   (resultados)

> `emi2egb local\04I0XX.TSX 0XX 2004-06-04T09:20:00`
O comando permite que os dados vão para pasta DATA, mesmo os dados estando em uma subpasta em raw data.

> `echo "04I0XX_TSX.bin janela ss" > tmp.tmp`  
ou
> `echo "04I0XX_TSX.bin janela ss;bsX" >tmp.tmp`
esse comando tem que ser utilizado a cada banda de processamento, pois o nome do arquivo modifica.

> `processamentoZbin tmp.tmp`
O processamento recebe o arquivo temp contendo o nome do arquivo e a janela




# Planejamento

Como alguns dados estão com inversão de polaridade, recomenda-se processar para checar o comportamento da curva dos tensores xy (deve ser majoritariamente positivo) e yx (deve ser majoritariamente negativo).

Após o processamento Z, se checado e sendo positivo a mudança de polaridade, modificar os fatores de ganho nos arquivos .sp referente a banda. 

Para inversão de polaridade referente ao eletrodos (checar as curvas), em relação as bobinas (checar o tipper).

