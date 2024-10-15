Apesar de algoritmos de Aprendizado de Máquina (AM) serem frequentemente adotados para extrair conhecimento de conjunto de dados, seu desempenho é geralmente afetado pelo estado dos dados. Conjuntos de dados podem apresentar diferentes características, dimensões ou formatos. Podem ainda estar limpos ou conter ruídos e imperfeições, com valores incorretos, inconsistentes, duplicados ou ausentes.

Técnicas de pré-processamento de dados são frequentemente utilizadas para melhorar a qualidade dos dados por meio da eliminação ou minimização dos problemas citados. Também podem tornar os dados mais adequados para sua utilização por um determinado algoritmo de AM. Por exemplo, alguns algoritmos de AM trabalham apenas com valores numéricos.

#### Integração de Dados

Quando dados a serem utilizados em uma aplicação de AM são oriundos de diferentes fontes, estando organizados em diferentes conjuntos de dados, esses conjuntos devem ser integrados antes do início do uso da técnica de AM.  Assim, na integração, é necessário identificar quais são os objetos que estão presentes nos diferentes conjuntos a serem combinados. Esse problema é conhecido como problema de identificação de entidade.

Essa identificação é realizada por meio da busca por atributos comuns nos conjuntos a serem combinados. Como exemplo, conjuntos de dados médicos podem ter um atributo que identifica o paciente. Assim, os objetos dos diferentes conjuntos que possuem o mesmo valor para o atributo que identifica o paciente são combinados em um único objeto do conjunto integrado. Alguns aspectos podem dificultar a integração. Por exemplo, atributos correspondentes podem ter nomes diferentes em bases de dados distintas. Além disso, os dados a serem integrados podem ter sido atualizados em momentos diferentes. 

A existência de um conjunto de dados grande, tanto em termos de número de objetos como de atributos, não implica que um algoritmo de AM deva utilizar todo ele. Muitas vezes é mais eficiente usar apenas parte do conjunto original. No que diz respeito ao número de atributos, um número elevado pode comprometer o desempenho dos algoritmos de aprendizado, por fatores relacionados à maldição da dimensionalidade. 

Além disso, a relevância dos atributos para o problema que está sendo tratado também é essencial para a qualidade dos resultados. A eliminação manual desses atributos, além de garantir a qualidade dos dados a serem utilizados, também ajuda a reduzir a dimensionalidade. Com relação à quantidade de objetos (observações), problemas podem ocorrer por causa da saturação de memória e aumento do tempo computacional. Para minimizar esses problemas, podem ser utilizadas técnicas de amostragem.

#### Eliminação Manual de Atributos

Observando novamente a tabela com os dados hospitalares (apresentada abaixo), pode ser facilmente percebido que nem todos os atributos do conjunto original são necessários para o diagnóstico clínico de um paciente. Não faz sentido, por exemplo, usar os valores dos atributos *Nome* e *Id.* para o diagnóstico.

| **Id.**  | **Nome**    | Idade | Sexo | Peso | Manchas      | Temp. | # Int. | Est. | Diagnóstico |
| -------- | ----------- | ----- | ---- | ---- | ------------ | ----- | ------ | ---- | ----------- |
| ~~4201~~ | ~~João~~    | 28    | M    | 79   | Concentradas | 38,0  | 2      | SP   | Doente      |
| ~~4039~~ | ~~Luiz~~    | 49    | M    | 92   | Espalhadas   | 38,0  | 2      | RS   | Saudável    |
| ~~2301~~ | ~~Ana~~     | 22    | F    | 72   | Inexistentes | 38,0  | 3      | RJ   | Doente      |
| ~~4340~~ | ~~Cláudia~~ | 21    | F    | 52   | Uniformes    | 37,6  | 1      | PE   | Saudável    |
Existem outras situações em que um atributo irrelevante pode ser facilmente detectado. Por exemplo, um atributo que possui o mesmo valor para todos os objetos não contém informação que ajude a distinguir os objetos. Assim, ele pode ser considerado irrelevante.

#### Amostragem de Dados

Algoritmos de AM podem ter dificuldades em lidar com um número grande de objetos. Associado ao número de objetos em um conjunto de dados, existe um balanço entre eficiência computacional e acurácia (taxa de predições corretas). Quanto mais dados utilizados, maior tende a ser a acurácia do modelo e menor a eficiência computacional do processo indutivo. Para se obter um bom compromisso entre eficiência e acurácia, geralmente trabalha-se com uma amostra ou subconjunto dos dados. Muitas vezes, o uso de uma amostra leva ao mesmo desempenho obtido com o uso do conjunto completo, porém com um custo computacional muito menor.

