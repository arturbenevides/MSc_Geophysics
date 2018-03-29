# MT INITIAL

Da série temporal até o modelo invertido


TS (*time series*) é um arquivo onde são armazenados os registros temporais dos campos elétricos e magnéticos adquiridos em campo. 

O processamento para estimativa do tensor de impedância é feito no domínio da frequência, por isso é necessário aplicar a Transformada de Fourier aos dados contidos na série tempora.

O passo a seguir é utilizar mínimos quadrados para estimar o tensor (Através de uma análise estatística).

Com a obtenção do tensor de impedância procede se a o cálculo da resistividade e fase (para cada componente do Tensor).

Objetivos:

- [ ] Arquivo para leitura de um ts
- [ ] Aplicação de transformada de fourier nos dados
- [ ] Estimativa do Tensor de Impedância
- [ ] Cálculo das resistividades
- [ ] Inversão 1D das resistividades
- [ ] Inversão 2D das resistividades
- [ ] Inversão 3D das resistividades
- [ ] Diferenças finitas visualização 2D
- [ ] Elemento finito visualização 2D
