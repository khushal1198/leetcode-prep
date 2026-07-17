# BinarySearch

162 problems across 14 patterns.

## classic_binary_search

**What it is** — Classic binary search eliminates half the search space each iteration by comparing a target against the middle element of a sorted collection. Recognize it when you need to find an exact value in O(log n) time and the input is sorted (or can be treated as sorted via an API).

**Common steps**
1. Set `lo = 0`, `hi = len(array) - 1`.
2. While `lo <= hi`, compute `mid = lo + (hi - lo) // 2`.
3. If `array[mid] == target`, return `mid`.
4. If `array[mid] < target`, move `lo = mid + 1`; otherwise move `hi = mid - 1`.
5. Return `-1` (or the appropriate sentinel) if the loop exits without a match.

**Key variations**
- Target is given explicitly vs. determined by an API (e.g., guess-number style problems).
- Array size is unknown, requiring exponential expansion of `hi` before binary search.
- The "array" is a virtual/implicit sequence accessed only through queries.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 704 | [Binary Search](https://leetcode.com/problems/binary-search/) | Easy | 1/10 | 60.8% | [ ] |
| 374 | [Guess Number Higher or Lower](https://leetcode.com/problems/guess-number-higher-or-lower/) | Easy | 1/10 | 57.5% | [ ] |
| 702 | [Search in a Sorted Array of Unknown Size](https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/) :lock: | Medium | 3/10 | 73.1% | [ ] |
| 1533 | [Find the Index of the Large Integer](https://leetcode.com/problems/find-the-index-of-the-large-integer/) :lock: | Medium | 4/10 | 56.6% | [ ] |

## boundary_search

**What it is** — Boundary search (also called "leftmost / rightmost binary search") finds the first or last position where a condition switches from false to true in a sorted array. Recognize it when you need the insertion point, the leftmost/rightmost occurrence of a value, or any problem that reduces to "find where property P first holds."

**Common steps**
1. Set `lo = 0`, `hi = len(array)` (use `hi = len - 1` for closed-interval variants; adjust based on whether the answer can be at index `len`).
2. While `lo < hi`, compute `mid = lo + (hi - lo) // 2`.
3. If the condition holds at `mid`, pull `hi = mid` (searching for the leftmost); otherwise push `lo = mid + 1`.
4. After the loop, `lo` is the leftmost index where the condition is true.
5. For rightmost boundary, flip the comparison: if the condition holds at `mid`, push `lo = mid + 1`; otherwise pull `hi = mid`. Answer is `lo - 1`.
6. Handle edge cases: target absent, all elements satisfy condition, no element satisfies condition.

**Key variations**
- Finding the first/last occurrence of an exact value (lower_bound / upper_bound).
- Finding the insertion index for a missing value (Search Insert Position).
- Searching for a structural property instead of a value (single non-duplicate element, fixed point, majority element).
- Combining two boundary searches (find first and last position simultaneously).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 2089 | [Find Target Indices After Sorting Array](https://leetcode.com/problems/find-target-indices-after-sorting-array/) | Easy | 1/10 | 78.0% | [ ] |
| 2529 | [Maximum Count of Positive Integer and Negative Integer](https://leetcode.com/problems/maximum-count-of-positive-integer-and-negative-integer/) | Easy | 1/10 | 74.3% | [ ] |
| 35 | [Search Insert Position](https://leetcode.com/problems/search-insert-position/) | Easy | 1/10 | 51.2% | [ ] |
| 1385 | [Find the Distance Value Between Two Arrays](https://leetcode.com/problems/find-the-distance-value-between-two-arrays/) | Easy | 2/10 | 71.7% | [ ] |
| 1608 | [Special Array With X Elements Greater Than or Equal X](https://leetcode.com/problems/special-array-with-x-elements-greater-than-or-equal-x/) | Easy | 2/10 | 66.8% | [ ] |
| 1064 | [Fixed Point](https://leetcode.com/problems/fixed-point/) :lock: | Easy | 2/10 | 63.8% | [ ] |
| 1150 | [Check If a Number Is Majority Element in a Sorted Array](https://leetcode.com/problems/check-if-a-number-is-majority-element-in-a-sorted-array/) :lock: | Easy | 2/10 | 59.9% | [ ] |
| 744 | [Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target/) | Easy | 2/10 | 59.1% | [ ] |
| 278 | [First Bad Version](https://leetcode.com/problems/first-bad-version/) | Easy | 2/10 | 47.1% | [ ] |
| 1539 | [Kth Missing Positive Number](https://leetcode.com/problems/kth-missing-positive-number/) | Easy | 3/10 | 63.4% | [ ] |
| 2300 | [Successful Pairs of Spells and Potions](https://leetcode.com/problems/successful-pairs-of-spells-and-potions/) | Medium | 3/10 | 49.6% | [ ] |
| 2936 | [Number of Equal Numbers Blocks](https://leetcode.com/problems/number-of-equal-numbers-blocks/) :lock: | Medium | 4/10 | 62.5% | [ ] |
| 1060 | [Missing Element in Sorted Array](https://leetcode.com/problems/missing-element-in-sorted-array/) :lock: | Medium | 4/10 | 59.7% | [ ] |
| 540 | [Single Element in a Sorted Array](https://leetcode.com/problems/single-element-in-a-sorted-array/) | Medium | 4/10 | 59.3% | [x] |
| 34 | [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) | Medium | 4/10 | 48.8% | [x] |
| 3350 | [Adjacent Increasing Subarrays Detection II](https://leetcode.com/problems/adjacent-increasing-subarrays-detection-ii/) | Medium | 5/10 | 58.9% | [ ] |
| 658 | [Find K Closest Elements](https://leetcode.com/problems/find-k-closest-elements/) | Medium | 5/10 | 49.6% | [ ] |
| 275 | [H-Index II](https://leetcode.com/problems/h-index-ii/) | Medium | 5/10 | 39.6% | [ ] |
| 2557 | [Maximum Number of Integers to Choose From a Range II](https://leetcode.com/problems/maximum-number-of-integers-to-choose-from-a-range-ii/) :lock: | Medium | 5/10 | 34.8% | [ ] |
| 3143 | [Maximum Points Inside the Square](https://leetcode.com/problems/maximum-points-inside-the-square/) | Medium | 6/10 | 39.6% | [ ] |

## matrix_search

**What it is** — Matrix search applies binary search to 2-D grids where rows and/or columns are sorted, enabling sub-linear scans. Recognize it when the matrix has a monotone structure that lets you map a 1-D index onto 2-D coordinates, or prune entire rows/columns at each step.

**Common steps**
1. Determine the structure: fully sorted row-major (treat as 1-D) vs. row-sorted + column-sorted (staircase search) vs. binary property per row (per-row binary search).
2. For fully sorted matrix: map `mid` index to `(mid // cols, mid % cols)` and run standard binary search.
3. For row-sorted + column-sorted: start at top-right (or bottom-left) corner; move left if current > target, move down if current < target.
4. For per-row binary search: binary search each row independently, or binary search over rows to find the relevant row first.
5. Handle out-of-bounds and edge cases (empty matrix, single row/column).

**Key variations**
- Fully sorted row-major matrix (Search a 2D Matrix) vs. partially sorted (Search a 2D Matrix II).
- Counting elements satisfying a condition (count negatives) vs. locating a specific value.
- Finding boundaries in a 2-D binary matrix (leftmost column with a one, smallest rectangle).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1351 | [Count Negative Numbers in a Sorted Matrix](https://leetcode.com/problems/count-negative-numbers-in-a-sorted-matrix/) | Easy | 2/10 | 79.6% | [ ] |
| 1337 | [The K Weakest Rows in a Matrix](https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/) | Easy | 3/10 | 74.3% | [ ] |
| 1428 | [Leftmost Column with at Least a One](https://leetcode.com/problems/leftmost-column-with-at-least-a-one/) :lock: | Medium | 4/10 | 55.2% | [ ] |
| 74 | [Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/) | Medium | 4/10 | 53.9% | [x] |
| 240 | [Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/) | Medium | 5/10 | 57.2% | [ ] |
| 302 | [Smallest Rectangle Enclosing Black Pixels](https://leetcode.com/problems/smallest-rectangle-enclosing-black-pixels/) :lock: | Hard | 7/10 | 60.9% | [ ] |

## rotated_array

**What it is** — A rotated sorted array has been split at some pivot and the two sorted halves swapped, creating exactly one "break point" in sorted order. Binary search still works because at least one half of any `[lo, mid]` or `[mid, hi]` window is guaranteed to be fully sorted, allowing you to decide which half to search.

**Common steps**
1. Set `lo = 0`, `hi = len - 1`.
2. Compute `mid = lo + (hi - lo) // 2`.
3. Determine which half is sorted: if `array[lo] <= array[mid]`, the left half is sorted; otherwise the right half is sorted.
4. Check whether the target falls inside the sorted half; if yes, restrict search to that half; otherwise restrict to the other half.
5. Repeat until `lo > hi` or the element is found.
6. For finding the minimum: track which side the break point is on and always move toward the unsorted side.

**Key variations**
- Searching for a target value vs. finding the rotation pivot (minimum element).
- Arrays with all-unique elements vs. arrays with duplicates (duplicates force worst-case O(n) in some implementations).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 153 | [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) | Medium | 4/10 | 54.1% | [x] |
| 33 | [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) | Medium | 5/10 | 44.5% | [x] |
| 154 | [Find Minimum in Rotated Sorted Array II](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/) | Hard | 6/10 | 44.9% | [ ] |
| 81 | [Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/) | Medium | 6/10 | 40.0% | [ ] |

## peak_finding

**What it is** — Peak finding uses the local slope (comparing `mid` with its neighbors) to determine which direction to move, guaranteeing convergence to a peak even without a globally sorted array. Recognize it when you need to find any element larger than its neighbors and can discard half the array based on the slope direction.

**Common steps**
1. Set `lo = 0`, `hi = len - 1`.
2. Compute `mid = lo + (hi - lo) // 2`.
3. Compare `array[mid]` with `array[mid + 1]` (ensure `mid + 1` is in bounds).
4. If `array[mid] < array[mid + 1]`, a peak lies to the right: set `lo = mid + 1`.
5. Otherwise a peak lies at `mid` or to the left: set `hi = mid`.
6. When `lo == hi`, that index is a peak; return it.

**Key variations**
- 1-D peak (Find Peak Element) vs. 2-D peak (Find a Peak Element II — binary search on rows, linear scan on columns).
- Mountain array where the peak is unique and you must search both ascending and descending sides for a target (Find in Mountain Array).
- Peak index is asked directly vs. needing to return the peak value.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 852 | [Peak Index in a Mountain Array](https://leetcode.com/problems/peak-index-in-a-mountain-array/) | Medium | 3/10 | 66.9% | [ ] |
| 162 | [Find Peak Element](https://leetcode.com/problems/find-peak-element/) | Medium | 5/10 | 46.9% | [x] |
| 1901 | [Find a Peak Element II](https://leetcode.com/problems/find-a-peak-element-ii/) | Medium | 7/10 | 54.7% | [ ] |
| 1095 | [Find in Mountain Array](https://leetcode.com/problems/find-in-mountain-array/) | Hard | 7/10 | 41.6% | [ ] |

## prefix_sum_binary_search

**What it is** — This pattern combines a precomputed prefix sum array with binary search to answer range-sum or threshold queries in O(log n) after O(n) preprocessing. Recognize it when you need to repeatedly ask "what is the sum of elements in some range?" or "at what index does the running sum first exceed a threshold?"

**Common steps**
1. Sort the input if needed, then build a prefix sum array `pre` where `pre[i] = pre[i-1] + arr[i-1]`.
2. For each query threshold `q`, binary search on `pre` for the leftmost index where `pre[mid] >= q` (or `> q` depending on the problem).
3. Use `bisect_left` / `bisect_right` (Python) or equivalent for clean implementation.
4. Translate the index back to the original array context to produce the answer.
5. Handle edge cases: query larger than total sum, empty prefix sum, off-by-one from 0-indexed vs. 1-indexed prefix arrays.

**Key variations**
- Offline queries (sort queries, then binary search) vs. online queries (use a sorted structure for each query).
- 1-D prefix sum vs. 2-D prefix sum (Max Sum of Rectangle No Larger Than K).
- Sorting the array first to enable prefix sums (Range Sum of Sorted Subarray Sums).
- Binary searching for a count rather than a sum (Count Number of Rectangles Containing Each Point).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 2389 | [Longest Subsequence With Limited Sum](https://leetcode.com/problems/longest-subsequence-with-limited-sum/) | Easy | 2/10 | 73.6% | [ ] |
| 2838 | [Maximum Coins Heroes Can Collect](https://leetcode.com/problems/maximum-coins-heroes-can-collect/) :lock: | Medium | 4/10 | 68.7% | [ ] |
| 1170 | [Compare Strings by Frequency of the Smallest Character](https://leetcode.com/problems/compare-strings-by-frequency-of-the-smallest-character/) | Medium | 4/10 | 63.3% | [ ] |
| 2070 | [Most Beautiful Item for Each Query](https://leetcode.com/problems/most-beautiful-item-for-each-query/) | Medium | 4/10 | 62.1% | [ ] |
| 1182 | [Shortest Distance to Target Color](https://leetcode.com/problems/shortest-distance-to-target-color/) :lock: | Medium | 4/10 | 56.5% | [ ] |
| 1894 | [Find the Student that Will Replace the Chalk](https://leetcode.com/problems/find-the-student-that-will-replace-the-chalk/) | Medium | 4/10 | 53.2% | [ ] |
| 1292 | [Maximum Side Length of a Square with Sum Less than or Equal to Threshold](https://leetcode.com/problems/maximum-side-length-of-a-square-with-sum-less-than-or-equal-to-threshold/) | Medium | 5/10 | 65.4% | [ ] |
| 911 | [Online Election](https://leetcode.com/problems/online-election/) | Medium | 5/10 | 52.8% | [ ] |
| 792 | [Number of Matching Subsequences](https://leetcode.com/problems/number-of-matching-subsequences/) | Medium | 5/10 | 50.6% | [ ] |
| 3152 | [Special Array II](https://leetcode.com/problems/special-array-ii/) | Medium | 5/10 | 45.8% | [ ] |
| 2602 | [Minimum Operations to Make All Array Elements Equal](https://leetcode.com/problems/minimum-operations-to-make-all-array-elements-equal/) | Medium | 5/10 | 38.3% | [ ] |
| 1818 | [Minimum Absolute Sum Difference](https://leetcode.com/problems/minimum-absolute-sum-difference/) | Medium | 5/10 | 32.4% | [ ] |
| 1508 | [Range Sum of Sorted Subarray Sums](https://leetcode.com/problems/range-sum-of-sorted-subarray-sums/) | Medium | 6/10 | 63.0% | [ ] |
| 2250 | [Count Number of Rectangles Containing Each Point](https://leetcode.com/problems/count-number-of-rectangles-containing-each-point/) | Medium | 6/10 | 37.6% | [ ] |
| 2271 | [Maximum White Tiles Covered by a Carpet](https://leetcode.com/problems/maximum-white-tiles-covered-by-a-carpet/) | Medium | 6/10 | 35.8% | [ ] |
| 1712 | [Ways to Split Array Into Three Subarrays](https://leetcode.com/problems/ways-to-split-array-into-three-subarrays/) | Medium | 6/10 | 34.2% | [ ] |
| 3771 | [Total Score of Dungeon Runs](https://leetcode.com/problems/total-score-of-dungeon-runs/) | Medium | 6/10 | 30.8% | [ ] |
| 3520 | [Minimum Threshold for Inversion Pairs Count](https://leetcode.com/problems/minimum-threshold-for-inversion-pairs-count/) :lock: | Medium | 7/10 | 55.0% | [ ] |
| 2819 | [Minimum Relative Loss After Buying Chocolates](https://leetcode.com/problems/minimum-relative-loss-after-buying-chocolates/) :lock: | Hard | 7/10 | 46.3% | [ ] |
| 3109 | [Find the Index of Permutation](https://leetcode.com/problems/find-the-index-of-permutation/) :lock: | Medium | 7/10 | 36.5% | [ ] |
| 1889 | [Minimum Space Wasted From Packaging](https://leetcode.com/problems/minimum-space-wasted-from-packaging/) | Hard | 8/10 | 33.5% | [ ] |
| 3748 | [Count Stable Subarrays](https://leetcode.com/problems/count-stable-subarrays/) | Hard | 8/10 | 32.6% | [ ] |
| 363 | [Max Sum of Rectangle No Larger Than K](https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/) | Hard | 9/10 | 45.5% | [ ] |
| 2234 | [Maximum Total Beauty of the Gardens](https://leetcode.com/problems/maximum-total-beauty-of-the-gardens/) | Hard | 9/10 | 30.2% | [ ] |

## math_binary_search

**What it is** — Math binary search applies binary search to a monotone mathematical function rather than an array, treating a numeric range as the search space. Recognize it when you need to find an integer (e.g., a square root, a coin-row count, or an LCM-based Nth term) and can write a function `f(x)` that is non-decreasing or non-increasing over candidate values.

**Common steps**
1. Identify the search space: set `lo` and `hi` to the smallest and largest plausible integer answers.
2. Define a monotone predicate `f(mid)` that evaluates whether `mid` is a valid or over/under-estimate.
3. Binary search: compute `mid = lo + (hi - lo) // 2`, evaluate `f(mid)`, and move `lo` or `hi` accordingly.
4. Watch for integer overflow when computing `f(mid)` (use `//` for integer arithmetic, avoid squaring large values naively).
5. After the loop, `lo` (or `lo - 1`) is the answer; verify with an exact check if needed.

**Key variations**
- Integer square/cube root problems (Sqrt(x), Valid Perfect Square).
- Closed-form formula search (Arranging Coins — triangular number inversion).
- LCM/GCD-based counting (Nth Magical Number, Preimage Size of Factorial Zeroes).
- Bit-level computation over a range (Maximum Number That Sum of the Prices Is Less Than or Equal to K).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 441 | [Arranging Coins](https://leetcode.com/problems/arranging-coins/) | Easy | 2/10 | 48.2% | [ ] |
| 367 | [Valid Perfect Square](https://leetcode.com/problems/valid-perfect-square/) | Easy | 2/10 | 44.9% | [ ] |
| 69 | [Sqrt(x)](https://leetcode.com/problems/sqrtx/) | Easy | 2/10 | 41.8% | [ ] |
| 1954 | [Minimum Garden Perimeter to Collect Enough Apples](https://leetcode.com/problems/minimum-garden-perimeter-to-collect-enough-apples/) | Medium | 4/10 | 55.6% | [ ] |
| 3296 | [Minimum Number of Seconds to Make Mountain Height Zero](https://leetcode.com/problems/minimum-number-of-seconds-to-make-mountain-height-zero/) | Medium | 5/10 | 58.3% | [ ] |
| 3453 | [Separate Squares I](https://leetcode.com/problems/separate-squares-i/) | Medium | 5/10 | 58.0% | [ ] |
| 3639 | [Minimum Time to Activate String](https://leetcode.com/problems/minimum-time-to-activate-string/) | Medium | 5/10 | 49.2% | [ ] |
| 2513 | [Minimize the Maximum of Two Arrays](https://leetcode.com/problems/minimize-the-maximum-of-two-arrays/) | Medium | 6/10 | 32.3% | [ ] |
| 3007 | [Maximum Number That Sum of the Prices Is Less Than or Equal to K](https://leetcode.com/problems/maximum-number-that-sum-of-the-prices-is-less-than-or-equal-to-k/) | Medium | 7/10 | 38.6% | [ ] |
| 878 | [Nth Magical Number](https://leetcode.com/problems/nth-magical-number/) | Hard | 7/10 | 36.7% | [ ] |
| 3344 | [Maximum Sized Array](https://leetcode.com/problems/maximum-sized-array/) :lock: | Medium | 8/10 | 51.5% | [ ] |
| 793 | [Preimage Size of Factorial Zeroes Function](https://leetcode.com/problems/preimage-size-of-factorial-zeroes-function/) | Hard | 8/10 | 47.0% | [ ] |
| 1956 | [Minimum Time for K Virus Variants to Spread](https://leetcode.com/problems/minimum-time-for-k-virus-variants-to-spread/) :lock: | Hard | 9/10 | 50.7% | [ ] |
| 3116 | [Kth Smallest Amount With Single Denomination Combination](https://leetcode.com/problems/kth-smallest-amount-with-single-denomination-combination/) | Hard | 9/10 | 20.2% | [ ] |
| 3145 | [Find Products of Elements of Big Array](https://leetcode.com/problems/find-products-of-elements-of-big-array/) | Hard | 10/10 | 24.6% | [ ] |

## search_on_answer_minimize_maximum

**What it is** — "Search on answer" (minimize the maximum) binary searches directly on the answer value rather than an index. The key insight is that the feasibility function "can we achieve a maximum of at most X?" is monotone: if X works, any larger value also works, so we can binary search for the smallest X that is feasible. Recognize it when a problem asks for the minimum possible value of the largest element (or cost, or time) under some partitioning or assignment constraint.

**Common steps**
1. Define the search space: `lo = minimum conceivable answer`, `hi = maximum conceivable answer` (e.g., max element, total sum).
2. Write a `feasible(mid)` function that checks whether it is possible to satisfy all constraints with maximum value `mid`. This usually involves a greedy scan.
3. Binary search: while `lo < hi`, set `mid = lo + (hi - lo) // 2`. If `feasible(mid)`, set `hi = mid`; else set `lo = mid + 1`.
4. Return `lo` as the minimum feasible maximum.
5. Verify the `feasible` function is correct at the boundary — off-by-one in greedy logic is the most common bug.

**Key variations**
- Splitting an array into k parts (Split Array Largest Sum, Capacity to Ship in D Days).
- Assigning tasks to workers or machines (Minimum Time to Complete Trips, Minimum Time to Repair Cars).
- Operations applied to elements (Minimum Limit of Balls in a Bag, Find the Smallest Divisor).
- Geometric or string constraints (Minimize Max Distance to Gas Station, Smallest Substring With Identical Characters).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1011 | [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) | Medium | 4/10 | 73.9% | [x] |
| 1760 | [Minimum Limit of Balls in a Bag](https://leetcode.com/problems/minimum-limit-of-balls-in-a-bag/) | Medium | 4/10 | 66.3% | [ ] |
| 1283 | [Find the Smallest Divisor Given a Threshold](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/) | Medium | 4/10 | 65.8% | [ ] |
| 1618 | [Maximum Font to Fit a Sentence in a Screen](https://leetcode.com/problems/maximum-font-to-fit-a-sentence-in-a-screen/) :lock: | Medium | 4/10 | 62.1% | [ ] |
| 2594 | [Minimum Time to Repair Cars](https://leetcode.com/problems/minimum-time-to-repair-cars/) | Medium | 4/10 | 59.5% | [ ] |
| 1891 | [Cutting Ribbons](https://leetcode.com/problems/cutting-ribbons/) :lock: | Medium | 4/10 | 53.0% | [ ] |
| 875 | [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) | Medium | 4/10 | 50.0% | [x] |
| 1870 | [Minimum Speed to Arrive on Time](https://leetcode.com/problems/minimum-speed-to-arrive-on-time/) | Medium | 4/10 | 47.8% | [ ] |
| 2187 | [Minimum Time to Complete Trips](https://leetcode.com/problems/minimum-time-to-complete-trips/) | Medium | 4/10 | 39.8% | [ ] |
| 2137 | [Pour Water Between Buckets to Make Water Levels Equal](https://leetcode.com/problems/pour-water-between-buckets-to-make-water-levels-equal/) :lock: | Medium | 5/10 | 68.4% | [ ] |
| 2560 | [House Robber IV](https://leetcode.com/problems/house-robber-iv/) | Medium | 5/10 | 64.7% | [ ] |
| 2064 | [Minimized Maximum of Products Distributed to Any Store](https://leetcode.com/problems/minimized-maximum-of-products-distributed-to-any-store/) | Medium | 5/10 | 63.1% | [ ] |
| 1482 | [Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/) | Medium | 5/10 | 56.5% | [ ] |
| 2616 | [Minimize the Maximum Difference of Pairs](https://leetcode.com/problems/minimize-the-maximum-difference-of-pairs/) | Medium | 5/10 | 50.9% | [ ] |
| 1898 | [Maximum Number of Removable Characters](https://leetcode.com/problems/maximum-number-of-removable-characters/) | Medium | 5/10 | 47.1% | [ ] |
| 2439 | [Minimize Maximum of Array](https://leetcode.com/problems/minimize-maximum-of-array/) | Medium | 5/10 | 46.5% | [ ] |
| 1300 | [Sum of Mutated Array Closest to Target](https://leetcode.com/problems/sum-of-mutated-array-closest-to-target/) | Medium | 5/10 | 46.3% | [ ] |
| 475 | [Heaters](https://leetcode.com/problems/heaters/) | Medium | 5/10 | 41.8% | [ ] |
| 3824 | [Minimum K to Reduce Array Within Limit](https://leetcode.com/problems/minimum-k-to-reduce-array-within-limit/) | Medium | 5/10 | 41.1% | [ ] |
| 3048 | [Earliest Second to Mark Indices I](https://leetcode.com/problems/earliest-second-to-mark-indices-i/) | Medium | 5/10 | 36.8% | [ ] |
| 1918 | [Kth Smallest Subarray Sum](https://leetcode.com/problems/kth-smallest-subarray-sum/) :lock: | Medium | 6/10 | 53.4% | [ ] |
| 3356 | [Zero Array Transformation II](https://leetcode.com/problems/zero-array-transformation-ii/) | Medium | 6/10 | 43.6% | [ ] |
| 3733 | [Minimum Time to Complete All Deliveries](https://leetcode.com/problems/minimum-time-to-complete-all-deliveries/) | Medium | 6/10 | 35.2% | [ ] |
| 410 | [Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/) | Hard | 7/10 | 60.4% | [ ] |
| 774 | [Minimize Max Distance to Gas Station](https://leetcode.com/problems/minimize-max-distance-to-gas-station/) :lock: | Hard | 8/10 | 54.0% | [ ] |
| 2448 | [Minimum Cost to Make Array Equal](https://leetcode.com/problems/minimum-cost-to-make-array-equal/) | Hard | 8/10 | 46.8% | [ ] |
| 2702 | [Minimum Operations to Make Numbers Non-positive](https://leetcode.com/problems/minimum-operations-to-make-numbers-non-positive/) :lock: | Hard | 8/10 | 44.1% | [ ] |
| 2604 | [Minimum Time to Eat All Grains](https://leetcode.com/problems/minimum-time-to-eat-all-grains/) :lock: | Hard | 8/10 | 40.7% | [ ] |
| 3399 | [Smallest Substring With Identical Characters II](https://leetcode.com/problems/smallest-substring-with-identical-characters-ii/) | Hard | 8/10 | 40.2% | [ ] |
| 644 | [Maximum Average Subarray II](https://leetcode.com/problems/maximum-average-subarray-ii/) :lock: | Hard | 8/10 | 37.7% | [ ] |
| 3049 | [Earliest Second to Mark Indices II](https://leetcode.com/problems/earliest-second-to-mark-indices-ii/) | Hard | 8/10 | 22.6% | [ ] |
| 3398 | [Smallest Substring With Identical Characters I](https://leetcode.com/problems/smallest-substring-with-identical-characters-i/) | Hard | 8/10 | 20.6% | [ ] |
| 2071 | [Maximum Number of Tasks You Can Assign](https://leetcode.com/problems/maximum-number-of-tasks-you-can-assign/) | Hard | 9/10 | 50.1% | [ ] |
| 2565 | [Subsequence With the Minimum Score](https://leetcode.com/problems/subsequence-with-the-minimum-score/) | Hard | 9/10 | 33.2% | [ ] |
| 3605 | [Minimum Stability Factor of Array](https://leetcode.com/problems/minimum-stability-factor-of-array/) | Hard | 9/10 | 20.6% | [ ] |
| 3357 | [Minimize the Maximum Adjacent Element Difference](https://leetcode.com/problems/minimize-the-maximum-adjacent-element-difference/) | Hard | 9/10 | 19.7% | [ ] |

## interval_binary_search

**What it is** — Interval binary search applies binary search to sorted interval endpoints to efficiently answer queries about overlapping, adjacent, or nearest intervals. Recognize it when you are given a set of intervals and need to quickly find the first interval that starts after a given point, or check whether a new interval overlaps any existing one.

**Common steps**
1. Sort intervals by their start (or end) point.
2. Extract start points (or end points) into a separate array for fast binary search.
3. For each query point `q`, use `bisect_left` / `bisect_right` to find the first interval starting at or after `q`.
4. Check the interval immediately before and after the insertion point to handle overlaps or "closest" comparisons.
5. For dynamic insertion (My Calendar I), maintain a sorted structure (e.g., `SortedList`) and use binary search to detect conflicts before inserting.

**Key variations**
- Finding the first non-overlapping interval to the right (Find Right Interval).
- Checking for overlap before inserting (My Calendar I).
- Optimizing over two non-overlapping segments simultaneously (Two Best Non-Overlapping Events, Maximize Win From Two Segments).
- Answering point-in-interval queries at scale (Number of Flowers in Full Bloom).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 436 | [Find Right Interval](https://leetcode.com/problems/find-right-interval/) | Medium | 4/10 | 55.8% | [ ] |
| 2054 | [Two Best Non-Overlapping Events](https://leetcode.com/problems/two-best-non-overlapping-events/) | Medium | 5/10 | 64.0% | [ ] |
| 729 | [My Calendar I](https://leetcode.com/problems/my-calendar-i/) | Medium | 5/10 | 58.3% | [ ] |
| 3488 | [Closest Equal Element Queries](https://leetcode.com/problems/closest-equal-element-queries/) | Medium | 5/10 | 51.4% | [ ] |
| 2555 | [Maximize Win From Two Segments](https://leetcode.com/problems/maximize-win-from-two-segments/) | Medium | 6/10 | 37.8% | [ ] |
| 2817 | [Minimum Absolute Difference Between Elements With Constraint](https://leetcode.com/problems/minimum-absolute-difference-between-elements-with-constraint/) | Medium | 6/10 | 37.6% | [ ] |
| 3635 | [Earliest Finish Time for Land and Water Rides II](https://leetcode.com/problems/earliest-finish-time-for-land-and-water-rides-ii/) | Medium | 6/10 | 35.3% | [ ] |
| 2251 | [Number of Flowers in Full Bloom](https://leetcode.com/problems/number-of-flowers-in-full-bloom/) | Hard | 7/10 | 57.8% | [ ] |
| 3661 | [Maximum Walls Destroyed by Robots](https://leetcode.com/problems/maximum-walls-destroyed-by-robots/) | Hard | 8/10 | 48.0% | [ ] |
| 1847 | [Closest Room](https://leetcode.com/problems/closest-room/) | Hard | 8/10 | 41.2% | [ ] |

## search_on_answer_maximize_minimum

**What it is** — The mirror image of minimize-maximum: binary search on the answer to find the largest value X such that you can satisfy all constraints with a minimum of at least X. The feasibility function "can we achieve a minimum of at least X?" is monotone decreasing, so we binary search for the largest feasible X. Recognize it when the problem asks for the maximum possible value of the smallest element (or gap, or score).

**Common steps**
1. Define the search space: `lo = minimum conceivable answer`, `hi = maximum conceivable answer`.
2. Write a `feasible(mid)` function that greedily checks whether all constraints can be met with minimum value `mid`.
3. Binary search: while `lo < hi`, set `mid = lo + (hi - lo + 1) // 2` (use ceiling mid to avoid infinite loop when `lo + 1 == hi`). If `feasible(mid)`, set `lo = mid`; else set `hi = mid - 1`.
4. Return `lo` as the maximum feasible minimum.
5. Double-check the greedy strategy in `feasible` — typically sort the input first and place elements greedily.

**Key variations**
- Placing objects with minimum distance (Magnetic Force Between Two Balls, Maximize Score of Numbers in Ranges).
- Allocating resources to maximize the minimum allocation (Maximum Candies Allocated to K Children, Divide Chocolate).
- Power/capacity distribution problems (Maximize the Minimum Powered City, Maximum Running Time of N Computers).
- Combined allocation with multiple constraints (Maximum Number of Alloys).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 2226 | [Maximum Candies Allocated to K Children](https://leetcode.com/problems/maximum-candies-allocated-to-k-children/) | Medium | 4/10 | 49.9% | [ ] |
| 1552 | [Magnetic Force Between Two Balls](https://leetcode.com/problems/magnetic-force-between-two-balls/) | Medium | 5/10 | 72.1% | [ ] |
| 2517 | [Maximum Tastiness of Candy Basket](https://leetcode.com/problems/maximum-tastiness-of-candy-basket/) | Medium | 5/10 | 68.1% | [ ] |
| 3155 | [Maximum Number of Upgradable Servers](https://leetcode.com/problems/maximum-number-of-upgradable-servers/) :lock: | Medium | 5/10 | 43.4% | [ ] |
| 2861 | [Maximum Number of Alloys](https://leetcode.com/problems/maximum-number-of-alloys/) | Medium | 5/10 | 40.9% | [ ] |
| 3281 | [Maximize Score of Numbers in Ranges](https://leetcode.com/problems/maximize-score-of-numbers-in-ranges/) | Medium | 5/10 | 35.7% | [ ] |
| 1802 | [Maximum Value at a Given Index in a Bounded Array](https://leetcode.com/problems/maximum-value-at-a-given-index-in-a-bounded-array/) | Medium | 6/10 | 38.9% | [ ] |
| 1231 | [Divide Chocolate](https://leetcode.com/problems/divide-chocolate/) :lock: | Hard | 7/10 | 60.5% | [ ] |
| 2528 | [Maximize the Minimum Powered City](https://leetcode.com/problems/maximize-the-minimum-powered-city/) | Hard | 8/10 | 61.7% | [ ] |
| 2141 | [Maximum Running Time of N Computers](https://leetcode.com/problems/maximum-running-time-of-n-computers/) | Hard | 8/10 | 56.4% | [ ] |
| 2790 | [Maximum Number of Groups With Increasing Length](https://leetcode.com/problems/maximum-number-of-groups-with-increasing-length/) | Hard | 8/10 | 23.1% | [ ] |
| 3464 | [Maximize the Distance Between Points on a Square](https://leetcode.com/problems/maximize-the-distance-between-points-on-a-square/) | Hard | 9/10 | 51.2% | [ ] |
| 3449 | [Maximize the Minimum Game Score](https://leetcode.com/problems/maximize-the-minimum-game-score/) | Hard | 9/10 | 26.3% | [ ] |

## rolling_hash_binary_search

**What it is** — This pattern combines binary search on length with rolling hash (Rabin-Karp style) to efficiently find the longest substring or subpath satisfying a repetition or similarity condition. Recognize it when asked for the longest duplicate/repeating substring and brute force O(n^2) comparison is too slow — binary search halves the candidate lengths while hashing makes equality checks O(1) per position.

**Common steps**
1. Binary search on the candidate length `L`: `lo = 1`, `hi = len(s) - 1`.
2. For a given `L`, compute rolling hashes of all substrings of length `L` using a polynomial hash with a large prime modulus.
3. Store hashes in a set; if any hash appears more than once (or k times), the condition is met — set `lo = L`; otherwise set `hi = L - 1`.
4. Use double hashing (two different bases/mods) to reduce collision probability for hard problems.
5. After binary search, reconstruct the actual substring if needed by re-scanning at the final length.

**Key variations**
- Duplicate substring (Longest Duplicate Substring) vs. substring occurring exactly k times (Find Longest Special Substring That Occurs Thrice).
- Single string (Longest Repeating Substring) vs. multiple arrays (Longest Common Subpath — apply rolling hash to each array, intersect hash sets).
- Collision handling: single hash sufficient for easier problems; double hash needed for hard constraints.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 2981 | [Find Longest Special Substring That Occurs Thrice I](https://leetcode.com/problems/find-longest-special-substring-that-occurs-thrice-i/) | Medium | 5/10 | 61.8% | [ ] |
| 1062 | [Longest Repeating Substring](https://leetcode.com/problems/longest-repeating-substring/) :lock: | Medium | 6/10 | 63.4% | [ ] |
| 2982 | [Find Longest Special Substring That Occurs Thrice II](https://leetcode.com/problems/find-longest-special-substring-that-occurs-thrice-ii/) | Medium | 6/10 | 39.2% | [ ] |
| 1044 | [Longest Duplicate Substring](https://leetcode.com/problems/longest-duplicate-substring/) | Hard | 8/10 | 31.1% | [ ] |
| 1923 | [Longest Common Subpath](https://leetcode.com/problems/longest-common-subpath/) | Hard | 9/10 | 29.5% | [ ] |

## kth_smallest_binary_search

**What it is** — Kth smallest binary search finds the k-th smallest value in an implicit sorted sequence (matrix, multiplication table, pair products) without enumerating all elements. The core idea: binary search on the value X and count how many elements are <= X; the k-th smallest is the smallest X where that count >= k.

**Common steps**
1. Set `lo = smallest possible value`, `hi = largest possible value` in the search space.
2. Write a `count(mid)` function that counts how many elements in the structure are <= `mid` in O(n) or O(n log n).
3. Binary search: while `lo < hi`, compute `mid = lo + (hi - lo) // 2`. If `count(mid) >= k`, set `hi = mid`; else set `lo = mid + 1`.
4. Return `lo` — it is the smallest value with at least k elements <= it, i.e., the k-th smallest.
5. For sorted matrices, count using a row-by-row binary search (O(n log n) total); for multiplication tables, use division per row (O(n) total).

**Key variations**
- Sorted matrix (Kth Smallest Element in a Sorted Matrix) vs. multiplication table (Kth Smallest Number in Multiplication Table).
- Pair products from two sorted arrays (Kth Smallest Product of Two Sorted Arrays) — count function must handle negatives carefully.
- Pair distances (Find K-th Smallest Pair Distance) — sort array, use sliding window inside count.
- Median of two sorted arrays (problem 4) — classic divide-and-conquer variant with O(log(min(m,n))).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 2387 | [Median of a Row Wise Sorted Matrix](https://leetcode.com/problems/median-of-a-row-wise-sorted-matrix/) :lock: | Medium | 5/10 | 71.0% | [ ] |
| 786 | [K-th Smallest Prime Fraction](https://leetcode.com/problems/k-th-smallest-prime-fraction/) | Medium | 6/10 | 69.0% | [ ] |
| 378 | [Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/) | Medium | 6/10 | 64.6% | [ ] |
| 668 | [Kth Smallest Number in Multiplication Table](https://leetcode.com/problems/kth-smallest-number-in-multiplication-table/) | Hard | 7/10 | 54.1% | [ ] |
| 2040 | [Kth Smallest Product of Two Sorted Arrays](https://leetcode.com/problems/kth-smallest-product-of-two-sorted-arrays/) | Hard | 8/10 | 48.8% | [ ] |
| 719 | [Find K-th Smallest Pair Distance](https://leetcode.com/problems/find-k-th-smallest-pair-distance/) | Hard | 8/10 | 46.5% | [ ] |
| 4 | [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/) | Hard | 9/10 | 46.5% | [ ] |
| 3134 | [Find the Median of the Uniqueness Array](https://leetcode.com/problems/find-the-median-of-the-uniqueness-array/) | Hard | 9/10 | 30.1% | [ ] |

## graph_connectivity_binary_search

**What it is** — Graph connectivity binary search applies binary search on a threshold parameter (edge weight, time, removal day) and uses graph connectivity checks (BFS/DFS or Union-Find) as the feasibility test. Recognize it when you need the minimum/maximum threshold at which a graph first becomes connected (or disconnected), because connectivity is monotone with respect to the threshold.

**Common steps**
1. Identify the monotone threshold parameter and define `lo` / `hi` bounds.
2. Write a `feasible(mid)` function that builds or filters the graph to include only edges (or cells) satisfying the threshold, then checks connectivity using BFS, DFS, or Union-Find.
3. Binary search on the threshold; move `lo` or `hi` based on whether connectivity is achieved.
4. For time-based problems (Last Day Where You Can Still Cross), binary search on the day and use BFS/Union-Find to check if a path exists.
5. Return the boundary value where connectivity first holds (or breaks).

**Key variations**
- Minimize the maximum edge weight to connect a graph (Minimize the Maximum Edge Weight of Graph).
- Find the last day a crossing is possible (Last Day Where You Can Still Cross).
- Connect exactly k components (Minimum Time for K Connected Components).
- Binary search + minimum spanning tree stability (Maximize Spanning Tree Stability with Upgrades).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 3807 | [Minimum Cost to Repair Edges to Traverse a Graph](https://leetcode.com/problems/minimum-cost-to-repair-edges-to-traverse-a-graph/) :lock: | Medium | 6/10 | 55.6% | [ ] |
| 3419 | [Minimize the Maximum Edge Weight of Graph](https://leetcode.com/problems/minimize-the-maximum-edge-weight-of-graph/) | Medium | 6/10 | 44.5% | [ ] |
| 3608 | [Minimum Time for K Connected Components](https://leetcode.com/problems/minimum-time-for-k-connected-components/) | Medium | 7/10 | 45.4% | [ ] |
| 3613 | [Minimize Maximum Component Cost](https://leetcode.com/problems/minimize-maximum-component-cost/) | Medium | 7/10 | 43.5% | [ ] |
| 1970 | [Last Day Where You Can Still Cross](https://leetcode.com/problems/last-day-where-you-can-still-cross/) | Hard | 8/10 | 68.7% | [ ] |
| 3600 | [Maximize Spanning Tree Stability with Upgrades](https://leetcode.com/problems/maximize-spanning-tree-stability-with-upgrades/) | Hard | 9/10 | 66.3% | [ ] |
| 2258 | [Escape the Spreading Fire](https://leetcode.com/problems/escape-the-spreading-fire/) | Hard | 9/10 | 38.1% | [ ] |

## lis_patience_sorting

**What it is** — Patience sorting is a binary-search-accelerated technique for computing the Longest Increasing Subsequence (LIS) in O(n log n). It maintains a "piles" array where each pile's top is the smallest possible tail value for an increasing subsequence of that length; binary search finds the correct pile for each new element. Recognize it when you need the LIS length (or a transform that reduces to LIS) and O(n^2) DP is too slow.

**Common steps**
1. Initialize an empty `tails` array (pile tops).
2. For each element `x` in the sequence, use `bisect_left(tails, x)` to find the leftmost pile whose top is >= x.
3. If the index equals `len(tails)`, append `x` (extending the longest subsequence found so far); otherwise replace `tails[index]` with `x`.
4. The length of `tails` at the end is the LIS length.
5. For non-strictly increasing, use `bisect_right` instead of `bisect_left`.
6. To reconstruct the actual LIS, store predecessor pointers during step 2-3.

**Key variations**
- Standard LIS (increasing) vs. non-decreasing (change `bisect_left` to `bisect_right`).
- 2-D LIS (Russian Doll Envelopes): sort by first dimension ascending, second descending, then run 1-D LIS on the second dimension.
- Minimum number of subsequences to partition an array (patience sorting pile count equals this by Dilworth's theorem).
- LIS on a transformed problem (Minimum Operations to Make a Subsequence — convert to LCS then LIS via coordinate compression).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1964 | [Find the Longest Valid Obstacle Course at Each Position](https://leetcode.com/problems/find-the-longest-valid-obstacle-course-at-each-position/) | Hard | 7/10 | 62.5% | [ ] |
| 1713 | [Minimum Operations to Make a Subsequence](https://leetcode.com/problems/minimum-operations-to-make-a-subsequence/) | Hard | 8/10 | 49.7% | [ ] |
| 3231 | [Minimum Number of Increasing Subsequence to Be Removed](https://leetcode.com/problems/minimum-number-of-increasing-subsequence-to-be-removed/) :lock: | Hard | 8/10 | 47.0% | [ ] |
| 2111 | [Minimum Operations to Make the Array K-Increasing](https://leetcode.com/problems/minimum-operations-to-make-the-array-k-increasing/) | Hard | 8/10 | 40.5% | [ ] |
| 354 | [Russian Doll Envelopes](https://leetcode.com/problems/russian-doll-envelopes/) | Hard | 8/10 | 37.9% | [ ] |
| 3288 | [Length of the Longest Increasing Path](https://leetcode.com/problems/length-of-the-longest-increasing-path/) | Hard | 9/10 | 19.5% | [ ] |