Deve ser observado que uma amostra pequena pode não representar bem o problema que se deseja modelar. A amostra deve ser representativa do conjunto de dados original. Se as amostras não forem representativas, diferentes amostras de uma mesma população podem gerar modelos diferentes. Isso porque características importantes do problema podem não estar presentes. Por outro lado, se a amostra for muito grande, são reduzidas as vantagens de utilizá-la.

O ideal é que a amostra não seja grande, mas que seus dados obedeçam à mesma distribuição estatística que gerou o conjunto de dados original. Embora não seja possível garantir que isso aconteça, existem técnicas de amostragem estatística que aumentam as chances disso ocorrer. São elas:

- **Amostragem aleatória simples**: A amostragem aleatória simples possui duas variações: sem reposição de exemplos, em que exemplos são extraídos do conjunto original para a amostra a ser utilizada e cada exemplo pode ser selecionado apenas uma vez; e a com reposição, quando uma cópia dos exemplos selecionados é mantida no conjunto de dados original.
- **Amostragem estratificada**: A amostragem estratificada é usada quando as classes apresentam propriedades diferentes. Em problemas de classificação, um cuidado que deve ser tomado na amostragem diz respeito à distribuição dos dados nas diferentes classes. A existência de classes com uma quantidade significativamente maior de exemplos que as demais pode levar à indução de classificadores tendenciosos para as classes majoritárias. Por outro lado, pode ser que algumas classes sejam mais difíceis de classificar que outras e isso possa ser minimizado no processo de amostragem. Essa abordagem também possui variações. A mais simples delas é manter o mesmo número de objetos para cada classe (exemplo 50 objetos na classe 0 e 50 objetos na classe 1). Outra opção é manter o número de objetos em cada classe proporcional ao número de objetos da classe no conjunto original.
- **Amostragem progressiva**: A amostragem progressiva começa com uma amostra pequena e aumenta progressivamente o tamanho da amostra extraída, enquanto a acurácia preditiva continuar a melhorar. Como resultado, é possível definir a menor quantidade de dados necessária, reduzindo ou eliminando a perda de acurácia. Essa abordagem geralmente fornece uma boa estimativa para o tamanho da amostra.

#### Dados Desbalanceados

O problema de dados desbalanceados é tópico da área de classificação de dados. Em vários conjuntos de dados reais, o número de objetos varia para diferentes classes. Um exemplo seria um conjunto de dados de clientes de um banco, em que cada cliente é rotulado como tendo ou não ficado com o saldo da sua conta negativo nos últimos 90 dias. Se a porcentagem de clientes que ficou com o saldo negativo nesse período for de 5%, a classe majoritária terá 95% dos dados.

Vários algoritmos de AM tem seu desempenho prejudicado na presença de dados desbalanceados. Quando alimentados com dados desbalanceados, esses algoritmos tendem a favorecer a classificação de novos dados na classe majoritária. Técnicas que procuram balancear artificialmente o conjunto de dados podem ser utilizadas para lidar com o problema de desbalanceamento. As principais técnicas são:
- Redefinir o tamanho do conjunto de dados.
- Utilizar diferentes custos de classificação para as diferentes classes.
- Induzir um modelo para uma classe.

No primeiro caso, podem ocorrer tanto o acréscimo de objetos à classe minoritária como a eliminação de objetos da classe majoritária. Para o acréscimo de novos objetos, existe o risco de os objetos acrescentados representarem situações que nunca ocorrerão, induzindo um modelo inadequado aos dados. Além disso, pode ocorrer *overfitting*, em que o modelo é superajustado aos dados de treinamento. Quando dados são eliminados da classe majoritária, é possível que dados de grande importância para a indução do modelo correto sejam perdidos. Isso pode levar ao problema de *underfitting*, em que o modelo induzido não se ajusta aos dados de treinamento.

A utilização de custos de classificação diferentes para as classes majoritária e minoritária tem como dificuldade a definição destes custos. Por exemplo, se o número de exemplos da classe majoritária for o dobro do número de exemplos da minoritária, um erro de classificação para um exemplo da classe minoritária pode equivaler à ocorrência de dois erros de classificação para um exemplo da classe majoritária. Entretanto, a definição dos diferentes custos geralmente não é tão direta assim.

