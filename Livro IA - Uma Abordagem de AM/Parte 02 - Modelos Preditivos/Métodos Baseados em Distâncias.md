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

Métodos baseados em distância, como o algoritmo dos vizinhos mais próximos, tem seu desempenho afetado pela medida ou função de distância utilizada. Um problema de medida de distância euclidiana está em pressupor que os dados correspondem a pontos no espaço dimensional, ou seja, que seus atributos são numéricos. Contudo, diversos problemas possuem dados com atributos qualitativos. Neste caso, os atributos qualitativos devem ser primeiramente convertidos em valores quantitativos ou uma medida de distância heterogênea pode ser empregada, sem necessidade de conversão prévia de valores.

Outro aspecto que deve ser observado no cálculo da distância entre objetos é a escala utilizada para os valores dos atributos. Por exemplo, qual o efeito na função distância da representação de um atributo em centímetros ou quilômetros? As medidas de distância são afetadas pela escala dos atributos. Para minimizar esse efeito, os atributos são usualmente normalizados.

#### O Algoritmo k-NN

Uma extensão imediata do algoritmo 1-NN é considerar, em vez de um vizinho mais próximo, os *k* objetos do conjunto de treinamento mais próximos do ponto de teste, em que *k* é um parâmetro do algoritmo. Quando o valor de *k* é maior que 1, para cada ponto de teste, são obtidos *k* vizinhos. Cada vizinho vota em uma classe. As previsões dos diferentes vizinhos são agregadas de modo a classificar o ponto de teste. Essa agregação é efetuada de forma diferente em problemas de classificação e regressão.

Em problemas de classificação, em que a classe toma valores em um conjunto discreto, cada vizinho vota em uma classe. O objeto de teste é classificado na classe mais votada (moda). Em problemas de regressão, podem ser utilizadas duas estratégias, dependendo da função de custo usada. Se a função de custo for minimizar o erro quadrático, a média dos valores obtidos para cada um dos *k* vizinhos deve ser utilizada. Se a função de custo a ser minimizada for o desvio absoluto, em vez da média, deve ser utilizada a mediana. 

Para facilitar o entendimento, considere a figura abaixo. Para *k = 3*, o objeto de teste seria classificado como classe B, enquanto para *k = 7*, o objeto de teste seria classificado como pertencendo à classe A.
![[Pasted image 20241021085135.png]]
A escolha do valor *k* mais apropriado para um problema de decisão específico pode não ser trivial. O valor de *k* é definido pelo usuário. Frequentemente, o valor de *k* é pequeno e ímpar (3, 5, ...). Em problemas de classificação com duas classes, não é usual utilizar *k = 2* ou valores pares, para evitar empates.

Duas estratégias referidas na literatura consistem em:
- Estimar *k* por validação cruzada;
- Associar um peso à contribuição de cada vizinho.

Nesse último caso, a contribuição de cada um dos *k* vizinhos é ponderada de forma inversamente proporcional à distância ao ponto de teste. Assim, é possível utilizar *k = n*, onde *n* são todos os objetos de treinamento. 
#### Análise do Algoritmo

**Aspectos Positivos**: O algoritmo k-NN representa um dos paradigmas mais conhecidos do aprendizado indutivo: *objetos com características semelhantes pertencem ao mesmo grupo.* O k-NN é um algoritmo baseado em memória, ou um algoritmo preguiçoso, porque toda a computação é adiada até a fase de classificação, já que o processo de aprendizado consiste apenas em memorizar objetos.
- O algoritmo de treinamento é simples (armazenar objetos apenas).
- O k-NN constrói aproximações locais da função objetivo, diferentes para cada novo dado a ser classificado.
- Ele é aplicável mesmo em problemas complexos.
- O algoritmo é naturalmente incremental: quando novos exemplos de treinamento estão disponíveis, basta armazená-los na memória. 

**Aspectos Negativos**: Também por ser um algoritmo preguiçoso (*lazy*), o algoritmo dos vizinhos mais próximos não obtém uma representação compacta dos objetos. De fato, não se tem um modelo explícito a partir dos dados. A fase de treinamento requer pouco esforço computacional. No entanto, classificar um objeto de teste requer calcular a distância desse objeto a todos os objetos de treinamento. Assim, a predição pode ser custosa, e para um conjunto grande de objetos de treinamento esse processo pode ser demorado. Como todos os algoritmos baseados em distâncias, ele é afetado pela presença de atributos redundantes e irrelevantes.

