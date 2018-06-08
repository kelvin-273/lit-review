# Introduction

Optimisation is at the heart of many of life's problems.
It rears its head in problems like price setting, ordering stock, scheduling tasks, and distributing power to cities [@Conforti2014, chap. 2]. Even in the story of Aladdin, whilst never explicitly mentioning optimisation, an opportunity to explore a discrete optimisation problem presents when the characters are fleeing the Cave of Wonders and potentially considering which treasures to pack in into their Knapsack [@Clements1992].

<!--give example of the lot-sizing problem-->
The lot-sizing problem is an excellent example of a discrete optimisation problem solved every day. Let us say that a store owner wants to order stock for their products. The question posed in the lot-sizing problem is: how many of each item should we order if we want to minimise the total cost from purchasing and holding the products. <!--There might be more-->

<!--
More detail about discrete optimisation in general
- constraints
- discrete solutions
-->
In general, a discrete optimisation problem is any problem where we want to find a set of values for variables that minimises (or maximises) some objective function $f(\mathbf{x})$, and satisfies some constraints. In the lot-sizing problem, the objective function that we are trying to minimise is the total cost, the variables that we have control over are the quantity ordered for each item and the constraint is the capacity of our storage facility which cannot be surpassed.

Solving discrete optimisation problems can be a computationally intensive task.
Much of the difficulty is knowing where to look for good solutions.

Solving discrete optimisation problems is difficult because each variable that you add to the problem multiplies the number of total possible feasible solutions by some factor. As another example, in solving the knapsack problem, you are trying to find the subset of items that has the greatest total monetary value but whose total weight is below some real positive value representing the capacity of the knapsack. For each item that you take into account, the total number of subsets to consider doubles. For $10$ items, there would be $2^{10} = 1024$ possible combinations to consider, but for $100$ items there are $2^{100}$ possible solutions to consider, which is more than the total number of stars in the known observable universe<!--TODO: cite this-->.

To get around this scale in complexity, many different solving approaches have been taken and are utilised in state of the art solvers today<!--TODO: do I need to cite this?-->. These approaches are in branching and pruning, searching, removing constraints, propagating constraints, decompositions, improving approximations, and so on<!--TODO: citations-->. The field of discrete optimisation is vast. <!--TODO: talk about reference seminal papers on these subsections for further reading-->

In the past decade, research has been done regarding the use of machine learning to improve the methods that solve these problems<!--TODO: either cut this sentence or the next-->. The last decade has seen an explosion in Machine Learning research and it has brought along uses in improving the efficiency of these solvers<!--TODO: citations-->. Machine learning is the process of tuning parameters of a predictive model to find the best fit of those parameters through training data. These models can be used to act as approximate functions for other functions<!--TODO: cite the strong branching paper-->.

Research has been done<!--TODO: vague, add references--> that utilises adaptive strategies to choose where to split the solution space of these discrete optimisation problems. 
Some of these methods use techniques from machine learning to guide the splitting (also called branching) strategies.
So far, the studies on these adaptive strategies have not considered learning with respect to the total amount of information that can be extracted from these problems.

The Branch and Bound <!--TODO: citation--> algorithm is a method for solving these problems that splits the solutions by branching on a particular variable at a time.
In this project we will investigate the amount of information that can be learned about the which variables to branch on, with and without complete prior knowledge of all feasible solutions in the solution space of a discrete optimisation problem.

However, there are limits to how much information can be learned from these problems. In this review, we will explore what kind of learning techniques have been utilised in the field of discrete optimisation and why research needs to be undertaken to explore the bounds of how much information can be learned from these problems.

In the research following from this review we will explore whether or not there exists information in the feasible solutions that can be exploited by a Branch and Bound tree. We hope that the research inspires new approaches to branching that utilise this information.
