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

Uma grande quantidade de informações úteis pode ser extraída de um conjunto de dados por meio de sua análise ou exploração. Uma das formas mais simples de explorar um conjunto de dados é a extração de medidas de uma área da estatística denominada estatística descritiva. A estatística descritiva resume de forma quantitativa as principais características de um conjunto de dados. As medidas da estatística descritiva assumem que os dados são gerados por um processo estatístico. Essas medidas permitem capturar informações como:
- Frequência;
- Localização ou tendência central (por exemplo, a média);
- Dispersão ou espelhamento (por exemplo, o desvio padrão);
- Distribuição ou formato.

A medida de frequência é a mais simples. Ela mede a proporção de vezes que um atributo assume um dado valor em um determinado conjunto de dados. Um exemplo seria: em um conjunto de dados médicos, 40% dos pacientes tem febre.
As outras medidas diferem para os casos em que os dados apresentam apenas um atributo (dados univariados) ou mais de um atributo (dados multivariados) e são geralmente aplicadas a dados numéricos. Apesar de a maioria dos conjuntos de dados utilizados em AM apresentar mais de um atributo, análises realizadas em cada atributo podem oferecer informações valiosas.

#### Dados Univariados

**Medidas de Localização**: As medidas de localidade definem pontos de referência nos dados e variam para dados numéricos e categóricos. Para dados categóricos, utiliza-se geralmente a moda, que é o valor encontrado com maior frequência para um atributo. Para atributos numéricos, medidas muito utilizadas são média, mediana e percentil.

Um problema da média é a sua sensibilidade à presença de *outliers*. Média é um bom indicador do meio de um conjunto de valores apenas se os valores estão distribuídos simetricamente. Um valor muito mais alto ou muito mais baixo que os demais valores do conjunto pode gerar um valor distorcido para a média, que poderia mudar radicalmente se for retirado o *outlier*. Esse problema é minimizado com o uso da mediana, que é menos sensível a *outliers*. 

Existem ainda variações da média e da mediana, como, por exemplo, a média truncada, que minimiza os problemas da média por meio do descarte dos exemplos nos extremos da sequência ordenada dos valores. Para isso, é necessário definir a porcentagem dos exemplos a serem eliminados em cada extremidade.

Outras medidas muito utilizadas são os quartis e os percentis. Assim como a mediana, essas medidas são utilizadas após os valores serem ordenados. Enquanto a mediana divide os dados ao meio, essas outras medidas utilizam pontos de divisão diferentes. Os quartis dividem os valores ordenados em quartos (quatro partes). Assim, o 1° quartil de uma sequência é o valor que tem 25% dos demais valores abaixo dele. Esse também é o valor do 25° percentil. O 2° quartil é a mediana, que é igual ao 50° percentil. Por fim, o 3° quartil corresponde ao valor que tem 75% dos demais valores abaixo dele.

**Medidas de Dispersão**: As medidas de espalhamento medem a dispersão ou espalhamento de um conjunto de valores. Assim, elas permitem observar se os valores estão amplamente espalhados ou relativamente concentrados em torno de um valor, por exemplo, a média. As medidas de espalhamento mais comuns são:
- Intervalo;
- Variância;
- Desvio padrão.

O intervalo é a medida mais simples e mostra o espalhamento máximo entre os valores de um conjunto (valor máximo subtraído do valor mínimo). Se a maioria dos valores for próxima de um ponto, com um pequeno número de valores extremos, o intervalo não será uma boa medida do espalhamento dos valores. 

A medida mais utilizada para avaliar o espalhamento de valores é a variância. Outra medida de espalhamento, o desvio padrão, é dada pela raiz quadrada da variância. Assim como a média, o valor da variância poder ser distorcido pela presença de *outliers*, pois a variância calcula a diferença entre cada valor e a média. 

Outras estimativas mais robustas de espalhamento frequentemente utilizadas são: desvio médio absoluto (*absolute average deviation*), desvio mediano absoluto (*median absolute deviation*) e intervalo interquartil (*interquartil range* ou IQR). 

**Medidas de Distribuição**: As medidas que são definidas em torno da média de um conjunto de valores, como as medidas média e desvio padrão, são em sua maioria instanciações de uma medida denominada **momento**.

$momento_k (x^j) = \sum_{i=1}^{n} (x_i - \bar{x}^j)^k / (n-1)$ 

