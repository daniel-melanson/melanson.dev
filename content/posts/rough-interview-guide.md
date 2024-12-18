+++
title = "A Rough Guide to Technical Interviews"
date = 2024-11-23
tags = "Career,LeetCode,Programming"
+++

## Background

While on the job hunt, I was fortunate enough to get a referral for an engineering position at a well-known tech company.
I spent nearly two months _grinding_ LeetCode and finishing [NeetCode 150](https://neetcode.io/practice).
After learning all the major patterns and purchasing a premium membership, I felt confident going into the technical screen.
That confidence was short lived.

After discussing the problem with my interviewer, I was feeling pretty good.
However, I rushed into implementing my ideas without thinking, wasted time hacking together a brute-force solution, and focused on irrelevant details.
I received a rejection letter the next day.

This blog post encapsulates my lessons, and wisdom from others, into a high-level guide for a macro-level approach to these type of LeetCode-style interviews.
Obviously, these steps should be done in order, but they do not need to be independent of each other ([Step 5](#5-decompose) and [Step 6](#6-implement) can be done in simultaneously).

Something not discussed in this post, but still important, is giving an nice introduction about yourself and ending the interview with questions about the company and role.
[This article](https://www.techinterviewhandbook.org/coding-interview-cheatsheet/) explains this in more detail.

## 0. Things To Consider

At the very least, your interviewer will be evaluating you on:

1. **Communication** - Ask clarifying questions. Discuss potential approaches and tradeoffs.
2. **Problem Solving** - Ability to understand, relate, and solve the problem.
3. **Implementation** - Write clean, efficient, and correct code.
4. **Testing** - Design normal and edge cases for your solution.
5. **Reasoning** - Ability to explain and reason about the complexity of applied algorithms, data structures, and solution.

Consider all of these aspects during your interview.
Do not focus on one aspect at the expense of the others.

Your ability to reason about the algorithmic complexity of your solution is something I do not think is discussed enough.
Always expect to be asked about the complexity of your solution.

## 1. Read

```python
def threeSum(nums: List[int]) -> List[List[int]]:
  """
  Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.
  """

  # Input: List[int]
  # Output: List[[int, int, int]] 
  # All possible triplets such that nums[i] + nums[j] + nums[k] == 0 and len(set([i, j, k])) == 3

  # Constraints:
  # - 3 <= nums.length <= 3000
  # - -10^5 <= nums[i] <= 10^5

  # Notes:
  # - Input can contain duplicates, but the output should not.
  # - Only one set for any input
  # - Output can be in any order

  pass
```

Read the problem statement out loud.
Repeat if necessary.
Establish an understanding of the following questions.
Write down the notes (in the shared file or on paper) if needed.

- What are the input and output types?
- Are there special cases to consider?
  - Examples: Empty input, negative numbers, duplicates, input on or near a bound.
- Is a valid and unique solution guaranteed each time?
  - If there can be no solution, what do we return?
  - If there are multiple solutions, which one do we return?

If input constraints are not explicitly stated, discuss them with them your interviewer.
Ask yourself if you can use the properties of the constraints to your advantage.

- Is the input guaranteed to be in a specific order?
- Is the domain of the input small enough to iterate through?
  - Example: Iterating through (or storing) lowercase English letters is $O(26)$ or $O(1)$.

## 2. Example

```python
nums = [0, 0, 0] # Extract arguments outside of the call for easy testing
print("Expected: [[0, 0, 0]], Actual: ", threeSum(nums)) # Print meaningful messages

nums = [-1, 0, 1, 2, -1, -4]
print("Expected: [[-1, 0, 1], [-1, -1, 2]], Actual: ", threeSum(nums))

nums = [0, 1, 1]
print("Expected: [], Actual: ", threeSum(nums))
```

Create your own test case beyond what was given to you.
Be specific (use real values).
Use sufficiently large input.
Avoid special cases.

Run through the example input out loud, on whiteboard, or on paper.
Ask yourself how changing the input could affect the output.

Take the initiative and write some driver code at the end of the file.
Your interviewer will probably have examples they want to test your code with.


## 3. Brute Force

```python
def threeSum(nums: List[int]) -> List[List[int]]:
  # initialize result set

  # loop through all possible triplets
    # check if the sum of the triplet is 0
    # check that the triplet is unique using result set
    # if it is, add it to the result

  # return the result 
```
Forget about developing an efficient algorithm.
State a naive approach out loud or using _rough_ pseudo-code.

Focus on the big picture, ignore the details of the implementation.
If there is some pre-processing, subroutine, or well-known algorithm you need to run, state it informally.
**Examples:** "Make an adjacency list", "Split the linked list in half", "Run DFS on each node to get max distance."
Do not waste time fleshing out the details of the implementation.

**Discuss this approach with your interviewer.**
Show that you are at least capable of understanding the problem.
This discussion can take up to 10 minutes (and likely strengthen your understanding of the problem).
Your interviewer may give you some hints that will guide you towards an optimal solution.


## 4. Optimize

```python
def threeSum(nums: List[int]) -> List[List[int]]:
  pass

  # Assuming (a + b + c == 0), we can reduce the problem to 2Sum with a target of -c
  # 2Sum can be solved in O(n) time using a hash table, but we need to check for duplicates
  # If we sort the input, we can use two pointers to find the two numbers that sum to -c and easily skip duplicates
```

This step is the most difficult and requires a significant amount of pattern recognition and the knowledge of similar problems.
I always recommend watching solutions to LeetCode problems to get a sense how to frame your thinking.

Walk through your brute force solution and look for bottlenecks, unnecessary computation, or duplicate work.

Helpful questions avoid duplicate work:
- Can I apply one of the common patterns to this problem?
  - Array, hash table, two pointers, sliding window, prefix sum, sliding window, divide and conquer, linked list, binary search, trees, graph, dynamic programming, heaps, backtracking, greedy algorithms, intervals, or bit manipulation.
- Is there any unused information from the problem I could use to my advantage?
- Does sorting the input help?
- If the brute force solution is recursive, can I use memoization to avoid redundant computation?
  - [10. Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/) or [115. Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/)
- Does inverting the problem help?
  - "Is it possible to go from point A to point B?" vs "Is it possible to go from point B to point A?"
  - [55. Jump Game](https://leetcode.com/problems/jump-game/), [417. Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/), or [312. Burst Balloons](https://leetcode.com/problems/burst-balloons/)
- If I consider the decision tree, can I reduce my decision space by skipping choices I have already made?
  - [40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/) or [518. Coin Change 2](https://leetcode.com/problems/coin-change-ii/)

## 5. Decompose

```python
def threeSum(nums: List[int]) -> List[List[int]]:
  # sort the input

  # loop through the input
    # skip if the same as previous or if the current number is positive
    # for each element, run two pointer 2Sum with a target of -nums[i]
      # add a found solution to the output
      # skip duplicates

  # return the output
```

Once you have a good idea for an optimal solution, take a moment to write down your ideas.
Use comments to decompose your algorithm into smaller steps.
Be concise and outline what is important, skip details relating to exact implementation.
Leave enough time to implement your solution.

If you use a data structure, state clearly what it stores and how elements are retrieved.

**Example:** "I'll use a hash table to map numbers to the index it was last seen at." could be written as:
```python
num_to_index = {} # (number -> index)
```

## 6. Implement

```python
def threeSum(nums: List[int]) -> List[List[int]]:
  # sort the input
  nums.sort()

  result = []
  for i, a in enumerate(nums):
    # skip if the same as previous or if the current number is positive
    if a > 0 and a == nums[i - 1]:
      continue

    # run two pointer 2Sum with a target of -nums[i]
    left, right = i + 1, len(nums) - 1
    while left < right:
      current_sum = a + nums[left] + nums[right]
      if current_sum < 0:
        left += 1
      elif current_sum > 0:
        right -= 1
      else:
        # add a found solution to the output
        result.append([a, nums[left], nums[right]])
        left += 1
        right -= 1
        # skip duplicates
        while nums[left] == nums[left - 1] and left < right:
          left += 1

  # return the output
  return result
```

If you have a good understanding of your solution, implementation should be the easiest step.
Remember that you do not need to write the entire solution from top to bottom.
Feel free to skip details if you get stuck; use pseudocode, stub bodies, and abstractions (functions, classes) to guide you if you do.

Use variable names that are descriptive and meaningful.
Strive to write [self-documenting](https://en.wikipedia.org/wiki/Self-documenting_code) code.

Write your solution in whatever programming language you practice LeetCode with.
I recommend Python for most problems and Go for bit manipulation.

Useful language features to know:

- The maximum and minimum possible numeric values (`math.inf`/`-math.inf`)
- Standard libraries ([`collections`](https://docs.python.org/3/library/collections.html), [`itertools`](https://docs.python.org/3/library/itertools.html), and [`bisect`](https://docs.python.org/3/library/bisect.html)) for data structures and algorithms

## 7. Test

Do a conceptual test of your solution by tracing through your code.
Double check conditions, loop bounds, initial values, and assumptions made.
Run your solution with the examples prepared in [Step 2](#2-example).

Review your solution with your interviewer and critique your own work.

## References

- [Tech Interview Handbook](https://www.techinterviewhandbook.org/)
- [NeetCode](https://neetcode.io/)
- [Cracking the Coding Interview](https://www.crackingthecodinginterview.com/)