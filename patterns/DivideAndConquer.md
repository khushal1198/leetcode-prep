# DivideAndConquer

24 problems across 10 patterns.

## sorting_divide_and_conquer

**What it is** — Sorting via divide and conquer means recursively splitting an array into halves, sorting each half independently, then merging the results. Recognize this pattern when you need to implement a comparison-based sort from scratch or when a merge step can simultaneously gather extra information (e.g., inversion counts).

**Common steps**
1. Base case: if the subarray has 0 or 1 element, return immediately.
2. Find the midpoint: `mid = (lo + hi) // 2`.
3. Recursively sort the left half `[lo, mid]` and the right half `[mid+1, hi]`.
4. Merge the two sorted halves back into the original array using a two-pointer technique.
5. (Optional) During the merge step, collect any auxiliary information needed (counts, pairs).

**Key variations**
- Pure merge sort for sorting (e.g., Sort an Array)
- Modified merge to count inversions or cross-half pairs during the merge step

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 912 | [Sort an Array](https://leetcode.com/problems/sort-an-array/) | Medium | 4/10 | 55.9% | [x] |

## recursive_simulation

**What it is** — Recursive simulation uses the divide and conquer framework to build or simulate a structure by repeatedly halving or partitioning the input and combining results according to problem-specific rules. Recognize this when the output at level n is directly derived from two outputs at level n-1 with a simple transformation.

**Common steps**
1. Identify the base case (usually n=1 or a single element).
2. Recursively compute the result for the two halves or sub-levels.
3. Apply the problem-specific combination rule to merge the two sub-results.
4. Return the combined result.

**Key variations**
- String construction where the second half is a transformation of the first (reversal, negation)
- Bracket/match pairing where recursive structure mirrors the problem constraints

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 544 | [Output Contest Matches](https://leetcode.com/problems/output-contest-matches/) :lock: | Medium | 4/10 | 77.5% | [ ] |

## tree_construction_from_traversal

**What it is** — This pattern reconstructs a binary tree by identifying the root from one traversal sequence and then recursively partitioning the remaining elements into left and right subtrees. Recognize it when you are given one or two traversal arrays (preorder, inorder, postorder) and asked to rebuild the tree.

**Common steps**
1. Identify the root: it is always the first element of preorder or the last element of postorder.
2. Find the root's position in the other traversal to determine the split between left and right subtrees.
3. Recursively build the left subtree using the corresponding slice of each traversal.
4. Recursively build the right subtree using the remaining slice.
5. Link both subtrees to the root node and return it.

**Key variations**
- Preorder + inorder reconstruction (standard, unambiguous)
- Preorder + postorder reconstruction (slightly ambiguous for trees with one child)
- Finding the maximum element as root (Maximum Binary Tree variant)

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 654 | [Maximum Binary Tree](https://leetcode.com/problems/maximum-binary-tree/) | Medium | 4/10 | 86.4% | [ ] |
| 889 | [Construct Binary Tree from Preorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/) | Medium | 5/10 | 78.1% | [ ] |

## expression_divide_and_conquer

**What it is** — Expression divide and conquer splits a mathematical expression string at each operator, recursively evaluates all possible left and right sub-expressions, then combines every pair of results using the current operator. Recognize it when a problem asks for all possible values or ways to parenthesize an arithmetic expression.

**Common steps**
1. Base case: if the string contains no operator, parse and return the numeric value.
2. Iterate over every character; when you hit an operator, treat it as the "split point."
3. Recursively collect all results from the left substring and all results from the right substring.
4. Combine every (left result, right result) pair using the current operator.
5. Return the union of all combined results (often memoized by substring boundaries).

**Key variations**
- Return all possible values (list of integers)
- Return the count of distinct values or parenthesizations
- Memoization with a map from `(left_index, right_index)` to avoid recomputation

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 241 | [Different Ways to Add Parentheses](https://leetcode.com/problems/different-ways-to-add-parentheses/) | Medium | 5/10 | 73.2% | [ ] |

## quad_tree_divide_and_conquer

**What it is** — Quad tree divide and conquer recursively partitions a 2D grid into four equal quadrants, solving each quadrant independently, then deciding whether to merge them or keep them as separate leaves. Recognize it when a problem involves a 2D region that can be uniformly described (all same value) or must be further subdivided.

**Common steps**
1. Base case: if the entire subgrid has a uniform value, return a leaf node with that value.
2. Split the current region into four equal quadrants (top-left, top-right, bottom-left, bottom-right).
3. Recursively build the quad tree node for each quadrant.
4. If all four children are leaves with the same value, merge them into a single leaf.
5. Otherwise, create an internal node with the four children.

**Key variations**
- Constructing a quad tree from a grid (uniform vs. mixed regions)
- Merging two quad trees with logical operations (OR, AND)
- Filling a grid according to quad tree rules (inverse construction)

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 427 | [Construct Quad Tree](https://leetcode.com/problems/construct-quad-tree/) | Medium | 5/10 | 78.3% | [ ] |
| 3537 | [Fill a Special Grid](https://leetcode.com/problems/fill-a-special-grid/) | Medium | 5/10 | 70.9% | [ ] |
| 558 | [Logical OR of Two Binary Grids Represented as Quad-Trees](https://leetcode.com/problems/logical-or-of-two-binary-grids-represented-as-quad-trees/) | Medium | 6/10 | 52.4% | [ ] |

## string_divide_and_conquer

**What it is** — String divide and conquer identifies a "bad" character or position in a string that prevents the whole string from satisfying some property, splits the string at that point, and recursively solves each part. Recognize it when a global string property fails at specific characters, making independent processing of substrings valid.

**Common steps**
1. Check if the entire current substring satisfies the target property; if so, return it as-is.
2. Find a character or position that violates the property (e.g., a character with only uppercase or only lowercase).
3. Split the string at every occurrence of that violating character.
4. Recursively apply the function to each resulting substring.
5. Combine results (e.g., take the maximum-length valid substring, sort and concatenate).

**Key variations**
- Longest valid substring (return the best among all recursive results)
- Binary string structure problems where the string at level n is defined by operations on level n-1
- Partitioning to minimize cost with DP-like recurrences on substrings

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1763 | [Longest Nice Substring](https://leetcode.com/problems/longest-nice-substring/) | Easy | 3/10 | 64.3% | [ ] |
| 1545 | [Find Kth Bit in Nth Binary String](https://leetcode.com/problems/find-kth-bit-in-nth-binary-string/) | Medium | 4/10 | 73.7% | [ ] |
| 395 | [Longest Substring with At Least K Repeating Characters](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/) | Medium | 6/10 | 46.3% | [ ] |
| 3864 | [Minimum Cost to Partition a Binary String](https://leetcode.com/problems/minimum-cost-to-partition-a-binary-string/) | Hard | 7/10 | 52.4% | [ ] |
| 761 | [Special Binary String](https://leetcode.com/problems/special-binary-string/) | Hard | 8/10 | 79.3% | [ ] |

## spatial_divide_and_conquer

**What it is** — Spatial divide and conquer recursively partitions a 2D space (usually defined by coordinate bounds) and queries or counts objects within each partition, using the API or oracle available for that region. Recognize it when you must count or find something in a rectangle and can subdivide the rectangle to narrow down results.

**Common steps**
1. Define the current search region with corner coordinates.
2. Call the oracle/API for the current rectangle to get an aggregate result (e.g., count of ships).
3. Base case: if the result is 0 or the region is a single cell, return immediately.
4. Split the rectangle along its longer axis into two halves.
5. Recursively query both halves and combine the results (sum, min, etc.).

**Key variations**
- Binary search on one axis with recursion on the other
- Closest-pair-of-points style splitting (sort by x, recurse, then check cross-strip)
- Budget-constrained API calls (prune when the region result is already 0)

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1274 | [Number of Ships in a Rectangle](https://leetcode.com/problems/number-of-ships-in-a-rectangle/) :lock: | Hard | 7/10 | 68.9% | [ ] |
| 2613 | [Beautiful Pairs](https://leetcode.com/problems/beautiful-pairs/) :lock: | Hard | 8/10 | 48.9% | [ ] |

## merge_sort_inversion_count

**What it is** — This is an augmented merge sort where the merge step not only combines two sorted halves but simultaneously counts or collects cross-half pairs that satisfy a given inequality. Recognize it when a problem asks you to count pairs (i, j) with i < j and some relationship between values, which can be evaluated efficiently during a sorted merge.

**Common steps**
1. Base case: a single element has no pairs; return it as-is with count 0.
2. Split the array at the midpoint and recursively sort + count each half.
3. During the merge step, use two pointers — for each element in the right half, count how many elements in the left half form a valid pair with it (the sorted order lets you do this in O(n)).
4. Accumulate the cross-half count into a running total.
5. Finish the merge normally and return the sorted array along with the total count.

**Key variations**
- Simple inversion count: count pairs where `left[i] > right[j]`
- Generalized inequality: count pairs satisfying `left[i] > 2 * right[j]` (requires separate pointer)
- Range sum counting: prefix sums + sorted merge to count pairs within a value range

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 2426 | [Number of Pairs Satisfying Inequality](https://leetcode.com/problems/number-of-pairs-satisfying-inequality/) | Hard | 7/10 | 47.2% | [ ] |
| 315 | [Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/) | Hard | 8/10 | 43.6% | [ ] |
| 493 | [Reverse Pairs](https://leetcode.com/problems/reverse-pairs/) | Hard | 8/10 | 34.2% | [ ] |
| 327 | [Count of Range Sum](https://leetcode.com/problems/count-of-range-sum/) | Hard | 9/10 | 38.9% | [ ] |

## array_construction_divide_and_conquer

**What it is** — Array construction via divide and conquer builds an output array by separately constructing the left and right halves from sub-problems and then combining them, leveraging the fact that the target property is closed under the chosen combination rule. Recognize it when an array property is preserved when independently applied to disjoint index sets.

**Common steps**
1. Identify the invariant that must hold for the final array (e.g., no arithmetic progressions).
2. Express how a valid construction for size n can be derived from a valid construction for size n/2.
3. Recursively build the left and right halves using scaled or transformed indices.
4. Interleave or concatenate the two halves to form the full result.
5. Verify the invariant holds across the join boundary.

**Key variations**
- Deterministic construction by mathematical invariant (Beautiful Array)
- Reconstruction from subset sums by inferring which elements belong to each half

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 932 | [Beautiful Array](https://leetcode.com/problems/beautiful-array/) | Medium | 7/10 | 69.2% | [ ] |
| 1982 | [Find Array Given Subset Sums](https://leetcode.com/problems/find-array-given-subset-sums/) | Hard | 9/10 | 49.2% | [ ] |

## offline_query_divide_and_conquer

**What it is** — Offline query divide and conquer processes a set of queries by recursively splitting both the data and queries by a midpoint, answering the contribution of the left-half data to right-half queries (or vice versa) at each level, then recursing. Recognize it when queries span ranges of indices and you can decompose "cross contributions" efficiently at each level.

**Common steps**
1. Sort or arrange queries offline (no need to answer in input order).
2. Split the current data range at the midpoint.
3. For queries whose range crosses the midpoint, compute the contribution from the left half to the right half (e.g., using prefix structures built in O(n log n)).
4. Recurse on left data + left queries and right data + right queries independently.
5. Aggregate answers for each query across all levels of the recursion.

**Key variations**
- CDQ divide and conquer: 3D partial-order problems decomposed into 2D at each level
- XOR / multiplicative queries where cross-contributions can be computed with prefix aggregates
- Majority / threshold queries requiring sorted order and binary search at each level

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 2792 | [Count Nodes That Are Great Enough](https://leetcode.com/problems/count-nodes-that-are-great-enough/) :lock: | Hard | 8/10 | 56.6% | [ ] |
| 3655 | [XOR After Range Multiplication Queries II](https://leetcode.com/problems/xor-after-range-multiplication-queries-ii/) | Hard | 9/10 | 47.8% | [ ] |
| 3636 | [Threshold Majority Queries](https://leetcode.com/problems/threshold-majority-queries/) | Hard | 10/10 | 21.9% | [ ] |
