# ModEM - Modular System for Electromagnetic Inversion 
Benevides, A.

**Rotina prática para modelagem e inversão .**
(Egbert and Kelbert, 2012; Kelbert et al., 2014).

## 3D grid
Interface gráfica utilzada para geração de arquivos modelo, dado e covariância no formato do ModEM, além de auxiliar na visualização dos resultados.

### Passos iniciais:
1. Importar os dados .edi ou .dat (ModEM) 
2. Criar modelo, definir parâmetros do grid: 
 * resistividade do semi-espaço;
 * n. de células nas direções x e y;
 * dimensão das células x e y;
 * n. de células de preenchimento e fator de crescimento;
 * n. de células em Z;
 * esperssura da primeira camada e fator de crescimento.
 
3. Após a criação do modelo é necessário certificar se cada estação está ocupando apenas uma célula:
 *TOOLS> Center all Station > In X,Y and Z directions*;

4. Incluir topografia e/ou batimetria:
 *TOOLS> TOPO/Bathymetry > From SRTM ou Load TOPO/Batrymetry from XYZ File*
 
5. Se o dado foi adquirido próximo a costa é necessário incluir o efeito do oceano
 *TOOLS >  ADD Sea sediment Layers > Cell wise and Thikness-wise* 

6. Após definição dos parâmetros do grid, deve-se:
>* Salvar o modelo: FILE > save model > Full Model (modelo completo);
>* Salvar o modelo reduzido (nested model): FILE > save model > Displayed Model.  Essa função permite otimizar a inversão, é uma boa opção para modelos muito grande,  ;
>+ Salvar o arquivo de covariância, se houver modificações de resistividade (criação de modelo a priori) ou suavização;

7. Dados: Os dados podem ser verificados em View/Edit Data
Opções possíveis para os dados: Mascarar pontos indesejados, Interporlar e Rotacionar.

8. Salvar os dados no formato ModEM .dat: 
*FILE> Save Data > EM Modular System > All sites.*
Opções:
Off diagonal, Full Impedance, Tipper, Phase Tensor etc..
Error setting:
Use Data Error; 
Set Error Floors: escolher a porcentagem de erro e o método de cálculo. 
Use periods layout

## ModEM

### Forward Modelling
* basic

`../ModEM -F input_model input_data output_Resp_large_model`

* Advanced

`../ModEM -F input_model input_data output_Resp_large_model` **`output_E_solution FWD_parameters`**

Output_E_solution (Binary format)
Is a file in which we store the electric field components (Ex, Ey, Ez) at all cell edges for all periods and both polarization,
is necessary to perform later e.g., the nested modeling.

FWD_para (ASCII format)
An Ascii file in which we define parameters that control the solver 
It contains the name of Output_E_solution which will be used for the nested modeling.

* Run the forward modelling for the nested model:

`../ModEM –F nested_model data_file Resp_large_model e_solution_tmp FWD_para`

*At the some point after executing ModEM to run the forward modelling or the inversion with nested modelling enabled (e_solution file name is inside FWD_para file)*

### Inversion

* Basic Input/Output
`../ModEM –I NLCG Input_Model Input_Data`
 
* Advanced-level1
`../ModEM -I NLCG Input_Model Input_data Input_INV_para.`
 
* Advanced-level2
`../ModEM –I  NLCG Input_Model Input_data Input_INV_para. FWD_para.`
 
* Advanced-level3
`Input_Model Input_data Input_INV_para. FWD_para. Model_Cov`
 
* Advanced-level4
`../ModEM –I  NLCG Input_Model Input_data Input_INV_para. FWD_para. Model_Cov model_prm`
 

- **Input_Model Input_data Input_INV_para.**
* Example: Input_INV_para (ASCII Format)
Information in this file controls the inversion process
Each line has an explanation of what are these information for:

>- Model and data output file name : ModEM3DMT;
>- Initial daming factor lambda: 1.0;
>- Restart when rms diff is less than: 2.0e-3;
>- Exit search when rms is less than: 1.05;
>- Exit when lambda is lesse than: 1.0e-8;
>- Maximun number of iterations : 100;

- **Input_Model Input_data Input_INV_para. FWD_para. Model_Cov model_prm**
To use the optional model perturbation file (model_prm) as an input we need first to understand few things:
The output files after each iteration are:  
***_NLCG_060.rho  > Inverted model   
***_NLCG_060.dat  > Predicted data 
***_NLCG_060.prm  > Transformed model parameter (rough)
***_NLCG_060.res  > Data residuals



**Para uso no clustercoge** o seguinte comando está sendo usado:

**`> srun -N [1]  -o out.txt -e out.error -n [2] --mpi=pmi2 Mod3DMT -I NLCG arq.mod arq.dat ctrl.inv ctrl.fwd arq.cov arq.prm &`**


* [1] é referente ao número de slaves que serão utilizadas para inversão. Ao todo, o cluster tem 28 slaves.
* [2] é referente ao valore resultante do = (N.Periodos x 2 ) + 1

#

miscelaneous 

comandos para converter j para modem 

j2ModEM list.txt Full_Impedance eZxx=0.2 eZyy=0.2 eZxy=0.1 eZyx=0.1 > all_data.dat
j2ModEM list.txt Full_Vertical_Components >> all_data.dat
