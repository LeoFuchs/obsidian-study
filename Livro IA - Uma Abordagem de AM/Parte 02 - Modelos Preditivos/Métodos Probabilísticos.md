Outra forma de lidar com tarefas preditivas em AM, principalmente quando as informações disponíveis são incompletas ou imprecisas, é por meio do uso de algoritmos baseados no teorema de Bayes, os métodos probabilísticos bayesianos. Tais métodos assumem que a probabilidade de um evento A, que pode ser uma classe (por exemplo, um doente apresentar determinada doença), dado um evento B, que pode ser um conjunto de valores dos atributos de entrada (por exemplo, ter resultado positivo em um exame), não depende apenas da relação entre A e B, mas também da probabilidade de observar A independentemente de observar B.

A probabilidade de ocorrência do evento B pode ser estimada pela observação da frequência com que esse evento ocorre. De forma semelhante, é possível estimar a probabilidade de que um evento B ocorra, para cada classe ou evento A, P(B | A). Mas como determinar a probabilidade de ocorrência de um evento A, quando for observado um evento B, P(B | A)? No domínio de AM, essa questão pode ser traduzida em qual a probabilidade de classificar uma determinada classe (um valor de A), dados os valores dos atributos (registrados em B)? 

O **teorema de Bayes** mostra como calcular P(B | A). Ele fornece uma maneira de calcular a probabilidade de um evento ou objeto pertencer a uma classe P(B | A) utilizando a probabilidade a priori da classe, P(A), a probabilidade de observar vários objetos com os mesmos valores de atributos que pertencem à classe, P(B | A), e a probabilidade de ocorrência destes objetos, P(B).

$P(A | B) = \frac{P(B | A) P(A)}{P(B)}$ 

#### Aprendizado Bayesiano

Para exemplificar como métodos probabilísticos podem ser utilizados em AM, considere o seguinte cenário: **a probabilidade de observar alguém com dada doença é de 8%. Existe um teste para o diagnóstico dessa doença, cujo resultado possui um grau de incerteza. É sabido que em 75% dos casos em que o resultado do teste foi positivo a doença foi confirmada e que em 96% em que o resultado do teste foi negativo o paciente realmente não tinha a doença**.

A doença pode ser vista como uma variável aleatória A com dois possíveis valores: presente e ausente. O resultado do teste B também tem dois possíveis valores: positivo ou negativo. É fácil observar que o valor da doença influencia o valor do teste, mas o oposto não é verdade (fazer ou não o teste não aumenta a chance da pessoa ficar doente).

Temos então:
P(Doença = presente) = 0,08
P(Doença = ausente) = 0,92

P(Teste = positivo | Doença = presente) = 0,75 (verdadeiros positivos ou sensibilidade)
P(Teste = negativo | Doença = ausente) = 0,96 (verdadeiros negativos ou especificidade)

Qual o poder preditivo do Teste com respeito à Doença? É possível calcular as probabilidades a priori para a variável Teste. Levamdno em conta que **P(A) = P(A | B) x P(B)**, obtemos:

P(Teste = positivo) = P(Teste = positivo | Doença = presente) x P(Doença = presente) +
                 P(Teste = positivo | Doença = ausente) x P(Doença = ausente)

P(Teste = positivo) = 0,75 x 0,08 + 0,04 x 0,92 = 0,0968

P(Teste = negativo) = P(Teste = negativo | Doença = presente) x P(Doença = presente) +
                 P(Teste = negativo | Doença = ausente) x P(Doença = ausente) 

P(Teste = negativo) = 0,25 x 0,08 + 0,96 x 0,92 = 0,9032

**Considere agora que, para dado paciente, o resultado do Teste foi positivo. Podemos concluir que o paciente está doente?** No aprendizado bayesiano, o valor de uma variável aleatória tem uma probabilidade associada. A questão que devemos colocar é: qual é a probabilidade **P(Doença = presente | Teste = positivo)**?

O teorema de Bayes é usado para calcular a probabilidade a posteriori de um evento, dadas sua probabilidade a priori e a verossimilhança do novo dado. Neste exemplo, precisamos inverter a probabilidade P(Teste = positivo | Doença = presente).

Utilizando o teorema de Bayes, temos que:

$P(A | B) = \frac{P(B | A) P(A)}{P(B)}$ 

