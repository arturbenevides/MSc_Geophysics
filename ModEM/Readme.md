**Rotina para modelagem e inversão.**


## 3D grid

Entrar com os dados, criar modelo, baixar topografia e/ou batimetria, certificar que cada estação está ocupando apenas uma célula.
> Salvar o modelo.

> Salvar o modelo reduzido

> Salvar os arquivos de covariância se houver modificações de resistividade ou suavização.

> Salvar os dados no formato ModEM

> Salvar os dados sintéticos

## ModEM

### Forward Modelling
* basic

`../ModEM -F input_model input_data output_response_model`

* Advanced

`../ModEM -F input_model input_data output_response_model` **`output_E_solution FWD_parameters`**

Output_E_solution (Binary format)
Is a file in which we store the electric field components (Ex, Ey, Ez) at all cell edges for all periods and both polarization,
is necessary to perform later e.g., the nested modeling.

FWD_para (ASCII format)
An Ascii file in which we define parameters that control the solver 
It contains the name of Output_E_solution which will be used for the nested modeling.


### Inversion

