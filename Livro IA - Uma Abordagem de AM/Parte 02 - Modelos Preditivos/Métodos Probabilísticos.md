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