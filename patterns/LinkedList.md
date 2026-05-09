# LinkedList

53 problems across 10 patterns.

## node_deletion

**What it is** — Node deletion is the process of removing one or more nodes from a linked list by redirecting the `next` (and sometimes `prev`) pointers of surrounding nodes so the target node is skipped. Recognize this pattern when a problem asks you to remove nodes based on a condition — a value match, a duplicate check, or a positional rule. The key challenge is always handling the node just before the one you want to delete, since you need to update its `next` pointer.

**Common steps**
1. Create a dummy (sentinel) node that points to the head — this eliminates edge cases when the head itself must be deleted.
2. Initialize a `prev` pointer at the dummy node and a `curr` pointer at the head.
3. Traverse the list with `curr`; at each node, check whether it satisfies the deletion condition.
4. If it does, set `prev.next = curr.next` to skip the node (do not advance `prev`).
5. If it does not, advance `prev = curr`.
6. Always advance `curr = curr.next`, then return `dummy.next` as the new head.

**Key variations**
- Remove by value: skip any node whose `val` equals the target (problem 203).
- Remove duplicates (keep one): advance past the duplicates but keep the first occurrence (problem 83).
- Remove duplicates (keep none): use an inner loop to detect duplicate runs and skip the entire run (problem 82).
- Delete without access to previous node: copy the next node's value into the current node and delete the next node (problem 237).
- Skip M, delete N pattern: count M nodes to keep, then count N nodes to delete, then repeat (problem 1474).
- Delete by set membership: store values in a hash set for O(1) lookup during traversal (problem 3217).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1474 | [Delete N Nodes After M Nodes of a Linked List](https://leetcode.com/problems/delete-n-nodes-after-m-nodes-of-a-linked-list/) :lock: | Easy | 2/10 | 74.4% | [ ] |
| 83 | [Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/) | Easy | 2/10 | 56.7% | [ ] |
| 203 | [Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/) | Easy | 2/10 | 54.4% | [ ] |
| 237 | [Delete Node in a Linked List](https://leetcode.com/problems/delete-node-in-a-linked-list/) | Medium | 3/10 | 83.8% | [ ] |
| 3217 | [Delete Nodes From Linked List Present in Array](https://leetcode.com/problems/delete-nodes-from-linked-list-present-in-array/) | Medium | 3/10 | 69.4% | [ ] |
| 82 | [Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/) | Medium | 5/10 | 51.7% | [ ] |

## two_pointer_traversal

**What it is** — Two-pointer traversal uses two pointers that move through the list at different speeds or starting offsets to locate a node relative to another without knowing the total length upfront. Recognize this pattern when a problem asks for a position defined from the end of the list, the intersection of two lists, or a node that is a fixed distance from another node. It trades a second pass (or a length calculation) for a single coordinated traversal.

**Common steps**
1. Initialize two pointers, `fast` and `slow` (or `p1` and `p2`), both starting at the head (or at the heads of two separate lists).
2. Advance one pointer ahead by the required offset — for "Nth from end" problems, move `fast` forward N steps first.
3. Move both pointers together one step at a time until the leading pointer reaches the end condition (e.g., `fast.next == null` or `fast == null`).
4. At this point, `slow` is at the target node (or just before it, depending on the offset).
5. Perform the required operation — read the value, swap values, or unlink the node.
6. Return the result or the (possibly modified) head.

**Key variations**
- Nth node from end: advance `fast` by N, then move both together until `fast` reaches the tail (problem 19).
- Intersection: equalize path lengths by switching each pointer to the other list's head when it reaches null — they meet at the intersection (problem 160).
- Swap kth nodes: use one pointer to find the kth node from the start, another to find the kth from the end, then swap values (problem 1721).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 160 | [Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/) | Easy | 3/10 | 63.7% | [ ] |
| 1721 | [Swapping Nodes in a Linked List](https://leetcode.com/problems/swapping-nodes-in-a-linked-list/) | Medium | 4/10 | 69.4% | [ ] |
| 19 | [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) | Medium | 4/10 | 51.5% | [ ] |

## merge_lists

**What it is** — Merge lists problems combine two or more linked lists into one by repeatedly comparing nodes and stitching them together. Recognize this pattern when the problem gives you multiple lists (often sorted) and asks you to produce a single list that interleaves or splices them according to some rule. The core idea is a "pick the better candidate" loop that advances only the pointer whose node was selected.

**Common steps**
1. Create a dummy node as the anchor for the result list; keep a `tail` pointer at it.
2. While both (all) input lists are non-null, compare the relevant property of the current nodes.
3. Attach the winning node to `tail.next` and advance that list's pointer forward.
4. Advance `tail` to the newly attached node.
5. Once one list is exhausted, attach the remainder of the other list directly to `tail.next`.
6. Return `dummy.next`.

**Key variations**
- Two sorted lists: compare values and always pick the smaller one (problem 21).
- Splice a sublist: find the anchor nodes at positions `a` and `b`, cut out the segment, and insert a second list in its place (problem 1669).
- Polynomial addition: match nodes by exponent (like a sorted-merge key), add coefficients when exponents are equal, and carry over non-matching terms as-is (problem 1634).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 21 | [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/) | Easy | 2/10 | 68.2% | [ ] |
| 1669 | [Merge In Between Linked Lists](https://leetcode.com/problems/merge-in-between-linked-lists/) | Medium | 4/10 | 83.0% | [ ] |
| 1634 | [Add Two Polynomials Represented as Linked Lists](https://leetcode.com/problems/add-two-polynomials-represented-as-linked-lists/) :lock: | Medium | 5/10 | 61.1% | [ ] |

## simulation_traversal

**What it is** — Simulation traversal problems require you to walk through a linked list and perform some action at each node — accumulating a result, inserting new nodes, or mapping the list onto another data structure. Recognize this pattern when there is no clever trick needed: the problem is essentially "do this for every node in order." The difficulty comes from correctly managing pointer updates and handling special structures like doubly linked lists, circular lists, or lists embedded in trees.

**Common steps**
1. Start a pointer at the head of the list.
2. At each node, perform the required operation (collect a value, compute something, insert a node, fill a matrix cell, etc.).
3. Advance the pointer to the next node (using `.next` for singly linked, `.next`/`.prev` for doubly linked).
4. Handle boundary conditions — null checks, end-of-list sentinels (zeros, specific values), or direction changes (spiral).
5. If inserting new nodes mid-traversal, carefully save the next pointer before overwriting it.
6. Return the result (modified list, array, integer, etc.).

**Key variations**
- Convert to array: collect node values in order into a list or array (problems 3263, 3294).
- Binary/numeric decoding: build up an integer by treating each node as a bit or digit (problem 1290).
- Conditional insertion: insert a new node between every pair of adjacent nodes based on a computed value (problem 2807).
- Accumulate between markers: sum values between sentinel nodes (zeros) and replace the segment with a single node (problem 2181).
- Map onto a 2D structure: fill a matrix following a spiral path, pulling one value per cell from the list (problem 2326).
- Flatten nested structure: use a stack or recursion to inline child lists into the main list in order (problem 430).
- Match list against a tree: attempt to match the linked list as a downward path starting from each tree node (problem 1367).
- Circular insertion: handle the wrap-around edge case where the new value is larger than all existing values (problem 708).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 3263 | [Convert Doubly Linked List to Array I](https://leetcode.com/problems/convert-doubly-linked-list-to-array-i/) :lock: | Easy | 1/10 | 94.9% | [ ] |
| 1290 | [Convert Binary Number in a Linked List to Integer](https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer/) | Easy | 1/10 | 82.4% | [ ] |
| 3062 | [Winner of the Linked List Game](https://leetcode.com/problems/winner-of-the-linked-list-game/) :lock: | Easy | 1/10 | 77.6% | [ ] |
| 3294 | [Convert Doubly Linked List to Array II](https://leetcode.com/problems/convert-doubly-linked-list-to-array-ii/) :lock: | Medium | 2/10 | 82.6% | [ ] |
| 1265 | [Print Immutable Linked List in Reverse](https://leetcode.com/problems/print-immutable-linked-list-in-reverse/) :lock: | Medium | 3/10 | 94.1% | [ ] |
| 2807 | [Insert Greatest Common Divisors in Linked List](https://leetcode.com/problems/insert-greatest-common-divisors-in-linked-list/) | Medium | 3/10 | 91.4% | [ ] |
| 2181 | [Merge Nodes in Between Zeros](https://leetcode.com/problems/merge-nodes-in-between-zeros/) | Medium | 3/10 | 89.7% | [ ] |
| 2326 | [Spiral Matrix IV](https://leetcode.com/problems/spiral-matrix-iv/) | Medium | 5/10 | 82.3% | [ ] |
| 2058 | [Find the Minimum and Maximum Number of Nodes Between Critical Points](https://leetcode.com/problems/find-the-minimum-and-maximum-number-of-nodes-between-critical-points/) | Medium | 5/10 | 69.5% | [ ] |
| 430 | [Flatten a Multilevel Doubly Linked List](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/) | Medium | 6/10 | 62.8% | [ ] |
| 1367 | [Linked List in Binary Tree](https://leetcode.com/problems/linked-list-in-binary-tree/) | Medium | 7/10 | 52.0% | [ ] |
| 708 | [Insert into a Sorted Circular Linked List](https://leetcode.com/problems/insert-into-a-sorted-circular-linked-list/) :lock: | Medium | 7/10 | 38.6% | [ ] |

## fast_slow_pointers

**What it is** — The fast/slow pointer technique (Floyd's algorithm) uses two pointers that advance at different speeds — typically fast moves two steps while slow moves one. Recognize this pattern when a problem involves detecting a cycle, finding the midpoint of a list, or locating a node at a position that is exactly half the list's length away. Because fast travels twice as fast, when fast reaches the end, slow is at the middle; and if there is a cycle, fast will eventually lap slow and they will meet inside the loop.

**Common steps**
1. Initialize `slow = head` and `fast = head`.
2. Advance `slow` by one step and `fast` by two steps in a loop.
3. For cycle detection: loop while `fast != null` and `fast.next != null`; if `slow == fast` at any point, a cycle exists.
4. For finding the midpoint: loop while `fast != null` and `fast.next != null`; when the loop ends, `slow` is at the middle.
5. For finding the cycle entry point (Floyd's phase 2): reset one pointer to `head`, keep the other at the meeting point, then advance both one step at a time — they meet at the cycle start.
6. Use the midpoint as needed — split the list, reverse the second half, or delete the middle node.

**Key variations**
- Detect cycle (yes/no): stop as soon as `slow == fast` (problem 141).
- Find cycle entry node: run the two-phase Floyd's algorithm (problem 142).
- Find midpoint: stop when fast can no longer move two steps (problem 876).
- Delete middle node: stop `slow` one node earlier by starting `fast` one step ahead (problem 2095).
- Palindrome check: find the midpoint, reverse the second half in-place, then compare the two halves (problem 234).
- Maximum twin sum: find the midpoint, reverse the second half, then pair corresponding nodes from each half (problem 2130).
- Split circular list: detect the midpoint in a circular list and rewire the `next` pointers to form two separate circles (problem 2674).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 876 | [Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/) | Easy | 1/10 | 81.8% | [ ] |
| 141 | [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) | Easy | 2/10 | 54.3% | [ ] |
| 2674 | [Split a Circular Linked List](https://leetcode.com/problems/split-a-circular-linked-list/) :lock: | Medium | 4/10 | 77.5% | [ ] |
| 2095 | [Delete the Middle Node of a Linked List](https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/) | Medium | 4/10 | 59.6% | [ ] |
| 234 | [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) | Easy | 4/10 | 57.9% | [ ] |
| 2130 | [Maximum Twin Sum of a Linked List](https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/) | Medium | 5/10 | 81.7% | [ ] |
| 142 | [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/) | Medium | 6/10 | 57.8% | [ ] |

## hash_map_auxiliary

**What it is** — Hash map auxiliary problems use a dictionary or set alongside the traversal to track information that cannot be determined from pointer relationships alone — things like which values have been seen, how many times a value appears, or a mapping from old nodes to new nodes. Recognize this pattern when the problem involves unsorted data, non-contiguous duplicates, node copying with non-sequential links (like random pointers), or prefix sums on node values. The hash map trades space for the ability to look up arbitrary historical information in O(1).

**Common steps**
1. Decide what to store in the map: seen values (for deduplication), value-to-node mappings (for deep copy), or prefix sums (for zero-sum removal).
2. On a first pass (or single pass), populate the map as you traverse each node.
3. On a second pass (if needed), use the map to make decisions — skip duplicates, link random/extra pointers, or identify segments to remove.
4. When deleting based on map lookups, use a dummy head and a `prev` pointer to safely unlink nodes.
5. When deep-copying, create all new nodes in the first pass (map old → new), then wire all `.next` and `.random` pointers in the second pass.
6. Return the new head or the required result.

**Key variations**
- Count frequencies: single pass with a counter map, then read off the result (problem 3063).
- Remove unsorted duplicates: two-pass — first count occurrences, second pass skip any node whose count > 1 (problem 1836).
- Group by membership: use a set of "allowed" values to decide whether consecutive nodes belong to the same component (problem 817).
- Deep copy with random pointers: map each original node to its clone, then set `.next` and `.random` via the map (problem 138).
- Remove zero-sum subsequences: use prefix sums as keys; if the same prefix sum appears twice, the nodes between them sum to zero and should be removed (problem 1171).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 3063 | [Linked List Frequency](https://leetcode.com/problems/linked-list-frequency/) :lock: | Easy | 1/10 | 85.4% | [ ] |
| 1836 | [Remove Duplicates From an Unsorted Linked List](https://leetcode.com/problems/remove-duplicates-from-an-unsorted-linked-list/) :lock: | Medium | 4/10 | 75.7% | [ ] |
| 817 | [Linked List Components](https://leetcode.com/problems/linked-list-components/) | Medium | 4/10 | 57.9% | [ ] |
| 138 | [Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/) | Medium | 6/10 | 62.8% | [ ] |
| 1171 | [Remove Zero Sum Consecutive Nodes from Linked List](https://leetcode.com/problems/remove-zero-sum-consecutive-nodes-from-linked-list/) | Medium | 7/10 | 53.2% | [ ] |

## list_restructuring

**What it is** — List restructuring problems rearrange the existing nodes of a linked list into a new order without creating new nodes — only pointer rewiring is allowed. Recognize this pattern when a problem says "reorder," "rotate," "partition," "split," or "swap" nodes. The key discipline is saving all necessary `next` pointers before overwriting any of them, since one wrong reassignment can permanently lose part of the list.

**Common steps**
1. Analyze the target order and identify which groups of nodes need to be separated and then reconnected.
2. Traverse the list to find the boundaries of each group (e.g., the end of the first half, the tail before rotation, the partition point).
3. Detach the groups from each other by setting terminal `next` pointers to null.
4. Rearrange the group heads and tails by rewiring `next` pointers in the correct new order.
5. Reconnect the groups, making sure no group is left dangling (the last group's tail must point to null or the next group's head).
6. Return the new head (which may differ from the original head).

**Key variations**
- Swap adjacent pairs: process two nodes at a time, rewire their `next` pointers, advance by two (problem 24).
- Separate by index parity: maintain two sub-lists (odd-indexed and even-indexed), build them in parallel, then concatenate (problem 328).
- Partition by value: maintain a "less than" sub-list and a "greater or equal" sub-list, then concatenate (problem 86).
- Split into k parts: compute `len / k` and `len % k` to decide each part's size, then cut and re-link (problem 725).
- Rotate by k: make the list circular, find the new tail at position `len - k % len - 1`, break the circle there (problem 61).
- Reorder L0 → Ln → L1 → Ln-1 → ...: find the midpoint, reverse the second half, then interleave the two halves (problem 143).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 24 | [Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/) | Medium | 4/10 | 69.4% | [ ] |
| 328 | [Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/) | Medium | 4/10 | 62.5% | [ ] |
| 86 | [Partition List](https://leetcode.com/problems/partition-list/) | Medium | 4/10 | 61.1% | [ ] |
| 725 | [Split Linked List in Parts](https://leetcode.com/problems/split-linked-list-in-parts/) | Medium | 5/10 | 70.5% | [ ] |
| 2046 | [Sort Linked List Already Sorted Using Absolute Values](https://leetcode.com/problems/sort-linked-list-already-sorted-using-absolute-values/) :lock: | Medium | 5/10 | 67.1% | [ ] |
| 61 | [Rotate List](https://leetcode.com/problems/rotate-list/) | Medium | 5/10 | 42.5% | [ ] |
| 143 | [Reorder List](https://leetcode.com/problems/reorder-list/) | Medium | 6/10 | 65.2% | [ ] |

## arithmetic_on_list

**What it is** — Arithmetic on list problems represent numbers as linked lists (most significant or least significant digit first) and ask you to perform addition, multiplication, or incrementing directly on those lists. Recognize this pattern when each node holds a single digit and the result must also be returned as a linked list. The core challenge is managing carries across nodes, which is straightforward when digits are stored least-significant-first (you can process left to right) but requires a stack or reversal when they are stored most-significant-first.

**Common steps**
1. Determine digit order: if the head is the most significant digit, reverse both lists first (or use a stack) so you can process from the ones place.
2. Traverse both lists simultaneously, extracting the digit from each (use 0 when one list is exhausted).
3. Compute `sum = digit1 + digit2 + carry`; the new node's value is `sum % 10` and the new carry is `sum // 10`.
4. Create a new node with the computed digit and append it to the result list.
5. After both lists are exhausted, if `carry > 0`, append one more node with value `carry`.
6. If you reversed the input lists, reverse the result list before returning; otherwise return it directly.

**Key variations**
- Least-significant-first (classic): traverse directly left to right, no reversal needed (problem 2).
- Most-significant-first: use stacks or reverse the lists first to reach the ones place (problem 445).
- Double a single number: equivalent to adding the number to itself; handle carry from right to left using a stack or reversal (problem 2816).
- Plus one: find the rightmost non-9 digit, increment it, and set all trailing 9s to 0 — a fast/slow pointer approach can locate the boundary (problem 369).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 445 | [Add Two Numbers II](https://leetcode.com/problems/add-two-numbers-ii/) | Medium | 5/10 | 62.6% | [ ] |
| 2816 | [Double a Number Represented as a Linked List](https://leetcode.com/problems/double-a-number-represented-as-a-linked-list/) | Medium | 5/10 | 61.3% | [ ] |
| 369 | [Plus One Linked List](https://leetcode.com/problems/plus-one-linked-list/) :lock: | Medium | 5/10 | 61.2% | [ ] |
| 2 | [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/) | Medium | 5/10 | 48.4% | [ ] |

## reversal

**What it is** — Reversal problems flip the direction of `next` pointers for all or part of a linked list. Recognize this pattern when the problem asks you to reverse the entire list, reverse a sublist between two positions, or reverse fixed-size groups of nodes repeatedly. The in-place iterative approach uses three pointers (`prev`, `curr`, `next`) and is the fundamental building block — mastering it unlocks all harder variants.

**Common steps**
1. Identify the segment to reverse: record the node just before the segment starts (`before`) and the first node of the segment (`start`).
2. Initialize `prev = null` (or `before`) and `curr = start`.
3. Enter the reversal loop: save `next_node = curr.next`, set `curr.next = prev`, advance `prev = curr`, advance `curr = next_node`.
4. Repeat until you have reversed the required number of nodes or `curr` is null.
5. Reconnect the reversed segment: `before.next = prev` (the new head of the segment) and `start.next = curr` (the node after the segment).
6. For group reversals (k-group), repeat steps 1-5 for each successive group, advancing `before` and `start` after each reversal.

**Key variations**
- Reverse entire list: `before` is null, reverse until `curr` is null, return `prev` as the new head (problem 206).
- Reverse sublist [left, right]: walk to position `left - 1` to find `before`, then reverse exactly `right - left + 1` nodes (problem 92).
- Reverse even-length groups: traverse group by group, counting each group's length, and reverse only those with even length (problem 2074).
- Reverse in k-groups: check that at least k nodes remain before reversing each group; leave a leftover tail as-is if it has fewer than k nodes (problem 25).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 206 | [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) | Easy | 1/10 | 80.5% | [x] |
| 92 | [Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/) | Medium | 6/10 | 51.5% | [ ] |
| 2074 | [Reverse Nodes in Even Length Groups](https://leetcode.com/problems/reverse-nodes-in-even-length-groups/) | Medium | 7/10 | 64.0% | [ ] |
| 25 | [Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/) | Hard | 8/10 | 66.0% | [ ] |

## sorting

**What it is** — Sorting problems ask you to rearrange the nodes of a linked list into a specific order (typically ascending) using only pointer manipulation. Recognize this pattern when the problem gives you an unsorted or partially-sorted list and requires a sorted output. Sorting a linked list is harder than sorting an array because there is no random access, but it is easier to splice nodes without shifting — insertion sort works well for nearly-sorted lists, while merge sort achieves optimal O(n log n) time for general cases.

**Common steps**
1. Choose your algorithm: insertion sort for small or nearly-sorted lists; merge sort (divide and conquer) for the general case.
2. For insertion sort: maintain a sorted sub-list starting from a dummy head; for each new node, traverse the sorted sub-list to find its correct position and splice it in.
3. For merge sort: use the fast/slow pointer technique to find the midpoint and split the list into two halves.
4. Recursively sort each half.
5. Merge the two sorted halves using the standard merge-two-sorted-lists routine (compare heads, pick the smaller, advance that pointer).
6. Return the head of the fully sorted list.

**Key variations**
- Insertion sort: O(n²) time but O(1) space and simple to implement; best when input is nearly sorted (problem 147).
- Merge sort (top-down): O(n log n) time and O(log n) stack space from recursion; the standard efficient approach (problem 148).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 147 | [Insertion Sort List](https://leetcode.com/problems/insertion-sort-list/) | Medium | 5/10 | 59.1% | [ ] |
| 148 | [Sort List](https://leetcode.com/problems/sort-list/) | Medium | 7/10 | 64.4% | [ ] |