O último caso inclui as técnicas de classificação com apenas uma classe, em que a classe minoritária ou a classe majoritária (ou ambas as classes) são aprendidas separadamente. Nesse caso, pode ser utilizado algoritmos de classificação para uma classe apenas. Esses algoritmos são treinados utilizando apenas exemplos da classe positiva.

#### Limpeza de Dados

Conjuntos de dados podem também apresentar dificuldades relacionadas com a qualidade dos dados. Exemplos mais frequentes dessas dificuldades são dados ruidosos, redundantes ou incompletos. Essas deficiências nos dados podem ser causadas por problemas nos equipamentos que realizam a coleta, a transmissão e o armazenamento dos dados ou problemas no preenchimento ou na entrada dos dados por seres humanos. Algumas técnicas de AM conseguem lidar bem com algumas dessas imperfeições nos dados. Já outras tem dificuldades ou não conseguem lidar com dados que apresentem algumas dessas deficiências.

**Dados Incompletos**
Como já mencionado, um dos problemas que pode ser encontrado em conjuntos de dados é a ausência de valores para alguns atributos de alguns objetos. Algumas técnicas de AM podem gerar erro de execução quando um ou mais atributos do conjunto de treinamento não apresentam valor. Várias alternativas tem sido propostas para lidar com esses atributos. As alternativas mais utilizadas são:
- Eliminar os objetos com valores ausentes. Essa alternativa não é indicada quando poucos atributos do objeto possuem valores ausentes, quando o número de atributos com valores ausentes varia muito entre os objetos com esse problema ou quando o número de objetos que restarem for pequeno.
- Definir e preencher manualmente valores para os atributos com valores ausentes. Essa alternativa não é factível quando o número de objetos ou atributos com valores ausentes for muito grande.
- Utilizar algum método ou heurística para automaticamente definir valores para atributos com valores ausentes. Essa é a alternativa mais utilizada.
- Empregar algoritmos de AM que lidam internamente com valores ausentes. Esse é o caso, por exemplo, de alguns algoritmos indutores de árvores de decisão.

A definição automática de valores para completar os valores ausentes tem seguido três abordagens diferentes na literatura:
- Estabelecer para o atributo um novo valor que indique que o atributo possuía um valor desconhecido (exemplo: -1). Esse valor pode ser comum a todos os atributos ou um valor diferente para cada atributo. O problema dessa alternativa é que o algoritmo indutor pode assumir que o valor desconhecido representa um conceito importante.
- Utilizar a média, moda ou mediana dos valores conhecidos para esse atributo. Essa medida pode ser calculada utilizando todos os objetos ou apenas os objetos da mesma classe do objeto com o atributo a ser preenchido.
- Empregar um indutor para estimar o valor do atributo. Para isso, o valor a ser definido seria o atributo alvo e os demais atributos seriam os atributos de entrada. A vantagem desse método é justamente a utilização de informação presente nos demais atributos para inferir o valor do atributo ausente. Essa abordagem é a mais popular. Em geral, resulta na utilização do valor empregado em objetos semelhantes.

**Dados Inconsistentes**
Dados inconsistentes são aqueles que possuem valores conflitantes em seus atributos. Essa inconsistência pode se dar entre valores de atributos de entrada (por exemplo, valor 120 para peso e 3 para idade) ou entre todos os valores dos atributos de entrada e o valor do atributo de saída (por exemplo, dois pacientes com as mesmas características, mas diagnósticos diferentes). 

Inconsistências podem ser identificadas quando relações conhecidas entre os atributos são violadas. Por exemplo, quando é sabido que os valores de um atributo variam de forma inversamente proporcional em relação a valores de um outro atributo.

**Dados Redundantes**
Um conjunto de dados pode possuir tanto objetos como atributos redundantes. Um objeto é redundante quando ele é muito semelhante a outro objeto do mesmo conjunto de dados, ou seja, seus atributos possuem valores muito semelhantes aos atributos de pelo menos um outro objeto. Um atributo é redundante quando seu valor para todos os objetos pode ser deduzido a partir do valor de um ou mais atributos. No caso extremo, possui o mesmo valor que um outro atributo para cada um dos objetos do conjunto de dados.

