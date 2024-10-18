A seguir serão apresentadas técnicas de AM (Aprendizado de Máquina) que consideram a proximidade entre os dados na realização de predições. A hipótese base é que dados similares tendem a estar concentrados em uma mesma região no espaço de entrada. De maneira alternativa, dados que não são similares estarão distantes entre si.

Um método baseado em distância utilizado com frequência é o **algoritmo dos vizinhos mais próximos**. Esse algoritmo é o mais simples de todos os algoritmos de AM. A intuição por trás do algoritmo é: **objetos relacionados com o mesmo conceito são semelhantes entre si**.

O algoritmo dos vizinhos mais próximos classifica um novo objeto com base nos exemplos do conjunto de treinamento que são próximos a ele. É um algoritmo preguiçoso, porque não aprende um modelo compacto para os dados, apenas memoriza os objetos de treinamento. Uma vantagem desse algoritmo é que ele pode ser utilizado tanto em problemas de classificação como em problemas de regressão de maneira direta, sem necessidade de alterações significativas.

Ao longo deste arquivo, apresentaremos a descrição do funcionamento do algoritmo dos vizinhos mais próximos utilizando o caso mais simples, apenas um vizinho. Depois, apresentamos o algoritmo k-NN, que é analisado posteriormente. Variações recentes desenvolvidas para o algoritmo k-NN são apresentadas em seguida. Por fim, apresentamos uma metodologia de AM que utiliza distância para recuperar a solução de problemas passados que sejam similares ao problema que se deseja resolver, conhecida como raciocínio baseado em casos.

#### O Algoritmo do 1-Vizinho Mais Próximo

O algoritmo dos vizinhos mais próximos tem variações definidas pelo número de vizinhos considerados. Dessas variações, a mais simples é o algoritmo 1-vizinho mais próximo (1-NN). Neste algoritmo, cada objeto representa um ponto em um espaço definido pelos atributos, denominado espaço de entrada. Definindo uma métrica nesse espaço, é possível calcular as distâncias entre cada dois pontos. A métrica mais usual para isso é a distância euclidiana.

O algoritmo 1-NN está ilustrado no código abaixo. Na fase de treinamento, o algoritmo memoriza os exemplos rotulados do conjunto de treinamento. Para classificar um exemplo não rotulado, ou seja, cuja classe não é conhecida, é calculada a distância entre o vetor de valores de atributos e cada exemplo rotulado em memória. O rótulo da classe associado ao exemplo de treinamento mais próximo do exemplo de teste é utilizado para classificar o novo exemplo.


**Entrada**: Um conjunto de treinamento $D = {(x_i, y_i), i = 1, ..., n}$
Um objeto de teste a ser classificado: $t = {x_t, y_t = ?}$
A função de distância entre objetos: $d(x_a, x_b)$
**Saída:** $y_t$: Classe atribuída ao exemplo $t$

1  $d_{min} = +\infty$
2  para cada $i \in 1, ..., n$ faça:
3      se $d(x_a, x_b) < d_{min}$ então
4           $d_{min} = d(x_a, x_b)$
5           $idx = i$
6  fim
7  $y_t = y_{idx}$
8  Retorna: $y_t$

Métodos baseados em distância....





#### O Algoritmo k-NN


#### Análise do Algoritmo


#### Desenvolvimentos


#### Raciocínio Baseado em Casos


