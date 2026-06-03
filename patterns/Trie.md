# Trie

43 problems across 10 patterns.

## trie_basic_design

**What it is** — A Trie (prefix tree) is a tree data structure where each node represents a single character, and paths from root to a node represent prefixes of inserted strings. Recognize this pattern when a problem asks you to build a reusable data structure that supports fast insert and prefix/word lookup. The core insight is that words sharing a common prefix share the same path in the tree.

**Common steps**
1. Define a `TrieNode` class with a dictionary (or fixed-size array) of children and a boolean `is_end` flag.
2. Implement `insert(word)`: iterate over each character, create a child node if it does not exist, then advance; mark `is_end = True` on the final node.
3. Implement `search(word)`: traverse the tree character by character; return `True` only if every character exists AND the final node has `is_end = True`.
4. Implement `startsWith(prefix)`: same as search but skip the `is_end` check — return `True` as long as all characters are found.
5. For Trie II, add reference counts (`count_end`, `count_prefix`) at each node and update them on insert/delete.

**Key variations**
- Basic Trie stores only `is_end`; Trie II also stores per-node counts to support `countWordsEqualTo` and `countWordsStartingWith`.
- Children can be stored as a `dict` (flexible, memory-efficient for sparse alphabets) or as an array of size 26 (faster access for lowercase letters).
- Deletion requires decrementing counts or pruning leaf nodes bottom-up.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 208 | [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/) | Medium | 3/10 | 69.5% | [x] |
| 1804 | [Implement Trie II (Prefix Tree)](https://leetcode.com/problems/implement-trie-ii-prefix-tree/) :lock: | Medium | 4/10 | 63.4% | [ ] |

## trie_prefix_search

**What it is** — This pattern uses a Trie to efficiently answer queries about prefixes: finding words that share a prefix, replacing words with their shortest prefix, or scoring/ranking words by prefix frequency. Recognize it when you need to repeatedly look up or aggregate information for all strings that start with a given prefix, especially across a large dictionary.

**Common steps**
1. Build the Trie by inserting all dictionary/word-list strings, storing any auxiliary data needed (frequency, index, mapped value) at end nodes.
2. For a query prefix, traverse the Trie following each character; if any character is missing, no matches exist.
3. Once at the prefix endpoint node, collect results — either return the stored value, DFS/BFS to gather all descendant words, or propagate counts back up.
4. For "replace with shortest prefix" problems, stop traversal as soon as you hit an `is_end` node and return that prefix.
5. For ranked/autocomplete results, maintain a sorted structure (e.g., a heap of size k) at each node or collect all matches and sort after the DFS.
6. Return or aggregate results across all queries.

**Key variations**
- Storing a value at each node enables map-sum style aggregation (e.g., prefix score = sum of values of all words with that prefix).
- Autocomplete requires collecting all terminal descendants — store top-k candidates at each node to avoid full DFS on every query.
- Some problems require the longest common prefix across two arrays of numbers, treating each digit as a character.
- Word abbreviation variants need both prefix uniqueness checking and suffix appending logic.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 3491 | [Phone Number Prefix](https://leetcode.com/problems/phone-number-prefix/) :lock: | Easy | 2/10 | 70.2% | [ ] |
| 1065 | [Index Pairs of a String](https://leetcode.com/problems/index-pairs-of-a-string/) :lock: | Easy | 2/10 | 68.6% | [ ] |
| 648 | [Replace Words](https://leetcode.com/problems/replace-words/) | Medium | 3/10 | 68.7% | [ ] |
| 1858 | [Longest Word With All Prefixes](https://leetcode.com/problems/longest-word-with-all-prefixes/) :lock: | Medium | 4/10 | 72.1% | [ ] |
| 1268 | [Search Suggestions System](https://leetcode.com/problems/search-suggestions-system/) | Medium | 4/10 | 65.2% | [ ] |
| 677 | [Map Sum Pairs](https://leetcode.com/problems/map-sum-pairs/) | Medium | 4/10 | 57.2% | [ ] |
| 720 | [Longest Word in Dictionary](https://leetcode.com/problems/longest-word-in-dictionary/) | Medium | 4/10 | 54.8% | [ ] |
| 3758 | [Convert Number Words to Digits](https://leetcode.com/problems/convert-number-words-to-digits/) :lock: | Medium | 5/10 | 70.1% | [ ] |
| 3043 | [Find the Length of the Longest Common Prefix](https://leetcode.com/problems/find-the-length-of-the-longest-common-prefix/) | Medium | 5/10 | 57.1% | [ ] |
| 527 | [Word Abbreviation](https://leetcode.com/problems/word-abbreviation/) :lock: | Hard | 7/10 | 62.7% | [ ] |
| 642 | [Design Search Autocomplete System](https://leetcode.com/problems/design-search-autocomplete-system/) :lock: | Hard | 7/10 | 49.9% | [ ] |

## trie_wildcard_and_fuzzy_search

**What it is** — This pattern extends standard Trie search to handle wildcard characters (typically `.`) that can match any single character. Recognize it when a search/match operation allows one or more positions to be "any character," requiring you to branch into all possible children at those positions during traversal.

**Common steps**
1. Build the Trie normally by inserting all known words character by character.
2. Implement a recursive (or DFS) search function that takes the current Trie node and the remaining query string.
3. At each step, if the current query character is a literal, advance to the matching child (or return False if missing).
4. If the current character is `.` (wildcard), recursively call search on ALL non-null children with the rest of the query.
5. Return True if any recursive branch reaches the end of the query at a node with `is_end = True`.
6. For "magic dictionary" style problems (exactly one substitution), track a mismatch counter and allow at most one non-matching character before failing.

**Key variations**
- Pure wildcard (`.` matches any char) requires branching over all children — worst case O(26^k) for k wildcards.
- Fuzzy match with exactly one allowed difference adds a `mismatch_count` parameter to the recursion.
- Wildcards can appear at any position, so the recursion must handle them at the start, middle, or end of a pattern.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 676 | [Implement Magic Dictionary](https://leetcode.com/problems/implement-magic-dictionary/) | Medium | 5/10 | 57.8% | [ ] |
| 211 | [Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/) | Medium | 5/10 | 48.4% | [ ] |

## trie_filesystem_design

**What it is** — File system paths are naturally hierarchical sequences of path components separated by `/`, making them a perfect fit for a Trie where each node represents one directory or file name. Recognize this pattern when a problem models paths (strings with `/` delimiters) and requires operations like creation, lookup, or de-duplication of directory structures.

**Common steps**
1. Split each path on `/` to get a list of path components (skip the empty string from the leading `/`).
2. Build a Trie where each node stores a map from component name to child node, plus any associated value (file content, timestamp, etc.).
3. For `create(path, value)`: traverse existing nodes for all but the last component; create the final node and store the value; return False if any intermediate node does not exist.
4. For `get(path)`: traverse all components and return the stored value at the leaf, or -1/-1 if any node is missing.
5. For sub-folder removal: sort paths lexicographically; skip any path that starts with the last accepted path followed by `/`.
6. For in-memory file systems, also handle `ls` (list children) and `cat` (read file content) by distinguishing file nodes from directory nodes.

**Key variations**
- Some problems allow creating intermediate directories automatically (mkdir -p style); others require all parents to exist.
- Sub-folder removal can be solved with just sorting + prefix checking, without building a full Trie.
- Full in-memory file systems need to distinguish files (leaf nodes with content) from directories (internal nodes with children).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1166 | [Design File System](https://leetcode.com/problems/design-file-system/) :lock: | Medium | 4/10 | 65.1% | [ ] |
| 1233 | [Remove Sub-Folders from the Filesystem](https://leetcode.com/problems/remove-sub-folders-from-the-filesystem/) | Medium | 5/10 | 78.6% | [ ] |
| 588 | [Design In-Memory File System](https://leetcode.com/problems/design-in-memory-file-system/) :lock: | Hard | 7/10 | 48.4% | [ ] |

## trie_lexicographic_traversal

**What it is** — Numbers or strings can be traversed in lexicographic (dictionary) order by treating each digit/character as a level of a conceptual Trie and performing a pre-order DFS. Recognize this pattern when you need to enumerate integers or strings in lexicographic order efficiently — especially when the range is large and you cannot afford to sort all elements.

**Common steps**
1. Think of integers 1–n as nodes in a 10-ary Trie where each level appends a digit 0–9.
2. Start DFS from each root digit 1–9; at each node with value `curr`, visit `curr` first (pre-order), then recurse into children `curr*10`, `curr*10+1`, ..., `curr*10+9` as long as the child does not exceed n.
3. To find the k-th lexicographic number without full enumeration, count how many numbers exist in the subtree rooted at `curr` (those in [curr, curr+1) * 10^level range within [1, n]).
4. If the count of the current subtree >= k, step into it (go to `curr * 10`); otherwise subtract that count from k and move to the next sibling (`curr + 1`).
5. Repeat until k == 1, then return `curr`.

**Key variations**
- Full enumeration (LC 386) uses iterative pre-order DFS and is O(n).
- K-th element (LC 440) skips entire subtrees by counting their size, achieving O(log^2 n).
- Subtree size counting must handle the upper boundary n carefully to avoid over-counting.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 386 | [Lexicographical Numbers](https://leetcode.com/problems/lexicographical-numbers/) | Medium | 5/10 | 76.2% | [ ] |
| 440 | [K-th Smallest in Lexicographical Order](https://leetcode.com/problems/k-th-smallest-in-lexicographical-order/) | Hard | 8/10 | 46.3% | [ ] |

## trie_deduplication_and_counting

**What it is** — A Trie naturally deduplicates strings and substrings because identical sequences follow the exact same path, making it powerful for counting distinct substrings, prefix scores, or unique structural patterns. Recognize this pattern when a problem asks you to count or rank distinct substrings/subsequences, or detect duplicate tree structures, often over large inputs where hashing alone is too slow or collision-prone.

**Common steps**
1. To count distinct substrings of a string, insert every suffix into the Trie; each new edge created during all insertions represents one unique substring, so the answer is the total number of edges added.
2. For prefix score problems, increment a `pass_count` at every node visited during insertion; the score for a word is the sum of `pass_count` values along its path.
3. For deduplication of subtree structures (e.g., duplicate folders), serialize each subtree into a canonical string, insert into a Trie or hash map, and mark nodes whose serialization appears more than once.
4. For counting distinct subarrays, encode each element as a Trie character and insert every suffix of the array; count new nodes created.
5. To find the shortest unique substring for each word, insert all words, then for each word query the depth at which it becomes unique (only one word passes through that node).

**Key variations**
- Suffix-based insertion counts all distinct substrings in O(n^2) time and space — feasible for n up to ~1000.
- Pass-count at nodes enables batch prefix-score queries in a single O(total characters) pass.
- Structural deduplication serializes subtrees (DFS post-order) and compares serializations, not raw strings.
- Problems may ask for partitions, subarrays, or deletions, each requiring a different aggregation on top of the core Trie structure.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 3597 | [Partition String ](https://leetcode.com/problems/partition-string/) | Medium | 5/10 | 59.1% | [ ] |
| 1698 | [Number of Distinct Substrings in a String](https://leetcode.com/problems/number-of-distinct-substrings-in-a-string/) :lock: | Medium | 6/10 | 64.7% | [ ] |
| 2416 | [Sum of Prefix Scores of Strings](https://leetcode.com/problems/sum-of-prefix-scores-of-strings/) | Hard | 6/10 | 60.8% | [ ] |
| 2261 | [K Divisible Elements Subarrays](https://leetcode.com/problems/k-divisible-elements-subarrays/) | Medium | 6/10 | 54.9% | [ ] |
| 3076 | [Shortest Uncommon Substring in an Array](https://leetcode.com/problems/shortest-uncommon-substring-in-an-array/) | Medium | 6/10 | 50.5% | [ ] |
| 3485 | [Longest Common Prefix of K Strings After Removal](https://leetcode.com/problems/longest-common-prefix-of-k-strings-after-removal/) | Hard | 8/10 | 23.9% | [ ] |
| 1948 | [Delete Duplicate Folders in System](https://leetcode.com/problems/delete-duplicate-folders-in-system/) | Hard | 9/10 | 77.5% | [ ] |

## trie_suffix_and_reverse

**What it is** — Some problems require matching or searching by suffix rather than prefix. The standard technique is to reverse all strings before inserting them into a Trie so that suffix queries become prefix queries. Recognize this pattern when a problem involves matching word endings, streaming character queries (check if any word ends at this point), or combined prefix-and-suffix lookups.

**Common steps**
1. Reverse all words and insert them into the Trie so that suffix matches become prefix traversals.
2. For streaming suffix queries (e.g., "does any word end here?"), maintain a pointer into the reversed Trie and advance it with each new character; check `is_end` after each step.
3. For combined prefix + suffix search, encode each word as `suffix + '#' + word` and insert all rotations, or use a double-ended Trie structure that supports both directions.
4. For suffix encoding (short encoding of words), detect which words are suffixes of other words — insert all words, then check if any word's reverse path is already fully contained in the Trie.
5. For suffix query problems, iterate queries against the reversed Trie and return the stored word/index at the deepest matching `is_end` node.

**Key variations**
- Pure suffix Trie: reverse all strings, use standard prefix Trie logic.
- Stream-of-characters: the Trie is queried character-by-character in real time; maintain a list of active search paths.
- Prefix-and-suffix combined: LC 745 requires lookup by both simultaneously — encode as `suffix#prefix` pairs in the Trie.
- Suffix pair counting (LC 3045) requires checking whether one string is both a prefix and suffix of another, often using Z-function or KMP combined with a Trie.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 820 | [Short Encoding of Words](https://leetcode.com/problems/short-encoding-of-words/) | Medium | 5/10 | 60.8% | [ ] |
| 1032 | [Stream of Characters](https://leetcode.com/problems/stream-of-characters/) | Hard | 7/10 | 52.2% | [ ] |
| 745 | [Prefix and Suffix Search](https://leetcode.com/problems/prefix-and-suffix-search/) | Hard | 8/10 | 40.9% | [ ] |
| 3093 | [Longest Common Suffix Queries](https://leetcode.com/problems/longest-common-suffix-queries/) | Hard | 8/10 | 35.8% | [ ] |
| 3045 | [Count Prefix and Suffix Pairs II](https://leetcode.com/problems/count-prefix-and-suffix-pairs-ii/) | Hard | 9/10 | 28.3% | [ ] |

## trie_with_backtracking

**What it is** — This pattern combines Trie-based word lookup with DFS backtracking on a 2D grid, allowing you to search for multiple words simultaneously while exploring paths on the board. Recognize it when you must find all words from a dictionary that can be formed by adjacent cells on a grid — the Trie prunes the search early whenever the current path cannot lead to any word.

**Common steps**
1. Insert all dictionary words into a Trie.
2. For each cell on the board, start a DFS using the current cell's character to enter the Trie.
3. At each DFS step, check if the current character exists as a child in the Trie node; if not, prune immediately (return).
4. If the current node has `is_end = True`, record the found word and clear `is_end` to avoid duplicates.
5. Mark the current cell as visited (e.g., set to `#`), recurse into all 4 neighbors, then restore the cell (backtrack).
6. Optionally prune Trie nodes that have no remaining children after a word is found, to speed up future searches.

**Key variations**
- Without Trie pruning, the DFS revisits dead branches repeatedly — pruning found words from the Trie is the key optimization.
- The board can have the same word reachable via multiple paths; using `is_end` as a "found" flag and resetting it prevents duplicates.
- For very large word lists, Trie search beats checking each word independently with DFS (O(words * 4^L) vs shared prefix traversal).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 212 | [Word Search II](https://leetcode.com/problems/word-search-ii/) | Hard | 8/10 | 38.4% | [ ] |

## trie_dp_and_graph

**What it is** — This pattern combines a Trie with dynamic programming or shortest-path algorithms to answer questions like "what is the minimum number of dictionary words needed to cover a target string?" or "what is the cheapest way to transform one string into another using valid substrings?" Recognize it when a problem asks for an optimal decomposition or transformation of a string where valid segments are defined by a dictionary, making Trie + DP a natural pairing.

**Common steps**
1. Build a Trie from the dictionary of valid strings/patterns.
2. Define a DP array where `dp[i]` represents the optimal answer (min cost, min count, etc.) for the first `i` characters of the target.
3. For each position `i`, traverse the Trie starting at `i`, advancing one character at a time; at every `is_end` node reached at position `j`, update `dp[j]` using `dp[i]` plus the cost of this segment.
4. For graph/shortest-path variants, build a graph where nodes are string positions and edges correspond to valid dictionary substrings (found via Trie traversal), then run Dijkstra or BFS for minimum cost.
5. Initialize `dp[0] = 0` (base case: empty prefix costs nothing) and return `dp[len(target)]`.

**Key variations**
- Minimum segments (LC 3291): each valid prefix costs 1; standard BFS/DP.
- Minimum cost with string replacement (LC 2977): edges have associated costs and the target must be transformed; requires Dijkstra on position nodes.
- Trie traversal replaces the inner loop of naive DP (O(n^2)) with a more pruned O(n * max_word_length) traversal.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 3291 | [Minimum Number of Valid Strings to Form Target I](https://leetcode.com/problems/minimum-number-of-valid-strings-to-form-target-i/) | Medium | 7/10 | 21.9% | [ ] |
| 2977 | [Minimum Cost to Convert String II](https://leetcode.com/problems/minimum-cost-to-convert-string-ii/) | Hard | 9/10 | 59.6% | [ ] |

## trie_xor_bitwise

**What it is** — A binary Trie stores numbers bit-by-bit from the most significant bit to the least significant bit, enabling greedy XOR maximization or range queries in O(32) per operation. Recognize this pattern when a problem asks for maximum XOR between elements, XOR within a range, or XOR-based queries on a set of integers — the Trie lets you greedily pick the best opposite bit at each level.

**Common steps**
1. Build a binary Trie by inserting each number bit-by-bit from bit 31 (or the highest relevant bit) down to bit 0; each node has two children: `0` and `1`.
2. To find the maximum XOR of a query number `x` against all numbers in the Trie, traverse from the MSB: at each level, try to go to the child opposite to `x`'s current bit (to maximize XOR); if that child does not exist, go to the same-bit child.
3. Accumulate the XOR value as you descend, adding the achieved bit at each level.
4. For problems with constraints (e.g., "element must be <= m"), process queries offline sorted by constraint, inserting numbers into the Trie only when they satisfy the constraint.
5. For counting XOR pairs in a range, maintain counts at each Trie node and use the range bounds to determine how many numbers in the Trie produce an XOR within [low, high].
6. For tree/graph variants, perform an Euler tour or DFS and maintain a running Trie of path XOR values, querying at each node.

**Key variations**
- Maximum XOR pair (LC 421): insert all numbers, query each number against the Trie — O(32n).
- Offline with constraint (LC 1707): sort queries and numbers by value, insert numbers incrementally, query Trie for max XOR within allowed set.
- XOR range counting (LC 1803): for each number, count how many existing numbers produce XOR in [low, high] using two traversals (count XOR < high+1 minus count XOR < low).
- Tree XOR (LC 2479, 1938): DFS on the tree while maintaining a Trie of root-to-node XOR prefix values; query on entry/exit.
- Subarray XOR (LC 3845): use prefix XOR + binary Trie to find subarrays whose XOR meets a condition, similar to prefix-sum techniques.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 421 | [Maximum XOR of Two Numbers in an Array](https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/) | Medium | 6/10 | 53.4% | [ ] |
| 1707 | [Maximum XOR With an Element From Array](https://leetcode.com/problems/maximum-xor-with-an-element-from-array/) | Hard | 8/10 | 57.9% | [ ] |
| 1803 | [Count Pairs With XOR in a Range](https://leetcode.com/problems/count-pairs-with-xor-in-a-range/) | Hard | 8/10 | 46.0% | [ ] |
| 3632 | [Subarrays with XOR at Least K](https://leetcode.com/problems/subarrays-with-xor-at-least-k/) :lock: | Hard | 8/10 | 42.7% | [ ] |
| 2479 | [Maximum XOR of Two Non-Overlapping Subtrees](https://leetcode.com/problems/maximum-xor-of-two-non-overlapping-subtrees/) :lock: | Hard | 9/10 | 51.9% | [ ] |
| 1938 | [Maximum Genetic Difference Query](https://leetcode.com/problems/maximum-genetic-difference-query/) | Hard | 9/10 | 46.9% | [ ] |
| 2935 | [Maximum Strong Pair XOR II](https://leetcode.com/problems/maximum-strong-pair-xor-ii/) | Hard | 9/10 | 32.6% | [ ] |
| 3845 | [Maximum Subarray XOR with Bounded Range](https://leetcode.com/problems/maximum-subarray-xor-with-bounded-range/) | Hard | 9/10 | 32.2% | [ ] |
