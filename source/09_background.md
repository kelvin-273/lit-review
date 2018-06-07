# Background

## Optimisation

In this project, we choose to focus on discrete linear optimisation problems, which can be formulated as Mixed Integer Programming (MIP) problems.
These kinds of optimisation problems take the form
$z = \mathbf{c}^{\text{T}}\mathbf{x}$ such that
$\mathbf{x}$ satisfies the linear constraints
$A\mathbf{x} \le \mathbf{b}$ and
$\mathbf{x} \ge \mathbf{0}$.
Here, $z$ is some variable that we want to maximise (commonly referred to as the objective value),
$\mathbf{x} = (x_{1}, x_{2}, ... , x_{n})$ is the vector of variables that we have control over where some of the variables are constrained to the integers,
and $\mathbf{c} = (c_{1}, c_{2}, ... , c_{n})$ is a vector of linear coefficients.
The constraints are rules that determine what values our controlled variables can take.

Mixed Integer Programming problems are Linear Programming problems with integer constraints on some of the variables.
Linear Programming problems are commonly solved using the simplex method or interior point method [@Conforti2014], which is able to solve them efficiently by finding an optimal solution at one of the extreme points of the solution space. Here, we define the *solution space* as the set of all feasible solutions to the problem, the extreme points of which exist at the intersections of various constraints. However, when the feasible solutions are constrained to be integers, the geometry of the solution space cannot be as easily exploited by an algorithm like Simplex, as those extreme points may not be integer solutions.

## The Class of Branch and Bound Algorithms

MIP is NP-Hard [@Conforti2014], which means that any problem in the class of NP can reduced to a MIP problem in polynomial time [@Du2016, pp. 16-17] <!--TODO: Not the best reference-->. 

The general method for solving NP-Hard optimisation problems formulated as MIPs is called Branch and Bound, which is not a single algorithm, but a class of algorithms; all of which, as the name implies, have two key components [@Clausen1999]:

1. **Branching** - splitting the solution space into smaller pieces
2. **Bounding** - calculating the lower/upper bound

In general, The Branch and Bound algorithm is an implicit enumerative search that explores a tree of subspaces by iteratively splitting a solution space into smaller subspaces, evaluating an upper bound (or lower bound for a minimisation problem) of the objective value for each of these subspaces, removing any subspaces whose bounds, by comparison against the optimal solution thus far, indicate that they are not worth considering, and then repeating this process with the next best subspace in the tree. Whenever feasible solutions are found by the algorithm, their objective values are checked against that of the current optimal solution, and the current optimal solution is updated if the new feasible solution is more optimal.

In the algorithm described thus far, the only information that is collected in this process is information on what the current optimal solution is; all other solutions are not used to guide the search, besides informing the algorithms of what has been searched before.
Information regarding the values of the variables at those solutions is not used.
Infeasible solutions and infeasible subspaces are used to inform the algorithm of where not to look.

In the execution of this algorithm, information is collected about what has not been explored, what has been explored and what the lower and upper bounds are. We hope to show that more information exists in the structure of the feasible solutions and that this structure can be exploited.

As shown in the Literature Review section, adaptive strategies have been developed that do use information obtained from previous upper bounds on the solutions, However, no approach has been considered as of yet that uses information collected from the whole solution space a priori.

## Information

So how do we measure information? Informally, Chris Wallace [-@Wallace2005] defines information as "something the receipt of which reduces our uncertainty of the world".

In this respect, information about where the optimal solutions exist would reduce uncertainty about what objective values we could expect to find in different areas of the solution space.

We refer to uncertainty as the degree to which we would be unable to predict the outcome from a random process.
Shannon Entropy [@Shannon1948] is an excellent measure for this uncertainty.
Shannon defines entropy from a discrete process $Y$ as $H = -\sum_{i} p_{i}\log{p_{i}}$, where 
$p_{i} = \mathbb{P}(Y = y_{i})$ is the probability that the event $y_{i}$ occurs [@Shannon1948]. 

There are many other methods to measure this uncertainty; including Gini, a measure commonly used for income inequality [@Yitzhaki2013]; and metrics that represent the uncertainty in sampling from a continuum like Variance, used to measure the spread of a distribution; Mean Absolute Error, Mean Squared Error and Friedman Mean Squared Error [@Hastie2009].

Information Gain provides a comparison of the uncertainty before and after splitting on a given variable. Information Gain (denoted $IG$) can be measured using $$IG(Y, x) = I(Y) - \sum_{i} \mathbb{P}(x_{i}) I(Y|x_i),$$
where $Y$ in our case is the set of objective values,
$I$ the particular criterion (entropy, gini index, etc.) used,
$x$ is the variable that we are splitting on,
$x_{i}$ is a unique element of $x$,
and $P(x_{i})$ the probability of $x_{i}$ occurring in $x$.
