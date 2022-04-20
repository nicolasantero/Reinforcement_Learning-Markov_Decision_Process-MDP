# Processo-de-decisao-de-Markov-MDP--Aprendizado-por-Reforco
Processo de decisao de Markov para encontrar trajeto ótimo


\subsection{Problema:}

Como escolher o melhor caminho para se chegar em um destino?

Sabendo de início o ponto de partida e de chegada, assim como informações históricas que nos ajudam a determinar as condições dos caminhos, podemos ter uma infinidade de possíveis caminhos para se chegar ao destino final. A decisão a ser feita depende do estado atual das estradas, relativo a condições de tráfego, limite de velocidade, semáforos, etc.

Temos como objetivo minimizar o tempo de trajeto de um aluno saindo de carro de sua casa com destino a Universidade Federal de Santa Catarina, considerando que as condições das estradas não se alteram, não há novas construções, as estradas não são fechadas e não há qualquer outro imprevisto que possa alterar a dinâmica das estradas. Dessa forma, temos dados suficientes para saber o que irá acontecer ao longo do caminho. Ainda, devemos nos atentar ao fato de que, a cada decisão de rota tomada, teremos uma mudança no estado atual, ou seja, o aluno terá novas decisões de rotas a serem tomadas, portanto a dinâmica de estados não é fixa.
