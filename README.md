# Processo-de-decisao-de-Markov-MDP--Aprendizado-por-Reforco
Processo de decisao de Markov para encontrar trajeto ótimo


## PROBLEMA SIMULADO:

Como escolher o melhor caminho para se chegar em um destino?

Sabendo de início o ponto de partida e de chegada, assim como informações históricas que nos ajudam a determinar as condições dos caminhos, podemos ter uma infinidade de possíveis caminhos para se chegar ao destino final. A decisão a ser feita depende do estado atual das estradas, relativo a condições de tráfego, limite de velocidade, semáforos, etc.

Temos como objetivo minimizar o tempo de trajeto de um aluno saindo de carro de sua casa com destino a Universidade Federal de Santa Catarina, considerando que as condições das estradas não se alteram, não há novas construções, as estradas não são fechadas e não há qualquer outro imprevisto que possa alterar a dinâmica das estradas. Dessa forma, temos dados suficientes para saber o que irá acontecer ao longo do caminho. Ainda, devemos nos atentar ao fato de que, a cada decisão de rota tomada, teremos uma mudança no estado atual, ou seja, o aluno terá novas decisões de rotas a serem tomadas, portanto a dinâmica de estados não é fixa.

A dinâmica do ambiente pode ser vista na figura 1

<img src="https://github.com/nicolasantero/Processo-de-decisao-de-Markov-MDP--Aprendizado-por-Reforco/blob/main/images/MDP.PNG" width="400">


Para resolução do problema defina os estados e ambiente como apresentado na figura 1. Podemos ver que existem caminhos com buracos, semáforos e faixa de pedestre. Nesses casos o tempo de trajeto pode ser elevado caso tomemos a decisão de seguir por esses caminhos. Dessa forma, consideramos que ir por esse caminho afetará negativamente as nossa decisões.


<img src="https://github.com/nicolasantero/Processo-de-decisao-de-Markov-MDP--Aprendizado-por-Reforco/blob/main/images/ambienteMDP.png" width="200" height="200">


## Solução:

Para entendermos como funciona a solução apresentada, primeiramente é preciso entender o conceito de agente e ambiente. 

O ambiente é o cenário ou situação em que o agente se encontra. O agente usa as informações que ele consegue do ambiente para tomar as decisões necessárias para alcançar um objetivo.

Para o processo de decisão de Markov, utilizado nessa solução, quando é possível tomar várias decisões, o objetivo é obter a maior recompensa possível no final do processo. Portanto, podemos estabelecer uma política que envolva o sacrifício de uma boa decisão a fim de atingir esse objetivo final.

Para isso, ele conta com:


- Conjunto de estados (S): todas as possíveis localizações do agente no ambiente.
- Conjunto de ações (A):  todas as ações que podem ser tomadas pelo agente estando em determinado estado. 
- Probabilidades de transição: probabilidade de que uma ação seja bem sucedida ao longo prazo. 
- Recompensa (R): o valor adquirido ao chegar em algum estado.
- Fator de desconto ($\gamma$): diminui o valor de futuras recompensas se comparado com as recompensas atuais.


Sabendo disso, podemos entender que o processo de decisão de Markov (PDM) é independente de ações do passado, ou seja, as ações futuras serão tomadas com base nas variáveis atuais, ou seja, $S_t$ e $R_t$. 

<img src="https://github.com/nicolasantero/Processo-de-decisao-de-Markov-MDP--Aprendizado-por-Reforco/blob/main/images/agente_ambiente.jpg" width="400">

Essa figura ilustra que o ambiente dá ao agente o estado e a recompensa atual, e o agente toma alguma decisão que altera o ambiente, de modo que isso se torna um ciclo.

A forma utilizada para resolver o PDM nesta solução foi a Iteração de Valor (\emph{Value Iteration}). Como o objetivo final é conseguir o maior valor de recompensa acumulado, o processo utiliza a equação de otimização de Bellman:

<img src="https://github.com/nicolasantero/Processo-de-decisao-de-Markov-MDP--Aprendizado-por-Reforco/blob/main/images/bellman.png" width="400">

A \emph{Value Iteration} é uma técnica de aprendizado por reforço. Ela computa o valor resultante para cada iteração e adiciona o valor mais alto à política atual. 

O algoritmo utilizado para a implementação dessa técnica converge com base em um erro mínimo aceitável pré definido e exige bastante tempo por iteração, já que sempre examina todo o conjunto de espaços.


## Algoritmo:


- Loop infinito até atingir convergência:
    
- - Define uma variável erro := 0. 
- - Para cada estado s no conjunto de estados:
- - - v anterior := V(s)   (Armazena o valor anterior do estado)
- - - v atual := 0
- - - Para cada possível ação em um estado:
- - - - v := valor de recompensa esperado passando por esse estado e ação
- - - - se o valor de v calculado para a ação e estado for maior que o v atual:
- - - - v atual := v
- - - - politica do estado := ação que teve maior valor v
- - - - V(s) := maior valor de v (v atual) dentre todas as diferentes ações do estado s
- - - - erro := max(erro, |v anterior – V(s)|)
- - - Se o erro for menor que epsilon o loop infinito se encerra, pois ocorreu a convergência.

A solução desse problema foi desenvolvida utilizando \emph{Python} e aplicando o algoritmo iterativo descrito até a convergência.


## Referências

BARTO, Richard S. Sutton And Andrew G.. Reinforcement Learning: an introduction. Cambridge,
Massachusetts: The Mit Press, 1992. Disponível em: http://incompleteideas.net/book/first/ebook/the-book.html

• BHANDARKAR, Raghuveer. Policy Iteration in RL: a step by step illustration. A step by step
Illustration. Disponível em: https://towardsdatascience.com/policy-iteration-in-rl-an-illustration-6d58bdcb87a7

• SILVER, David. UCL Course on RL. 2015. Disponível em: https://www.davidsilver.uk/teaching/.

• POOLE, David; MACKWORTH, Alan. Artificial Intelligence: foundations of computational agents.
Vancouver: Cambridge University Press, 2017. Disponível em: https://artint.info/aifca1e.html.


