<!--

- the aim of branching
- the naive method
  - as in 1960 (ref)
  - the issue with it (ref Acterberg 2005)
- various methods have been introduced since
  - pseudo-cost
  - strong branching
  - hybrid
  - reliability
  - lookahead
  - 

-->

## Branching

<!--Naive approach-->
The naive approach to choosing a variable to branch on, as defined in the seminal paper [@Land1960], is to choose the variable whose value from the solved LP relaxation is the furthest from an integer. As shown by [@Achterberg2005], this method can be shown to have worse performance then simply picking a variable to branch on at random.

Two of the main approaches to branching are *strong branching* and *psuedocost branching*. 
<!--Strong branching--><!--TODO: does not make any sense-->
Strong branching is a method that chooses a variable to branch on by computing the LP gains of the child nodes that would be generated after branching of that variable. 

<!--Pseudocost Branching-->
Pseudocost branching, on the other hand, keeps track of the change in objective function of the relaxed LP solution when a variable had been branched on in past exploration in the tree. The <!--is this meant to be pseudocosts?-->future costs can be defined as follows <--will define here-->. This branching rule can be quite uninformative at the start of the search and so strong branching is often performed toward the start of the search to get some history to go off of <!--note to self reword that sentence-->.

<!--Lookahead branching-->
Lookahead branching takes strong branching a level further by looking at not only the LP gains of the child nodes but of the grandchild nodes.
<!--Information Theoretic Branching-->
In 2014, Gilpin and Sandholm developed branching methods that reduced the uncertainty about the value of the variables at the optimal solutions by computing the entropy of each variable and branching on the variable with the greatest changing entropy. However, they use the fractional component of the solution found by solving the LP relaxation as the probability that the entropy is based on. This implies that the entropy that they are computing and the subsequent information that they are gaining from branching on those variables is not collected from the feasible solutions, but rather from the fractional components of the LP relaxation.

## The use of ML
<!--Decision Trees-->
Now on to decision trees<!--TODO: cite-->.
In our research, we want to find branching strategies that exploit information found in the feasible solutions of MIPs.
This is not so different from the training process of decision trees. The goal in training a decision tree is to find the best ways to split the dataset such that the uncertainty of the result is reduced. There are many different measures of uncertainty that can be used in the decision tree model, such as variance or entropy, but the underlying process remains the same. In this light, a branch and bound search tree can be likened to a decision tree where the decisions are which variables to branch on and the results are the objective values at those solution.

<!--SVMs-->
Support Vector machines<!--TODO: cite--> may also be useful in this regard although less obviously.
A support Vector Machine classifier also splits a data set to reduce uncertainty about the outcome, but only one split is made using a kernel<!--TODO: explain--> that combines the variables in a linear or nonlinear way, depending on which one you choose. This can be likened to that of a disjunctive cut <!--TODO: reference to disjunctive-->.
<!--refer to survey-->For more information about Machine Learning, we refer the reader to [@Kotsiantis2007].

<!--ML Review-->
Machine learning has been used extensively in the field of discrete optimisation to improve the components of branch and bound search.
<!--Learning to search-->
In 2014, He et al. used imitation learning to train mode selection strategies. To train these strategies, they observe the behaviour from an oracle that knew where the optimal solution was before training.<!--TODO: good/bad, pros/cons, how does it affect us?-->

<!--Approximation for strong branching-->
In 2016, Khalil et al. developed a framework to learn an approximation algorithm for strong branching which would be more efficient to compute during the branch and bound search. As features, the learning algorithm used the coefficients of the objective function, the number of constraints, and statistics pertaining to the constraint degrees i.e. the number of variables that participated in a constraint the statistics included mean standard deviation minimum and maximum. These features do not necessarily provide information about the variables from the feasible solutions.

<!--Balcan2018-->
In a more recent paper Balcan et al. [@Balcan2018] used ML to learn an optimal mixture of branching rules. This mixture is a linear combination of several different branches of these <!--include list them here!-->. Their results showed that the optimal mixture learnt on one set of instances would result in substantially bigger tree sizes than on other instances and hence does not generalise well.

## Other research - learning from solutions

<!--
Discuss in brief paragraphs:

- Learning from nogoods
- (possibly not) Genetic programming to guide search
- Local Impact search

-->

Although, to the best of our knowledge, there is no work in the realm of MIP that learns from feasible solutions, there exists techniques to learn from *infeasible* solutions.
More precisely, whenever a node of the branch and bound is proven to be infeasible, a *nogood* is created to encapsulate the reason for the infeasibility @[Sandholm2006].
A nogood is a constraint that explains why this solution subspace can be pruned.
Once generated, it can be added at the root node of the search tree, and can help prune other nodes of the tree.
A nogood is thus information learnt from infeasible subspaces.
This is in contrast to feasible subspaces, for which such techniques do not seem readily applicable, but from which we posit that different interesting and performance-improving techniques could be designed.


# Conclusion

As we have shown, there is a need to explore whether or not information about the feasible solutions can be used to guide the branching strategies of discrete optimisation solvers. In this review we have discussed the approaches taken by the state of the art branching strategies, and shown that the current state of the art strategies do not use information from feasible solutions, but rather information collected from fractional solutions to the LP relaxations. We have also explored how ML can be used to extract information from these problems and we have explored different ML based approaches used in solving discrete optimisation problems. Many of the applications of ML in MIP use information collected about the meta-features of the problems to guide the behaviour of these components or <!--TODO: talk about the results of the Balcan-->. We anticipate that this study will provide an answer to our research question.