Para cada valor do parâmetro *k*, uma medida diferente do momento é definida. Assim:
- quando k = 1, tem-se o valor 0, que é o primeiro momento em torno da origem ou primeiro momento central;
- quando k = 2, tem-se a variância, que é o segundo momento central;
- quando k = 3, tem-se a obliquidade (*skweness*), que é o terceiro momento central;
- quando k = 4, tem-se a curtose (*kurtosis*), que é o quarto momento central.

O terceiro e quarto momentos, obliquidade e curtose, são medidas de distribuição, por mostrarem como os valores estão distribuídos. O terceiro momento, obliquidade (em inglês *skweness*), mede a simetria da distribuição dos dados em torno da média. Em uma distribuição simétrica, se os valores forem distribuídos em intervalos do mesmo tamanho, um histograma com a quantidade de valores em cada intervalo tem a mesma aparência à direita e à esquerda do ponto central. 

A distribuição dos valores em um conjunto de dados está associada ao valor da obliquidade da seguinte forma:
- obliquidade = 0 (simétrica): a distribuição é aproximadamente simétrica (ocorre para uma distribuição normal);
- obliquidade > 0 (positiva): a distribuição concentra-se mais ao lado esquerdo;
- obliquidade < 0 (negativa): a distribuição concentra-se mais ao lado direito.

![[Pasted image 20241003091222.png]]

O quarto momento calcula a curtose (em inglês *kurtosis*), que é uma medida de dispersão que captura o achatamento da função de distribuição. Assim como na medida de obliquidade, a seguinte relação, é observada entre o valor da curtose e a distribuição dos valores em um conjunto de dados:
- curtose = 0 (normal): o histograma de distribuição dos dados apresenta o mesmo achatamento que uma distribuição normal;
- curtose > 0 (positiva): o histograma de distribuição dos dados apresenta uma distribuição mais alta e concentrada que a distribuição normal;
- curtose < 0 (negativa): o histograma de distribuição dos dados apresenta uma distribuição mais achatada que a distribuição normal.
![[Pasted image 20241003091618.png]]

#### Dados Multivariados
Dados multivariados são aqueles que possuem mais de um atributo de entrada. Nesses casos, as medidas de localidade podem ser obtidas calculando a medida de localidade para cada atributo separadamente. As medidas de espalhamento também podem ser calculadas para cada atributo independentemente dos demais utilizando qualquer medida de espalhamento. 

Dados multivariados permitem ainda análises da relação entre dois ou mais atributos. Por exemplo, para atributos quantitativos, o espalhamento de um conjunto de dados é mais bem capturado por uma matriz de covariância, em que cada elemento é a covariância entre dois atributos. 

A covariância entre dois atributos mede o grau com que os atributos variam juntos. Seu valor depende da magnitude dos atributos. Um valor próximo de 0 indica que os atributos não tem um relacionamento linear. Um valor positivo indica que os atributos são diretamente relacionados, enquanto o contrário ocorre se o valor for negativo.

A medida de covariância é afetada pela escala de variação de valores dos atributos avaliados. Assim, dois atributos com variação de valores elevada (por exemplo, na escala dos milhares) podem apresentar um valor de covariância maior que dois atributos mais semelhantes entre si, mas de menor variação de valores (por exemplo, na escala entre 0 e 1). Por isso, não é possível avaliar o relacionamento entre dois atributos observando apenas a covariância entre eles.

A medida de **correlação** elimina esse problema retirando a influência da variação dos valores. Como resultado, ela apresenta uma indicação mais clara da força da relação linear entre dois atributos. Por isso, a correlação é mais utilizada para explorar dados multivariados que a covariância. A matriz de correlação apresenta a correlação entre cada possível par de atributos de um conjunto de dados.

Assim como na medida de covariância, quando dois atributos apresentam uma correlação positiva, o aumento do valor de um deles é geralmente acompanhado por um aumento no valor do outro. Da mesma forma, quando dois atributos tem uma correlação negativa, a redução no valor de um deles é geralmente acompanhada do aumento do valor do outro.

A análise dos dados multivariados também pode ser facilitada pelo uso de recursos de visualização. Assim como histogramas, gráficos de pizza e boxplots são utilizados para visualizar dados univariados, outros diagramas tem sido adotados para visualizar dados multivariados, particularmente a relação entre os diferentes atributos. Entre estes diagramas, um dos mais utilizados é o *scatter plot*, que ilustra a correlação linear entre dois atributos.

Em um *scatter plot*, a cada objeto, considerando apenas dois dos seus atributos, é associado uma posição ou ponto em um plano bidimensional. Os valores dos atributos definem as coordenadas desse ponto. 

![[Pasted image 20241004091824.png]]