Objetos redundantes em um conjunto de dados participam mais de uma vez do processo de ajuste de parâmetros de um modelo, contribuindo assim mais que os outros objetos para a definição do modelo final. Isso pode dar ao modelo a falsa impressão de que esse perfil do objeto é mais importante que os demais. Como resultado, o tempo necessário para a indução de um modelo pode aumentar. Por isso, geralmente é desejável a eliminação de redundâncias, que pode ser feita em dois passos: identificação de objetos redundantes e eliminação das redundâncias encontradas.

A eliminação da redundância pode ocorrer pela elminação dos objetos semelhantes a um dado objeto ou pela combinação dos valores dos atributos dos objetos semelhantes. Conforme dito anteriormente, não apenas objetos, mas atributos também podem apresentar redundância. Um exemplo seria termos um atributo *quantidade de vendas*, um atributo *valor por venda* e um atributo *venda total*. Nesse caso, o valor do atributo *venda total* pode ser definido a partir do valor dos outros dois atributos. Um atributo redundante pode supervalorizar um dado aspecto  dos dados, por estar presente mais de uma vez. Assim , o desempenho de um algoritmo de AM geralmente melhora com a eliminação de atributos redundantes.

A redundância de um atributo está relacionada com a sua correlação com um ou mais atributos do conjunto de dados. Dois ou mais atributos estão correlacionados quando apresentam um perfil de variação semelhante para os diferentes objetos Quanto mais correlacionados os atributos, maior o grau de redundância. Se a correlação ocorre entre um atributo de entrada e um atributo rótulo, esse atributo de entrada terá grande influência na predição do valor do rótulo.

**Dados com Ruídos**
Dados com ruídos são dados que contém objetos que, aparentemente, não pertencem à distribuição que gerou os dados analisados. Dados com ruídos podem levar a um superajuste do modelo utilizado, pois o algoritmo que induz o modelo pode se ater às especificidades relacionadas com os ruídos, em vez da distribuição verdade que gerou os dados. Por outro lado, a eliminação de dados ruidosos pode levar à perda de informação importante. A eliminação desses dados pode fazer com que algumas regiões do espaço de atributos não sejam consideradas no processo de indução de hipóteses.

Existem diversas técnicas de pré-processamento que podem ser aplicadas na detecção e remoção de ruídos. Em estatística, esse problema é comumente solucionado por meio de técnicas baseadas em distribuição, em que os ruídos são identificados como observações que diferem de uma distribuição utilizada na modelagem dos dados. O maior problema dessa abordagem está em assumir que a distribuição dos dados é conhecida a priori, o que não reflete a verdade em grande parte das aplicações práticas.

Diversas outras técnicas podem ser utilizadas para reduzir o ruído em um atributo, que pode ser em um atributo de entrada, mas também no atributo meta. De forma resumida, elas podem ser reunidas em cinco grupos:
- **Técnicas de encestamento**: essas técnicas suavizam o valor de um atributo da seguinte forma. Primeiro, os valores encontrados para esse atributo em todos os objetos são ordenados. Em seguida, esses valores são divididos em cestas, cada uma com um mesmo número de valores. Os valores em uma mesma cesta são substituídos, por exemplo, pela média ou mediana dos valores presentes na cesta.
- **Técnicas baseadas em agrupamento dos dados**: essas técnicas podem ser utilizadas tanto para os objetos como para os atributos. No caso dos atributos, os valores dos atributos são agrupados por uma técnica de agrupamento. Valores de atributos que não formarem um grupo com outros valores são considerados ruídos ou *outliers*. O mesmo é dito de objetos que forem colocados em um grupo no qual os demais objetos pertencem a uma outra classe.
- **Técnicas baseadas em distância**: a presença de ruído em um ou mais atributos de um objeto frequentemente faz com que esse objeto se distancie dos demais objetos de sua classe. As técnicas baseadas em distância verificam a que classe pertencem os objetos mais próximos de cada objeto x. Se esses objetos mais próximos pertencem a outra classe, são boas as chances do objeto x apresentar ruído, embora possa também ser um *borderline* (próximo à fronteira de separação das classes).
- **Técnicas baseadas em regressão ou classificação**: as técnicas baseadas em regressão utilizam uma função de regressão para, dado um valor com ruído, estimar seu valor verdadeiro. Se o valor a ser estimado for simbólico, uma técnica de classificação pode ser utilizada.

#### Transformação de Dados