Outro problema do k-NN está relacionado com a dimensionalidade dos exemplos. O espaço definido pelos atributos de um problema cresce exponencialmente com o número de atributos, ou seja, o número de atributos define o número de dimensões do espaço. O ponto que está mais perto de outro pode estar muito distante em problemas de alta dimensionalidade. A dimensionalidade de um problema pode afetar de forma negativa o desempenho dos algoritmos baseados em distâncias. Uma das formas de reduzir o impacto da dimensionalidade de um problema consiste em selecionar um subconjunto de atributos relevantes para o problema tratado.
#### Desenvolvimentos

Uma grande parte dos trabalhos de pesquisa relacionados com o algoritmo k-NN investiga a redução do espaço do problema. Já foi salientado que o k-NN é um algoritmo lento no processo de classificação de exemplos de teste. Uma das possibilidades para minimizar esse inconveniente consiste em obter um subconjunto de exemplos representativos. Por exemplo, eliminando objetos redundantes, ou eliminando objetos em que todos os vizinhos são da mesma classe. Outra possibilidade consiste em eliminar objetos com ruído, por exemplo, eliminando objetos em que todos os vizinhos são de outra classe.

Alguns autores apresentaram vários algoritmos para selecionar os objetos mais relevantes, designados por protótipos, para o problema de aprendizado, de forma a reter em memória apenas esses objetos. As versões do algoritmo Edit k-NN para eliminação e inserção sequencial são dois exemplos de algoritmos que armazenam apenas protótipos. No primeiro caso, o algoritmo começa com todos os objetos e vai descartando os objetos que são corretamente classificados pelo conjunto de protótipos. No segundo, o conjunto de protótipos começa vazio. Os objetos que são incorretamente classificados pelo conjunto de protótipos são acrescentados a esse conjunto.
#### Raciocínio Baseado em Casos

Raciocínio baseado em casos (RBC) é uma metodologia de AM para a resolução de problemas fundamentada na utilização de experiências passadas. Assim, um sistema de RBC procura resolver um novo problema apresentado por meio da recuperação de problemas similares previamente solucionados de uma memória ou base de casos (BC) e adaptação da solução utilizada no problema recuperado para resolver o novo problema.

RBC difere de outros paradigmas de AM nos seguintes aspectos:
- Enquanto outros paradigmas utilizam conhecimento geral do domínio ou constroem relações entre problemas e soluções, RBC é capaz de utilizar conhecimento específico de problemas vistos anteriormente.
- RBC possibilita de forma natural o aprendizado incremental, pela atualização da BC sempre que um novo problema é resolvido, tornando o novo conhecimento disponível para futuro uso.

O desempenho de um sistema de RBC depende da estrutura e conteúdo de sua base de casos. Para a construção de uma base de casos, é necessário decidir o que armazenar em um caso, encontrar uma estrutura apropriada para descrever o conteúdo dos casos e definir como os casos devem ser organizados e indexados, para possibilitar a recuperação rápida e a reutilização eficaz de soluções anteriores.

Um caso pode representar diferentes tipos de conhecimento e assumir distintas formas de representação. Uma forma simples de representar casos é por meio de um conjunto de pares atributo-valor. Esse conjunto é dividido em dois subconjuntos. O primeiro possui os atributos que descrevem o problema e o segundo, os atributos relacionados com sua solução. Por exemplo, podemos ter um RBC que escolhe pacotes de viagens. Então, a descrição recebe o ambiente desejado, a duração, a região do país e uma estimativa de custo. Por sua vez, a solução do problema apresenta um local, um transporte sugerido, a acomodação ideal e onde fazer as refeições.

Um modelo frequentemente utilizado para descrever as etapas de um sistema RBC é o ciclo de RBC. Esse ciclo compreende quatro etapas principais:
- **Recuperação**: recuperação do caso armazenado na BC mais similar ao novo problema apresentado.
- **Reutilização**: adaptação da parte de solução do caso recuperado. A solução do problema recuperado é geralmente utilizada como ponto de partida para propor uma solução para o novo problema. Essa etapa também é denominada adaptação de casos.
- **Revisão**: a solução adaptada é revisada pelo usuário para validar sua relevância para resolver o novo problema.
- **Retenção**: caso, após a etapa de revisão, a solução adaptada seja considerada relevante, o novo problema, junto com essa solução, pode ser armazenado na BC.


