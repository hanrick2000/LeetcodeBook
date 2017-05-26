# Overview

## Explanation

- ![must-have][must-have] means __must do__ question, that includes many key points;
- ![recommended][recommended] means __good question__, that is quite clear and enjoyable;
- ![easy][easy] means __this is easy__ for me, that there might only be no fancy things;
- ![medium][medium] means __this is medium__ for me, that there is at least one important thing;
- ![hard][hard] means __this is hard__ for me, that it's hard to code;
- ![star][star] means __how many times I've done__ for this question;
- ![freq][freq] means __this is frequently asked__ in interviews.

## When to use DFS

- Find all possible permutations or combinations.
- Non-recursion with stack.

## Comparsion with BFS

- In BFS, each node has a uniform rule to get its neighbors. But often DFS doesn't have such rule. Sometimes you need to consider other constraints, like __Subsets__ question. But it can still be solved by BFS.
- It's hard to pass information like __ArrayList__ from last level to next level in BFS to build some path. But it's easier to do in DFS since it's using recursion, and it has backtracking to return information even from low level to hight level.
- Why we need to use DFS not BFS sometimes ?
  - The interviewer wants to see that you can write recursion.
  - BFS is complicated for some kind of questions like building a set of paths.
  - DFS can save a lot of memory, since it doesn't need to store previous state.
- BFS can get results by level, but only DFS can get all possible solutions.

## Recursion

- Define the recursion function.
  - What parameters to use.
- When to go into recursion.
  - In binary tree, entrance is left child or right child.
- When to end recursion.
  - If ... then return.

## Category

- Combination
  - According to some valid rule, check how many states can there be in current level and **only pass valid to next level**.
  - Cut off all the unnecessary states in the step2 of recursion as many as possible, and keep step3 as simple as only one sentence. In this way, the running time can be reduced a lot.
  - The content of each solution is not related to element order.
  - Question list
    - [Subsets](Subsets.md) ![easy][easy] ![star][star]
    - [Subsets2](Subsets2.md) ![easy][easy] ![recommended][recommended] ![star][star]
    - [CombinationSum](CombinationSum.md) ![medium][medium] ![recommended][recommended] ![must-have][must-have] ![star][star]
    - [CombinationSum2](CombinationSum2.md) ![easy][easy] ![star][star]
    - [PalindromePartitioning](PalindromePartitioning.md) ![hard][hard] ![recommended][recommended] ![star0][star0]
- Permutation
  - The content of each solution is related to element order.
  - Question list
    - [Permutations](Permutations.md) ![easy][easy] ![freq][freq] ![star][star]
    - [Permutations2](Permutations2.md) ![hard][hard] ![recommended][recommended] ![must-have][must-have] ![star][star]
    - [NQueens](NQueens.md) ![medium][medium] ![recommended][recommended] ![must-have][must-have] ![star][star]
    - [NQueens2](NQueens2.md) ![easy][easy] ![star][star]
- Graph search
    - [WordLadder2](WordLadder2.md) ![hard][hard] ![recommended][recommended] ![must-have][must-have] ![star0][star0]
- Non-recursion
- Others
  - Question list
    - [NextPermutation](NextPermutation.md) ![medium][medium] ![recommended][recommended] ![must-have][must-have] ![star][star]

## Time complexity

- O(numer of answers * time spent on each answer)
- Combination
  - 2^n * n
- Permutation
  - n! * n

## Notes

- DFS has __backtracking__ nature.
- For DFS, first build up a search tree.
- Actually if we don't optimize operations insied DFS for loop from O(n) to O(1), it's not that big deal. Because the main part of time complexity is 2^n or n!.
- **If we want to use HashMap to map Integer to Integer, then we can probably just use an array to do the mapping.**
- DFS does not need to have backtracking like number of islands, but if the question is about finding paths, then we need DFS to do backtracking.

## Appendix

- Time complexity growing speed

![](https://farm5.staticflickr.com/4189/34646069805_ca6c55be8e_o.png)

[must-have]: https://jaywcjlove.github.io/sb/ico/min-bibei.svg
[recommended]: https://jaywcjlove.github.io/sb/ico/min-tuijian.svg
[easy]: https://jaywcjlove.github.io/sb/ico/min-free.svg
[medium]: https://jaywcjlove.github.io/sb/ico/min-oss.svg
[hard]: https://jaywcjlove.github.io/sb/ico/min-hot.svg
[freq]: https://jaywcjlove.github.io/sb/ico/min-app-store.svg
[star]: https://jaywcjlove.github.io/sb/star/red.svg
[star0]: https://jaywcjlove.github.io/sb/star/gray.svg
[star1]: https://jaywcjlove.github.io/sb/star/red1.svg
[star2]: https://jaywcjlove.github.io/sb/star/red2.svg
[star3]: https://jaywcjlove.github.io/sb/star/red3.svg
[star4]: https://jaywcjlove.github.io/sb/star/red4.svg
[star5]: https://jaywcjlove.github.io/sb/star/red5.svg