Várias técnicas de AM estão limitadas à manipulação de valores de determinados tipos, por exemplo, apenas valores numéricos ou apenas valores simbólicos. Adicionalmente, algumas técnicas tem seu desempenho influenciado pelo intervalo de variação dos valores numéricos.

Esta seção divide as diferentes técnicas para abordar esse problema em três partes. A primeira parte descreve técnicas que podem ser utilizadas para converter valores simbólicos em numéricos. A segunda parte parte mostra técnicas para converter valores numéricos em valores simbólicos. Finalmente, a terceira parte mostra casos em que a conversão não altera o tipo do atributo, notadamente relacionados com atributos com valores numéricos, ou seja, transformações que podem envolver, por exemplo, mudanças de escala ou de intervalo de valores.

**Conversão Simbólico-Numérico**
Técnicas como redes neurais artificiais e *support vector machines* e vários algoritmos de agrupamento liam apenas com dados numéricos. Assim, quando o conjunto de dados utilizado por essas técnicas apresenta atributos simbólicos, os valores desses atributos devem ser convertidos para valores numéricos.

Quando o atributo é do tipo nominal e assume apenas dois valores, se os valores denotam a presença ou ausência de uma característica ou se apresentam uma relação de ordem, um dígito binário é suficiente. Para um atributo simbólico com mais de dois valores, a técnica utilizada na conversão depende de o atributo ser nominal ou ordinal. Se houver uma relação de ordem entre os valores do atributo, a inexistência de uma relação de ordem deve continuar para os valores numéricos gerados. Ou seja, a diferença entre quaisquer dois valores numéricos deve ser a mesma. Uma forma de conseguir isso é codificar cada valor nominal por uma sequência de bits, em que *c* é igual ao número de possíveis valores ou categorias.

Na codificação 1 - de - c, também denominada canônica ou topológica, cada sequência possui apenas um bit com o valor 1 e os demais com o valor 0. Nessa codificação, cada posição da sequência binária corresponde a um possível valor do atributo nominal. Por exemplo, se a sequência binária possui 4 bits, o primeiro bit corresponde ao primeiro valor, o segundo bit ao segundo valor e assim por diante. A moda do valor de um atributo para o conjunto de objetos é definida pela posição (bit) da sequência que apresenta o maior número de valores iguais a 1.

A tabela abaixo ilustra a codificação 1 - de - c para um conjunto de seis valores nominais, em que cada valor representa uma cor.

| Atributo Nominal | Código 1 - de - c |
| ---------------- | ----------------- |
| Azul             | 100000            |
| Amarelo          | 010000            |
| Verde            | 001000            |
| Preto            | 000100            |
| Marrom           | 000010            |
| Branco           | 000001            |
Dependendo do número de valores nominais, a sequência binária para representar cada valor pode ficar muito longa. Imagine que você queira codificar os nomes de países com a codificação 1 - de - c. Como existem 193 países, seria necessário utilizar vetores com 193 elementos. Uma alternativa para este problema é a representação dos possíveis valores nominais por um conjunto de pseudoatributos. Para este mesmo exemplo, ao invés de simbolizar o nome do país, poderíamos simbolizar características que somadas, se tornarão únicas e são suficientes para identificar o país, como continente, PIB, população e área.

Quando existe uma relação de ordem, o atributo é do time ordinal, e a codificação deve preservar essa relação. Para isso, deve ser utilizada uma codificação em que a ordem dos valores esteja clara. Quando o valor numérico é um número inteiro ou real, essa transformação é simples e direta: basta ordenar os valores categóricos ordinais e codificar cada valor de acordo com sua posição na ordem, como ilustrado na tabela abaixo.

| Atributo Nominal | Código 1 - de - c |
| ---------------- | ----------------- |
| Primeiro         | 0                 |
| Segundo          | 1                 |
| Terceiro         | 2                 |
| Quarto           | 3                 |
| Quinto           | 4                 |
| Sexto            | 5                 |

**Conversão Numérico-Simbólico**
Algumas técnicas de AM foram desenvolvidas para trabalhar com valores qualitativos. Isso ocorre com uma parcela dos algoritmos de classificação e de associação. Se o atributo quantitativo for do tipo discreto e binário, com apenas dois valores, a conversão é trivial. Basta associar um nome a cada valor. Se o atributo original for formado por sequências binárias sem uma relação de ordem em si, cada sequência pode ser substituída por um nome ou categoria.

