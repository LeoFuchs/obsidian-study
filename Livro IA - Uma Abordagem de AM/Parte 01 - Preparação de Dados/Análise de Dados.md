A análise das características presentes em um conjunto de dados permite a descoberta de padrões e tendências que podem fornecer informações valiosas para compreender o processo que gerou os dados. Mutas dessas características podem ser obtidas por meio da aplicação de fórmulas estatísticas simples. Outras podem ser observadas usando técnicas de visualização.
### Caracterização de Dados

Considere um conjunto de dados provenientes de pacientes de um hospital:

| Id.  | Nome    | Idade | Sexo | Peso | Manchas      | Temp. | # Int. | Est. | Diagnóstico |
| ---- | ------- | ----- | ---- | ---- | ------------ | ----- | ------ | ---- | ----------- |
| 4201 | João    | 28    | M    | 79   | Concentradas | 38,0  | 2      | SP   | Doente      |
| 4039 | Luiz    | 49    | M    | 92   | Espalhadas   | 38,0  | 2      | RS   | Saudável    |
| 2301 | Ana     | 22    | F    | 72   | Inexistentes | 38,0  | 3      | RJ   | Doente      |
| 4340 | Cláudia | 21    | F    | 52   | Uniformes    | 37,6  | 1      | PE   | Saudável    |
Os valores que um atributo pode assumir podem ser definidos de diferentes formas. Aqui serão definidos dois aspectos: tipo e escala. O tipo de um atributo diz respeito ao grau de quantização dos dados, enquanto a escala indica a significância relativa dos valores.

#### Tipo: 
O tipo define se o atributo representa quantidades, sendo então denominado quantitativo (ou numérico) ou então qualidades, denominado como qualitativo (ou categórico).== Exemplos de conjuntos de valores qualitativos são {pequeno, médio e grande}, enquanto para valores quantitativos seriam {23, 45, 12}. 
Note ainda que valores quantitativos podem ser **contínuos** ou **discretos**. Valores contínuos podem assumir um número infinito de valores, frequentemente representados por números reais. Exemplos clássicos são peso, tamanho e distância. Por outro lado, atributos discretos contém um número finito de valores. Um caso especial dos atributos discretos são os atributos binários (ou booleanos), que apresentam apenas dois valores, como 0 ou 1.

Sendo assim, os atributos da nossa tabela com os pacientes de um hospital possuem as seguintes classificações:

| Atributo    | Classificação         |
| ----------- | --------------------- |
| Id.         | Qualitativo           |
| Nome        | Qualitativo           |
| Idade       | Quantitativo discreto |
| Sexo        | Qualitativo           |
| Peso        | Quantitativo contínuo |
| Manchas     | Qualitativo           |
| Temp.       | Quantitativo contínuo |
| # Int.      | Quantitativo discreto |
| Est.        | Qualitativo           |
| Diagnóstico | Qualitativo           |

#### Escala
A escala define as operações que podem ser realizadas sobre os valores do atributo. Em relação à escala, os atributos podem ser classificados como **nominais, ordinais, intervalares e racionais.** Os dois primeiros são para valores qualitativos (nominais e ordinais), enquanto os dois últimos são para valores quantitativos (intervalares e racionais).

Na escala **nominal**, como o nome sugere, os valores são apenas nomes diferentes, carregando a menor quantidade de informação possível. Não existe uma relação de ordem entre seus valores. Assim, as operações mais utilizadas são as de igualdade ou desigualdade de valores. 
	Exemplos: nome, RG, CPF, número da conta do banco, CEP, cores, sexo.

Os valores de uma escala **ordinal**, como o nome sugere, refletem também uma ordem das categorias representadas. Dessa forma, além dos operadores de igualdade e desigualdade, operadores como maior, menor, maior igual e menor igual podem ser utilizados. 
	Exemplos: hierarquia militar e avaliações qualitativas de temperatura, como frio morno e quente.

Na escala **intervalar**, os atributos são representados por números que variam dentro de um intervalo. Assim, é possível definir tanto a ordem quanto a diferença em magnitude entre dois valores. 
	Exemplos: duração de um evento em minutos e datas em um calendário.

Atributos com a escala **racional** são os que carregam mais informações. Os números tem um significado absoluto, ou seja, existe um zero absoluto junto com uma unidade de medida, de forma que a razão tenha significado.
	Exemplos: tamanho, distância e valores financeiros, como salário e saldo em conta.

Sendo assim, os atributos da nossa tabela com os pacientes de um hospital possuem as seguintes classificações:

| Atributo    | Classificação |
| ----------- | ------------- |
| Id.         | Nominal       |
| Nome        | Nominal       |
| Idade       | Racional      |
| Sexo        | Nominal       |
| Peso        | Racional      |
| Manchas     | Nominal       |
| Temp.       | Intervalar    |
| # Int.      | Racional      |
| Est.        | Nominal       |
| Diagnóstico | Nominal       |

### Exploração de Dados

