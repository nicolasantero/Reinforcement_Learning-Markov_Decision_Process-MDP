# Markov_Decision_Process-MDP--Reinforcement_Learning

Markov Decision Process to find optimal path.


## Problem:

How to choose the best path to reach a destination?

Knowing the starting and ending point, as well as historical information that helps us determine the conditions of the roads, we can have a multitude of possible routes to reach the final destination. The decision to be made depends on the current state of the roads, relative to traffic conditions, speed limits, traffic lights, etc.

Our goal is to minimize the travel time for a student leaving his or her home by car to the University, considering that the road conditions don't change, there are no new constructions, the roads won't be closed or any other unforeseen event that could alter the dynamics of the roads. Thus, we have enough data to know what will happen along the way. Still, we must pay attention to the fact that, at each route decision made, we will have a change in the current state, that is, the student will have new route decisions to be made, so the dynamics of states is not fixed.

The dynamics of the environment can be seen in the following figure.

<img src="https://github.com/nicolasantero/Processo-de-decisao-de-Markov-MDP--Aprendizado-por-Reforco/blob/main/images/MDP.PNG" width="400">


To solve the problem, define the states and environment as shown in the picture. We can see that there are paths with holes, traffic lights and crosswalks. In these cases the travel time can be high if we make the decision to follow these paths. So we consider that going this way will negatively affect our decisions.


<img src="https://github.com/nicolasantero/Processo-de-decisao-de-Markov-MDP--Aprendizado-por-Reforco/blob/main/images/ambienteMDP.png" width="200" height="200">


## Solution:

To understand how the presented solution works, we first need to understand the concept of agent and environment. 

The environment is the scenario or situation in which the agent finds itself. The agent uses the information it gets from the environment to make the necessary decisions to achieve a goal.

For the Markov decision process used in this solution, when multiple decisions can be made, the goal is to obtain the highest possible reward at the end of the process. Therefore, we can establish a policy that involves the sacrifice of a good decision in order to achieve this final goal.

To do this, it relies on:


- Set of states (S): all possible locations of the agent in the environment.
- Set of actions (A): all the actions that can be taken by the agent in a given state. 
- Transition Probabilities: probability that an action will be successful in the long run. 
- Reward (R): the value acquired by reaching some state.
- Discount factor ($\gamma$): decreases the value of future rewards compared to current rewards.


Knowing this, we can understand that the Markov decision process (MDP) is independent of past actions, in other words, future actions will be taken based on the current variables, that is, $S_t$ and $R_t$. 

<img src="https://github.com/nicolasantero/Processo-de-decisao-de-Markov-MDP--Aprendizado-por-Reforco/blob/main/images/agente_ambiente.jpg" width="400">

This figure illustrates that the environment gives the agent the current state and reward, and the agent makes some decision that changes the environment, so this turns into a loop.

The way used to solve the MDP in this solution was Value Iteration. Since the end goal is to achieve the highest cumulative reward value, the process uses the Bellman optimization equation:

<img src="https://github.com/nicolasantero/Processo-de-decisao-de-Markov-MDP--Aprendizado-por-Reforco/blob/main/images/bellman.png" width="400">

The \emph{Value Iteration} is a reinforcement learning technique. It computes the resulting value for each iteration and adds the highest value to the current policy. 
The algorithm used to implement this technique converges based on a predefined minimum acceptable error and requires a lot of time per iteration, since it always examines the entire set of spaces.


## Algorithm:


- Infinite loop until convergence is reached:
    
- - Sets an error variable := 0
- - For each state s in the state set:
- - - previous v := V(s) (Stores the previous value of the state)
- - - current v := 0
- - - For each possible action on a state:
- - - - v := expected reward value passing through that state and action
- - - - if the value of v calculated for the action and state is greater than the current v:
- - - - current v := v
- - - - state policy := action that had the highest v value
- - - - V(s) := largest value of v (current v) among all the different actions in state s
- - - - error := max(error, |previous v - V(s)|)
- - - If error is less than epsilon the infinite loop terminates because convergence has occurred

The solution to this problem was developed using \emph{Python} and applying the described iterative algorithm until convergence.


## References

BARTO, Richard S. Sutton And Andrew G.. Reinforcement Learning: an introduction. Cambridge,
Massachusetts: The Mit Press, 1992. Available at: http://incompleteideas.net/book/first/ebook/the-book.html

• BHANDARKAR, Raghuveer. Policy Iteration in RL: a step by step illustration. A step by step
Illustration. Available at: https://towardsdatascience.com/policy-iteration-in-rl-an-illustration-6d58bdcb87a7

• SILVER, David. UCL Course on RL. 2015. Available at: https://www.davidsilver.uk/teaching/.

• POOLE, David; MACKWORTH, Alan. Artificial Intelligence: foundations of computational agents.
Vancouver: Cambridge University Press, 2017. Available at: https://artint.info/aifca1e.html.