Nos demais casos, métodos de discretização permitem transformar atributos quantitativos em qualitativos. Para isso, eles transformam valores numéricos em intervalos ou categorias. Quando um atributo quantitativo é discretizado, o conjunto de possíveis valores é dividido em intervalos, e cada intervalo de valores quantitativos é convertido em um valor qualitativo. Em alguns métodos, o usuário pode influenciar a definição dos intervalos, definindo valores para parâmetros como número máximo de intervalos. Esses métodos são denominados paramétricos. Os métodos não paramétricos definem os intervalos utilizando apenas as informações presentes nos valores do atributo.

Os métodos de discretização podem ainda ser supervisionados ou não supervisionados. No primeiro caso, é utilizada a informação sobre a classe dos exemplos. as técnicas supervisionadas levam a melhores resultados, uma vez que a definição dos intervalos sem conhecimento das classes pode levar à uma mistura. Uma abordagem supervisionada simples seria escolher pontos de corte dos intervalos que maximizam a pureza destes.

Algumas das estratégias utilizadas pelos diferentes métodos são:
- Larguras iguais: divide-se o intervalo original de valores em subintervalos com a mesma largura. O desempenho dessa estratégia pode ser afetado pela presença de *outliers*.
- Frequência iguais: atribui o mesmo número de objetos a cada subintervalo. Essa estratégia pode gerar intervalos de tamanhos muito diferentes.
- Uso de algoritmo de agrupamento de dados.
- Inspeção visual.

**Transformação de Atributos Numéricos**
Algumas vezes, o valor numérico de um atributo precisa ser transformado em outro valor numérico. Isso geralmente ocorre quando os limites inferior e superior de valores dos atributos são muito diferentes, o que leva a uma grande variação de valores, ou ainda quando vários atributos estão em escalas diferentes. Essa transformação é geralmente realizada para evitar que um atributo predomine sobre o outro. No entanto, pode haver situações em que essa variação deve ser preservada por ser importante para indução de um bom modelo.

Vamos supor que, dado um atributo com valores inteiros, para a indução de um bom modelo apenas a magnitude dos valores seja importante, não o sinal. Uma transformação necessária seria então converter os valores desse atributo para o seu valor absoluto.

Outra transformação muito utilizada é a **normalização de dados**. A normalização de dados é recomendável quando os limites de valores de atributos distintos são muito diferentes, para evitar que um atributo predomine sobre outro. Quando recomendada, ela é aplicada a cada atributo individualmente e pode ocorrer de duas formas: por **amplitude ou por distribuição**.

**A normalização por amplitude pode ser por reescala (min-max) ou por padronização (*standardization*).** A primeira define uma nova escala de valores, limites mínimo e máximo, para todos os atributos. Enquanto a segunda define um valor central e um valor de espalhamento comuns para todos os atributos.

Na normalização por reescala, também chamada de min-max, são inicialmente definidos os valores mínimo (min) e máximo (max) para os novos valores de cada atributo (comumente definidos com min = 0 e max = 1). Depois, a equação a seguir é utilizada sobre cada atributo, em cada observação, onde maior é o maior valor encontrado na distribuição e menor o menor valor encontrado na distribuição do atributo.

$v_{novo} = min + \frac{v_{atual} - menor}{maior - menor} (max - min)$

Para a normalização por padronização, a cada valor do atributo a ser normalizado é adicionada ou subtraída uma medida de localização e o valor resultante é em seguida multplicado ou dividido por uma medida de escala. Se as medidas de localização e de escala forem a média (μ) e a variância (σ), respectivamente, os valores de um atributo são convertidos para um novo conjunto de valores com média 0 e variância 1, que é obtido conforme a equação:

$v_{novo} = \frac{v_{atual} - μ}{σ}$

**Geralmente, é preferível padronizar (StandardScaler) à reescala (min-max Scaler), pois a padronização lida melhor com *outliers*.** 

A normalização por distribuição muda a escala de valores de um atributo. Um exemplo dessa normalização é a aplicação da função para ordenar os valores do atributo a ser normalizado a substituição de cada valor pela posição que ele ocupa no ranking (por exemplo, a aplicação dessa normalização aos valores 1, 5, 9 e 3 gera, respectivamente, os valores 1, 3, 4 e 2).

https://vitalflux.com/minmaxscaler-standardscaler-python-examples/#Differences_between_MinMaxScaler_and_StandardScaler

#### Redução de Dimensionalidade