P(Doença = **presente** | Teste = positivo) = (P(Teste = positivo | Doença = presente) x P(Doença = presente) / P(Teste = positivo) = (0,75 x 0,08) / 0,09 = 0,06 / 0,09 = 0,66

e

P(Doença = **ausente** | Teste = positivo) = (P(Teste = positivo | Doença = ausente) x P(Doença = ausente) / P(Teste = positivo) = (0,92 x 0,04) / 0,09 = 0,0368 / 0,09 = 0,40

Como 0,66 > 0,40, podemos considerar que o paciente está doente.

#### Classificador Naive Bayes

Assumindo que os valores dos atributos de um exemplo são independentes entre si dada a classe $P(x | y_{i})$ pode ser decomposto no produto $P(x^{1} | y_{i}) x ... x P(x^{d} | y_{i})$, em que $x^j$ é o j-ésimo atributo do exemplo x. Com isso, a probabilidade de um exemplo pertencer à classe $y_i$ é proporcional à expressão:

$P(y_i | x) = P(y_{i})  \prod_{j=1}^{d} P(x^j | y_i)$ 

O classificador obtido pelo uso da função discriminante apresentada acima é conhecido como classificador naive Bayes. O termos naive (ingênuo) vem da hipótese de que os valores dos atributos de um exemplo são independentes de sua classe.

A fórmula do naive Bayes pode ser expressa de uma outra forma. Aplicado logaritmos à equação anterior, obtém-se:

$log(P(y_i | x)) = log(P(y_i)) + \sum{j}{} log(P(x^j | y_i))$

**Detalhes da Implementação**

Todas as probabilidades necessárias para a obtenção do classificador naive Bayes são computadas a partir dos dados de treinamento. Para calcular a probabilidade a priori de observar a classe $y_i$, $P(y_i)$, é necessário manter um contador para cada classe. Para calcular a probabilidade condicional de observar o valor de um atributo dado que o exemplo pertence a uma classe, é necessário distinguir entre atributos qualitativos e atributos quantitativos.

No caso de atributos qualitativos, o conjunto de possíveis valores é um conjunto enumerável. Para calcular a probabilidade condicional, basta manter um contador para cada valor de atributo por classe. No caso de atributos contínuos, quando o número de possíveis valores é infinito, há duas possibilidades. A primeira é assumir uma distribuição particular para os valores do atributo, e geralmente é assumida a distribuição normal. A segunda alternativa é discretizar o atributo em uma fase de pré-processamento. Alguns trabalho evidenciam que a primeira alternativa produz piores resultados que a última.

Alguns autores propõem que o número de intervalos seja fixado em k = min (10, número de valores diferentes) intervalos do mesmo tamanho. Uma vez que o atributo foi discretizado, um contado para cada classe e para cada intervalo pode ser utilizado para calcular a probabilidade condicional $P(Atributo_j | Classe_j)$.

**Exemplo Ilustrativo**

Este exemplo utiliza um conjunto de dados para o problema balance. Nesse problema, cada exemplo é classificado em uma de três posições de uma balança: a balança está inclinada para a direita, para a esquerda ou sem inclinação (equilibrada ou balanceada). Os atributos são o peso do lado esquerdo, a dimensão do braço esquerdo, o peso do lado direito e a dimensão do braço direito. A forma correta para encontrar a classe é o maior valor entre: $Distância_{esq} \times Peso_{esq}$  e $Distância_{dir} \times Peso_{dir}$. Se estes valores são iguais, o estado da balança, sua classe, é balanceada.

Para esse conjunto de dados, o domínio de todos os atributos é o conjunto {1, 2, 3, 4, 5}. O conjunto de dados contém 625 exemplos, distribuídos da forma como é apresentado na tabela abaixo. Para calcular as probabilidades a priori, $P(Classe_i)$, é necessário contar o número de exemplos para cada classe.

|           | Balanceada | Esquerda | Direita |
| --------- | ---------- | -------- | ------- |
| Contagem  | 49         | 288      | 288     |
| P(Classe) | 0,078      | 0,461    | 0,461   |

Para calcular a probabilidade condicional de observar um valor específico de atributo dada a classe, $P(Atributo_j | Classe_j)$, é necessário descobrir o tipo do atributo. Nesse problema, todos os atributos são numéricos, pois dizem respeito a distâncias e pesos. Pode-se assumir que seu domínio é um conjunto de números reais. Sem mais nenhuma informação, a hipótese mais razoável é que eles são normalmente distribuídos. Considerando essa hipótese, para estimar as probabilidades condicionais, é preciso calcular a média e o desvio padrão dos valores dos atributos para cada classe.

Como alternativa, pode-se discretizar os atributos. Nesse problema, aplicando a regra k = min (10; número de atributos diferentes), são obtidos cinco intervalos. A tabela abaixo apresenta a distribuição de valores para cada atributo em cada classe.


| $Peso_{esq}$      | V = 1 | V = 2 | V = 3 | V = 4 | V = 5 |
| ----------------- | ----- | ----- | ----- | ----- | ----- |
| Balanceada        | 10    | 11    | 9     | 10    | 9     |
| Esquerda          | 17    | 43    | 63    | 77    | 88    |
| Direita           | 98    | 71    | 53    | 38    | 28    |
| $Distância_{esq}$ | V = 1 | V = 2 | V = 3 | V = 4 | V = 5 |
| Balanceada        | 10    | 11    | 9     | 10    | 9     |
| Esquerda          | 17    | 43    | 63    | 77    | 88    |
| Direita           | 98    | 71    | 53    | 38    | 28    |
| $Peso_{dir}$      | V = 1 | V = 2 | V = 3 | V = 4 | V = 5 |
| Balanceada        | 10    | 11    | 9     | 10    | 9     |
| Esquerda          | 17    | 43    | 63    | 77    | 88    |
| Direita           | 98    | 71    | 53    | 38    | 28    |
| $Distância_{dir}$ | V = 1 | V = 2 | V = 3 | V = 4 | V = 5 |
| Balanceada        | 10    | 11    | 9     | 10    | 9     |
| Esquerda          | 17    | 43    | 63    | 77    | 88    |
| Direita           | 98    | 71    | 53    | 38    | 28    |




