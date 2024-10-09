+++
title = " Mastering Backtracking for LeetCode Success"
author = "Alejandro Armas"
tags = ["Computer Science", "Algorithms", "Leetcode"]
date = 2024-10-08
+++


### Goal of Today's Post

When you're done reading my blogpost, my goal is for you to:
1. To leave with a generic scaffolding to set up Backtracking Problems 
2. Have a framework to reason about most Backtracking Problems
3. Worked through 5 Backtracking Examples ([Just give me the examples!](#examples))

### Introduction


At the time of this writing, I currently find myself at 450+ leetcode problems solved. I tricked myself into liking the grind! It's bad. I should go outside and touch grass. 

![LeetCode Stats](https://leetcard.jacoblin.cool/armas?theme=dark&font=Cairo&ext=contest)

I'm actually quite proud of this fact though. It's been a journey filled with tons of learning experiences. In fact, I have been studying for Big Tech technical interviews for the past 7 months. It's the third time doing a studying regiment. It's terrible I know!! I hate this. On the bright side at-least I've gotten pretty good at a few types of problem categories. Today, I'll be adding to this saturated conversation with my two-cents on the Backtracking problem categories.

{{< figure src="/posts/leetcode/Leetcode-Progress.png" alt="Leetcode Progress">}}

### Prerequisites

For your benefit and to be most effective, I recommend brushing up on the following, if neccessary: 
1. Coding Depth First Search (DFS) Algorithm
2. Understanding Pre-Order, In-order and Post-Order traversals using DFS

### Identifying These Problems

When are these problems used anyways?

There are many cues to identify when to use Backtracking, in general you might identify them with the following:

1. **Problem Description or Solution Output:**  Usually these problems say want you to find all solutions, or combinations. If not possible, then to return an error code
2. **Solution Input (Constraint):** Generally the input space is really small, so a brute force approach is a perfectly acceptable answer (i.e. no larger than ~10-15 elements) 

### Relation to Other Problem Categories

**Backtracking:** is also closely tied to Dynamic Programming (DP), greedy, and math-based solutions. Those approaches all represent optimizations over this brute force search approach. 

### Template for Solving These Problems 

Here's pseudocode outlining a very generic template for solving backtracking problems:

```python
def backtracking_algorithm(data): 

	initial_state: "State" = SetInitState()

	def modify_state(state: "State") -> "State":
		return state + "modification"

	def revert_state(state: "State") -> "State":
		return state - "modification"

	def _traverse_search_space(state)

		if valid_termination_state:
			return "Solution"
		elif invalid_termination_state:
			return "Prune Current Search"
		else:
			new_state: "State" = modify_state(state)
			_traverse_search_space(state=new_state)
			state = revert_state(new_state)
			return "Keep Searching"

return _traverse_search_space(state=initial_state)
```

1. `modify_state`: As we traverse down the search space, we transition our state to the state of the search space's children. The state must reflect this.
2. `revert_state`: This encapsulates the logic in returning a the state of a child back into its parent. This represents traversing upward in the search space. 
3. `valid_termination_state`: Solution has been found, so either mutate a value outside of the recursion scope or propagate this return value up to the parent node 
4. `invalid_termination_state`: Depending on the state we can infer that the search must terminate. We prune accordingly. i.e. return an invalid result or do nothing

### Framework for Solving Backtracking

First understand that you will use the backtracking machinery to construct a **Directed Acyclic Graph (DAG)**. This tree represents the search space of the problem. Depending on your vision on how to frame the search, "solutions" can look very different. There will be a root node, children nodes and leaf nodes. It's up to you to design an effective and correct recursive formulation. Therefore, I like to think about the following ideas before I start any code: 
#### 1. Reason About States

Each node in the search is a state. You can expect some auxiliary data structures or variables to be highly coupled with this state. Either the recursive function has side-effects to an external state or the state is encapsulated in the function stack scope.   

In general, candidate solutions are being incrementally built here.

#### 2. How do State Transitions Occur

Lastly, you want to decide exactly on what kind of branching takes place for your nodes. Choose state transitions that will build onto each-other to eventually achieve a termination state. 

More often than not, one might either take a value or not as a state transition. Possibly a path is taken. There are so many possibilities. In either case, one would mutate the state as the crawl continues. When that recursive call is done, however, one should revert the state or "backtrack" to where one was previously.

#### 3. Be Specific About Termination States

These are the leaf nodes in your search tree. They can either represent candidate solutions turned into finalized solutions or terminated searches. Finalized solutions are either returned or some externalized variable is updated.

### Lets Get Some Problems Down for Practice!! {#examples}

Here's a quick legend giving you access to the 5 problems we cover below:

| Subsection Link                                       | Github Gist                                                                                     | Leetcode Link                                                                          | Difficulty |
| ----------------------------------------------------- | ----------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- | ---------- |
| [216. Combination Sum III](#prob1)                    | [Three Combination.md](https://gist.github.com/alejandroarmas/5a2900c055f5f3176e3dc7d30c7249e6) | [Combination Sum](https://leetcode.com/problems/combination-sum-iii)                   | Medium     |
| [980. Unique Paths III](#prob2)                       | [Unique Paths.md](https://gist.github.com/alejandroarmas/c39556940a38c6074c8bb5f2e1d75c2b)      | [Unique Paths III](https://leetcode.com/problems/unique-paths-iii)                     | Hard       |
| [37. Sudoku Solver](#prob3)                           | [Sudoku Solver.md](https://gist.github.com/alejandroarmas/fe3cefc3312a03dfe7803fe19c245973)     | [Sudoku Solver](https://leetcode.com/problems/sudoku-solver)                           | Hard       |
| [465. Optimal Account Balancing](#prob4)              | [Account Balancing.md](https://gist.github.com/alejandroarmas/14e57b7740a29c6046ed729a0164abd3) | [Optimal Account Balancing](https://leetcode.com/problems/optimal-account-balancing)   | Hard       |
| [1255. Maximum Score Words Formed by Letters](#prob5) | [Max Word Score.md](https://gist.github.com/alejandroarmas/75b42192ff46252e7e14967a02da7ad1)    | [Max Word Score](https://leetcode.com/problems/maximum-score-words-formed-by-letters/) | Hard       |


#### Backtracking Basics {#prob1}


In [216. Combination Sum III](https://leetcode.com/problems/combination-sum-iii), we are leveraging backtracking to generate all array's containing combination of numbers from 1-9 that sum to `k`. At a high level, each combination represents a subsequence of numbers from `[1,2,3,4,5,6,7,8,9]`. 


{{< gist alejandroarmas 5a2900c055f5f3176e3dc7d30c7249e6
 combination_sum_three.py >}}


The basic principles outlined by the template are appearant. We have two termination states. One that provides valid combinations and another that prunes the search space. All other cases involve continuing the search.

There is no mutation of our state beyond adding an element to a child traversal call. The revert of this state is handled implicitly, as we are not reusing the array that is copied to child calls. 

> [Back to Problem Legend](#examples) 

#### Lets Really Drill This In! {#prob2}


In [980. Unique Paths III](https://leetcode.com/problems/unique-paths-iii) we can follow the same methodology

{{< gist alejandroarmas c39556940a38c6074c8bb5f2e1d75c2b
 num_unique_paths.py >}}


> [Back to Problem Legend](#examples) 
#### Backtracking State Manipulation is Explicit Sometimes! {#prob3}

In [37. Sudoku Solver](https://leetcode.com/problems/sudoku-solver) we use the same machinery described in the previous problem. This time around, we must be intelligent in choosing a state and state transition that will effectively solve our problem. 

{{< gist alejandroarmas fe3cefc3312a03dfe7803fe19c245973
 sudoku_solver.py >}}

Notice that the perturbation and reverting of our state is more explicit this time around. This is a critical detail for solving these kinds of problems. 


> [Back to Problem Legend](#examples)

#### Maybe We Want to Identify a Min/Max Value? {#prob4}


Keeping in line with the state management we see in our previous problem, we see that in the following problem we are actually concerned with identifying a min/max value: [465. Optimal Account Balancing](https://leetcode.com/problems/optimal-account-balancing)

{{< gist alejandroarmas 14e57b7740a29c6046ed729a0164abd3 optimal_account_balance.py >}}

> [Back to Problem Legend](#examples)

#### Backtracking Tree Height Matters!! {#prob5}


In [1255. Maximum Score Words Formed by Letters](https://leetcode.com/problems/maximum-score-words-formed-by-letters/), I encountered a limitation posed by our tree's maximum recursion depth. One must be very careful to recognize that you really don't want to go above 20-30 in the exponential. The problem will become prohibitively expensive.


{{< gist alejandroarmas 75b42192ff46252e7e14967a02da7ad1
 max_word_scores.py >}}


Originally, the runtime of the algorithm was too slow. I realized I needed to process the word of an entire string at each node, instead of recursing onto the next character. This reduced the compexity down from `O(2 ^(num_words * max_word_len)`to `O(max_word_len * 2 ^(num_words)`

In other words, we had {{< katex "15 * 2^{14} \approx 245,760" true />}} to {{< katex "1.64 * 10^{64}" true />}}, which is too big to ever be completed when working with `max_word_len = 15` and `num_words = 14`


> [Back to Problem Legend](#examples)


### Conclusion










