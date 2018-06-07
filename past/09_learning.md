<!--

All of the papers need to be analysed for the following questions:

- What was the research question of this paper?
- What were the methods employed by the paper?
- Did the paper use the best method to achieve this?
- How good were the results, really?
- if ML:
  - What features were used?
  - What portion of the solution space was used in the learning process?

-->

# Learning to Branch
*Balcan et al. 2018*

- Uses machine learning to learn an optimal mixture of branching rules. This mixture is a linear combination of the different branching rules.
- Show experimentally that using an optimal configuration from a different set of instances can lead to substantial increase in tree size.
- Proved that the increase can be exponential.
- Provided the first sample complexity guarantees. <!--What is this-->
- uses abstract methods of evaluating cost, such as tree size. <!--What other methods get used? How do these methods get used?-->
- Using empirical Rademacher complexity, bounds can be tightened further. <!--What bounds, what is Rademacher complexity? Is it even important?-->
- Closes before the conclusion, stating that "we showed that learning to branch is practical and hugely beneficial". Big statement !!
- says that learning to branch can be applied to other tree-growing applications, which is obvious.

# Learning to Branch in Mixed Integer Programming
*Khalil et al. 2016*

- Develops a machine learning framework for MIP.
- The framework learns to imitate the branching behaviour of Strong Branching by learning to rank the variables. <!--This is probably really inaccurate-->
- The learned approximation is then used to branch on the variables.
- The learned function is benchmarked against other methods. The other methods include CPLEX-D, Strong Branching, Pseudocost Branching and a Hybrid of Strong Branching and Pseudocost Branching. <!--How does the hybrid work?-->
- Features used:
  - Objective function coefficients
  - Number of constraints
  - Statistics pertaining to the constraint degrees i.e. the number of variables that participate in a constraint. These statistics are mean, std, min, max.
  - 
# Learning Combinatorial Optimisation Algorithms over Graphs
*Dai et al. 2017*

- Aims to develop an algorithm that learns to make heuristics that exploit the structure of problems? Their reasoning for doing so 
- Reinforcement Learning and Graph embedding to do so
- "Learned greedy policy is then used to incrementally construct a heuristic to the optimisation algorithm"
- "The action is determined by output of a graph embedding network tacking the current state of the solution"
- Test the method on MVC, MAXCUT and TSP
- The algorithm designs heuristics for problems on graphs. <!--Can it be used to design algorithms for problems not on graphs-->
- <!--How big are the problems that are being solved?-->
- <!--How many instances are tested?-->
- <!--What portion of the feasible solutions are used?-->

# Learning when to use a decomposition
*Kruber et al. 2016*

 <!--What is a decomposition?-->
 <!--Why and when would it be useful?-->
 <!--How did they learn?-->
 <!--What features if supervised?-->
 <!--How did they represent the information?-->
 <!--What kind of information would they capture?-->
 Instances, number of feasible solutions used, portion of the max?
- A decomposition is a means of reformulating the problem. Often requires a fair amount of effort `GCG` does this prior to solving but it's only in few cases where `GCG` outperforms `SCIP`.
- Kruber et al. set out to use machine learning to decide whether or not to use `GCG` or `SCIP`
- They use supervised learning methods: k nearest neighbors, SVM with RBF kernel and random forests.
- They create a function that takes a problem, a decomposition and a time limit and produce a data set with features.
- Instances from a large range of families
- >100 features:
  <!--- number of variables-->
  <!--- number of constraints-->
  <!--- number non-zeros-->
  <!--- proportion of integer, binary, continuous variables.-->
  <!--so many-->
  <!--- instance based-->
  <!--- decomposition variables-->
  <!--- adjacencies in the bipartite graph-->
  <!--- detector based features-->
  <!--- detector indicator-->
<!--- families of instances:-->
  <!--- vertex colouring-->
  <!--- set covering-->
  <!--- capacitated p-median-->
  <!--- survivable fixed telecommunication network design-->
  <!--- cutting stock-->
  <!--- generalized assignment-->
  <!--- network design-->
  <!--- lot-sizing (25/25 optimal solutions)-->
  <!--- bin packing-->
  <!--- capacitated vehicle routing-->
- not really anything about the information to be gained from each variable


