
Grid produzido assumindo espaçamento correto baseado no skin depht e respeitando o espaço dos paddings cells
## Grid técnico 

Item \ direction  |     X       |   y        |     Z
------------------|:-----------:|:----------:|:----------:
N of cell         |   110       |  90        |   88 *         
Cell dimension    |   745       |  500       |   2          
N of padding cells|   11        |   11       |            
increasing Factor |   1.3       |   1.3      |   1.1   

* Colocar um número de células para alcancar no máximo 100 km.

* Padding cells: A escolha desse parâmetro tem que ser de acordo com o tamanho do perfil.
Podemos separar o grid em dois meios. o meio refinado onde estão as estações e o meio dos paddings cells que serve para respeitar as condições de frontreiras e evitar os efeitos de borda.

* Podemos fazer um cálculo usando o skin depth para saber o tamanho do meio do paddings cells. Este meio é contado a partir do final do meio refinado até o fim do grid. 

* Devemos obter um meio refinado que abranja todas as estações, por isso o número de celeluas pode variar nas direções e não serem iguais.

* O fator de crescimento só passa a valer após o espaço do grid refinado, antes da contagem do padding cells. A ideia é que os blocos comecem a ficar maiores no espaço dos paddings cells.



# 
### Rough grid 1

Item \ direction  |     X       |   y        |     Z
------------------|:-----------:|:----------:|:----------:
N of cell         |    57       |   64       |   35         
Cell dimension    |   750       |  750       |   50         
N of padding cells|    11       |   11       |  ~~-~~         
increasing Factor |     1.2     |    1.2     |   1.2          

### Rough grid 2

Item \ direction  |     X       |   y        |     Z
------------------|:-----------:|:----------:|:----------:
N of cell         |   70        |  70        |   20         
Cell dimension    |   500       |  500       |   50         
N of padding cells|   18        |     18     |            
increasing Factor |   1.2       |   1.2      |   1.2          

### finer grid

Item \ direction  |     X       |   y        |     Z
------------------|:-----------:|:----------:|:----------:
N of cell         |   100       |  95        |   67         
Cell dimension    |   300       |  300       |   5         
N of padding cells|   25        |   25       |            
increasing Factor |   1.2       |   1.2      |   1.2     

### Combined grid

Item \ direction  |     X       |   y        |     Z
------------------|:-----------:|:----------:|:----------:
N of cell         |   70        |  70        |   30 *         
Cell dimension    |   500       |  500       |   5          
N of padding cells|   11        |   11       |            
increasing Factor |   1.2       |   1.2      |   1.2   


### Combined grid2

Item \ direction  |     X       |   y        |     Z
------------------|:-----------:|:----------:|:----------:
N of cell         |   70        |  70        |   86 *         
Cell dimension    |   500       |  500       |   2          
N of padding cells|   11        |   11       |            
increasing Factor |   1.2       |   1.2      |   1.1   

* Colocar um número de células para alcancar no máximo 100 km.
