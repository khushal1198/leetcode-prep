# SegmentTree

25 problems across 11 patterns.

## segment_tree_order_statistic

**What it is** — An order-statistic segment tree tracks, for each position in a value range, how many elements have been inserted so far, enabling O(log n) queries for the k-th smallest element or rank of a value. Recognize it when a problem requires dynamically finding the k-th available position or the rank of a newly inserted value among previously seen values.

**Common steps**
1. Compress coordinates if values are large; map values to indices 1..n.
2. Build a segment tree over the value range where each node stores a count.
3. To insert a value, point-update its position by +1.
4. To find the k-th smallest, walk the tree: if the left child's count >= k, go left; otherwise subtract left count from k and go right.
5. Return the value corresponding to the leaf you land on.

**Key variations**
- Finding the first available slot >= a given index (walk right-to-left with a minimum/count check)
- Persistent segment tree variant for offline k-th order queries across subarrays

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 3477 | [Fruits Into Baskets II](https://leetcode.com/problems/fruits-into-baskets-ii/) | Easy | 3/10 | 70.2% | [ ] |
| 3479 | [Fruits Into Baskets III](https://leetcode.com/problems/fruits-into-baskets-iii/) | Medium | 5/10 | 39.2% | [ ] |

## point_update_range_query

**What it is** — This is the most fundamental segment tree pattern: update a single element and query an aggregate (sum, min, max, GCD, etc.) over any contiguous range, both in O(log n). Recognize it whenever an array is mutable and you need repeated range aggregation after individual element changes.

**Common steps**
1. Build the segment tree bottom-up: each leaf holds the element value, each internal node holds the aggregate of its children.
2. To update index i: walk from root to the leaf at i, update the leaf, then recompute aggregates on the way back up.
3. To query range [l, r]: recursively combine results from the left and right children, only descending into children whose ranges overlap [l, r].
4. Return the combined aggregate.

**Key variations**
- Sum queries (most common; node stores subtree sum)
- Min/max queries (node stores subtree min or max)
- More complex aggregates like popcount sums or GCD

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 307 | [Range Sum Query - Mutable](https://leetcode.com/problems/range-sum-query-mutable/) | Medium | 4/10 | 43.0% | [ ] |
| 3624 | [Number of Integers With Popcount-Depth Equal to K II](https://leetcode.com/problems/number-of-integers-with-popcount-depth-equal-to-k-ii/) | Hard | 7/10 | 59.5% | [ ] |

## 2d_segment_tree_range_query

**What it is** — A 2D segment tree (or a segment tree of segment trees) supports point updates and rectangular range queries on a 2D grid in O(log^2 n) time. Recognize it when the grid is mutable and you need repeated sum or aggregate queries over axis-aligned rectangles.

**Common steps**
1. Build an outer segment tree over rows; each node of the outer tree maintains an inner segment tree over columns.
2. To update cell (r, c): update position r in the outer tree, which triggers an update at position c in that node's inner tree, propagating up both trees.
3. To query rectangle [r1, r2] x [c1, c2]: query the outer tree for the row range, and within each visited outer node query the inner tree for the column range.
4. Combine all results bottom-up.

**Key variations**
- Sparse 2D segment tree (build inner trees lazily to save memory)
- 2D BIT (Fenwick tree) as a simpler alternative when only prefix queries are needed

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 308 | [Range Sum Query 2D - Mutable](https://leetcode.com/problems/range-sum-query-2d-mutable/) :lock: | Medium | 6/10 | 45.5% | [ ] |

## bit_rank_counting

**What it is** — A Binary Indexed Tree (Fenwick tree) used for rank counting maintains a frequency array and answers prefix sum queries in O(log n), making it ideal for counting how many previously seen elements fall below/above a threshold or within a value range. Recognize it when you process elements left to right and need to count elements before index i that satisfy a value-based condition.

**Common steps**
1. Coordinate-compress values to a range [1, n].
2. Initialize a BIT of size n with all zeros.
3. For each element processed left to right: first query the BIT to count relevant prior elements (e.g., prefix sum up to value - 1), then update the BIT at the current element's compressed value by +1.
4. Accumulate query results into the answer.
5. (For triplet counting) do two passes or nest two BIT queries.

**Key variations**
- Count of smaller elements to the right (process right to left)
- Count good triplets (for each middle element, combine a left BIT query with a right BIT query)
- Distinct element squared sums (track last-occurrence positions with BIT updates)

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 2031 | [Count Subarrays With More Ones Than Zeros](https://leetcode.com/problems/count-subarrays-with-more-ones-than-zeros/) :lock: | Medium | 5/10 | 49.2% | [ ] |
| 2519 | [Count the Number of K-Big Indices](https://leetcode.com/problems/count-the-number-of-k-big-indices/) :lock: | Hard | 6/10 | 53.6% | [ ] |
| 2179 | [Count Good Triplets in an Array](https://leetcode.com/problems/count-good-triplets-in-an-array/) | Hard | 7/10 | 65.5% | [ ] |
| 1649 | [Create Sorted Array through Instructions](https://leetcode.com/problems/create-sorted-array-through-instructions/) | Hard | 7/10 | 41.7% | [ ] |
| 2916 | [Subarrays Distinct Element Sum of Squares II](https://leetcode.com/problems/subarrays-distinct-element-sum-of-squares-ii/) | Hard | 9/10 | 23.1% | [ ] |

## coordinate_compression_segment_tree

**What it is** — Coordinate compression maps a large or sparse value/coordinate space down to a compact index range so that a standard segment tree can operate on it without excessive memory. Recognize it when problem values can be up to 10^9 but the total number of distinct values is at most O(n), making a direct segment tree infeasible.

**Common steps**
1. Collect all relevant values (endpoints, query boundaries) into a list and sort + deduplicate.
2. Map each original value to its compressed index (its rank in the sorted list).
3. Build a segment tree of size equal to the number of distinct compressed values.
4. Perform updates and queries using compressed indices instead of raw values.
5. When reporting results, map compressed indices back to original values if needed.

**Key variations**
- Falling squares: track the maximum height in each compressed x-interval
- Range coverage: use interval-based updates with lazy propagation on compressed coordinates

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 699 | [Falling Squares](https://leetcode.com/problems/falling-squares/) | Hard | 8/10 | 47.8% | [ ] |

## sweep_line_range_query

**What it is** — A sweep line combined with a segment tree processes geometric events (interval starts/ends, rectangle edges) in sorted order, using the segment tree to maintain an aggregate over the active set at each step. Recognize it when you need to compute area, maximum overlap count, or a cut line for a set of intervals or rectangles.

**Common steps**
1. Convert each interval or rectangle into two events: a start event and an end event.
2. Sort all events by their sweep coordinate (usually x or y).
3. Coordinate-compress the perpendicular axis (y or x) and build a segment tree over it.
4. Process events in order: a start event adds coverage (+1 or +height), an end event removes it (-1 or -height).
5. After each event, query the segment tree for the current aggregate (max overlap, total covered length, etc.) and use it to accumulate the answer.

**Key variations**
- Maximum simultaneous bookings (segment tree max query)
- Total covered area (segment tree tracks covered length with lazy count)
- Horizontal cut that equalizes area above and below (binary search on y combined with sweep)

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 732 | [My Calendar III](https://leetcode.com/problems/my-calendar-iii/) | Hard | 7/10 | 71.7% | [ ] |
| 850 | [Rectangle Area II](https://leetcode.com/problems/rectangle-area-ii/) | Hard | 8/10 | 56.1% | [ ] |
| 3454 | [Separate Squares II](https://leetcode.com/problems/separate-squares-ii/) | Hard | 9/10 | 59.6% | [ ] |

## segment_tree_lazy_propagation

**What it is** — Lazy propagation extends a segment tree to support range updates (e.g., set all elements in [l, r] to a value, or add a constant to all elements in [l, r]) in O(log n) by deferring the actual update to child nodes until they are explicitly queried. Recognize it when both updates and queries operate over ranges, not just individual points.

**Common steps**
1. Add a `lazy` field to each node to store a pending operation that has not yet been pushed to children.
2. When performing a range update on [l, r]: if the current node's range is fully within [l, r], update the node's aggregate and set its lazy tag; otherwise, first push the existing lazy tag down to children, then recurse on the relevant child(ren) and recompute the current node.
3. When performing a range query on [l, r]: before recurring into children, push the lazy tag down so children have correct values.
4. Define how lazy tags compose (e.g., two "add" operations just sum; an "assign" then "add" collapses to an "assign with offset").

**Key variations**
- Range assign (set all to a value) with lazy propagation
- Range add with lazy propagation
- Combined operations like range reversal (XOR flip) requiring careful lazy composition

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 3526 | [Range XOR Queries with Subarray Reversals](https://leetcode.com/problems/range-xor-queries-with-subarray-reversals/) :lock: | Hard | 8/10 | 62.6% | [ ] |

## bit_greedy_ordering

**What it is** — This pattern uses a BIT (Fenwick tree) to greedily construct or rearrange elements by efficiently tracking and querying the count of remaining available positions, enabling O(log n) selection of the next valid element. Recognize it when a greedy construction requires repeatedly finding the k-th remaining element in a dynamic set.

**Common steps**
1. Initialize a BIT where each position starts with value 1 (available) or 0 (used).
2. For each step of the greedy process, determine which position to select next based on the problem's greedy criterion.
3. Use the BIT's prefix sum query to find the rank of the desired position among remaining elements (binary search on the BIT).
4. Update the BIT to mark the selected position as used (set to 0).
5. Record the selection and continue until done.

**Key variations**
- Digit-by-digit construction of the lexicographically smallest number using adjacent swaps (track used positions with BIT)
- Selection problems where the greedy choice depends on the count of remaining elements before/after a position

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1505 | [Minimum Possible Integer After at Most K Adjacent Swaps On Digits](https://leetcode.com/problems/minimum-possible-integer-after-at-most-k-adjacent-swaps-on-digits/) | Hard | 9/10 | 41.4% | [ ] |

## segment_tree_range_max_sum

**What it is** — This advanced pattern stores multiple aggregate values per segment tree node (e.g., total sum, max prefix sum, max suffix sum, max subarray sum) so that range queries for maximum subarray or similar composite metrics can be answered in O(log n). Recognize it when a problem needs the maximum sum subarray within a dynamic range or requires merging intervals based on a non-trivial combination of left and right sub-results.

**Common steps**
1. Define the node structure: store `total`, `max_prefix`, `max_suffix`, and `max_subarray` (or the relevant metrics for your problem).
2. Write a `merge(left_node, right_node)` function that correctly computes all four fields for the combined interval.
3. Build the tree bottom-up using the merge function.
4. For range queries, collect all relevant nodes and merge them left to right.
5. For point or range updates with lazy propagation, push down lazy tags and recompute merged values up the tree.

**Key variations**
- Maximum subarray sum in a range (classic four-field node)
- Maximum active section length after a flip operation
- Segment tree beats (track max and second-max to handle "clamp" range updates)
- Booking with group constraints (track max available seats in any prefix of rows)

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 3691 | [Maximum Total Subarray Value II](https://leetcode.com/problems/maximum-total-subarray-value-ii/) | Hard | 9/10 | 22.4% | [ ] |
| 3501 | [Maximize Active Section with Trade II](https://leetcode.com/problems/maximize-active-section-with-trade-ii/) | Hard | 9/10 | 21.0% | [ ] |
| 3762 | [Minimum Operations to Equalize Subarrays](https://leetcode.com/problems/minimum-operations-to-equalize-subarrays/) | Hard | 9/10 | 20.0% | [ ] |
| 2286 | [Booking Concert Tickets in Groups](https://leetcode.com/problems/booking-concert-tickets-in-groups/) | Hard | 9/10 | 19.6% | [ ] |

## segment_tree_dp

**What it is** — Segment tree DP uses a segment tree where each node stores a DP transition matrix or state vector, so that range queries compose DP transitions in O(log n) rather than O(n). Recognize it when a DP recurrence depends on a contiguous range of previously computed values and updates arrive online, making naive recomputation too slow.

**Common steps**
1. Define the DP state and identify the transition as a composable operation (associative, like matrix multiplication or max-plus algebra).
2. Represent each leaf's transition and store it in the corresponding segment tree leaf.
3. Each internal node stores the composed transition of its entire range (using the merge/combine operator).
4. For a range DP query, query the segment tree for the composed transition over [l, r] and apply it to the initial state.
5. For updates, modify the leaf and recompute parent nodes up to the root.

**Key variations**
- LIS with value constraint: segment tree over value space, each node stores best LIS length ending in that value range
- Non-adjacent max sum: 2x2 matrix multiplication in segment tree nodes encoding the DP transition
- Palindrome path queries: store interval palindrome DP in tree nodes with path-based composition

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 3841 | [Palindromic Path Queries in a Tree](https://leetcode.com/problems/palindromic-path-queries-in-a-tree/) | Hard | 9/10 | 35.7% | [ ] |
| 2407 | [Longest Increasing Subsequence II](https://leetcode.com/problems/longest-increasing-subsequence-ii/) | Hard | 9/10 | 26.3% | [ ] |
| 3165 | [Maximum Sum of Subsequence With Non-adjacent Elements](https://leetcode.com/problems/maximum-sum-of-subsequence-with-non-adjacent-elements/) | Hard | 10/10 | 15.9% | [ ] |

## offline_query_segment_tree

**What it is** — Offline query segment tree processes all queries after sorting them (by value, index, or some constraint) so that you can sweep through the data and maintain a segment tree that gives efficient answers when each query is processed at the right moment. Recognize it when queries have two coordinates and answering them in a sorted order lets you reduce a 2D problem to a 1D segment tree query.

**Common steps**
1. Read all queries offline and sort them by one dimension (e.g., by value constraint or right endpoint).
2. Sort or process data in the same order.
3. As you advance through the sorted data, update the segment tree to reflect the current state.
4. When you reach a query's trigger condition, query the segment tree for the answer to that query.
5. Store results indexed by original query order and output at the end.

**Key variations**
- Sort queries by value threshold; sweep data sorted by value and query a range max/min segment tree
- Sort queries by right endpoint; sweep array left to right and query prefix max segment tree
- Combine with binary search on the segment tree to find the leftmost valid position

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 2736 | [Maximum Sum Queries](https://leetcode.com/problems/maximum-sum-queries/) | Hard | 9/10 | 30.4% | [ ] |
| 3161 | [Block Placement Queries](https://leetcode.com/problems/block-placement-queries/) | Hard | 10/10 | 18.5% | [ ] |
