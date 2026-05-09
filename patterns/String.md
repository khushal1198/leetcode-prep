# String

124 problems across 13 patterns.

## string_manipulation

**What it is** — String manipulation covers direct in-place or character-by-character transformations: reversing, replacing, reformatting, and splitting strings. Recognize this pattern when the problem asks you to produce a modified version of the input string using simple rules applied to characters, words, or substrings.

**Common steps**
1. Identify the unit of transformation (individual characters, words, segments, or substrings).
2. Decide whether to build a new result string/list or modify in place (use a list/array for mutability in Python).
3. Iterate through the string, applying the transformation rule at each position or word boundary.
4. Handle edge cases: leading/trailing spaces, empty strings, single characters, and case sensitivity.
5. Join the result back into a string and return.

**Key variations**
- Reversals: entire string, prefix up to a character, or every word individually.
- Reformatting: inserting/removing separators (dashes, dots, spaces) at fixed intervals.
- Character-level swaps: toggling case, shifting by an offset (`chr(ord(c) + shift)`).
- Multi-pass transforms: apply one rule (e.g., strip spaces) then a second (e.g., redistribute spaces).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1119 | [Remove Vowels from a String](https://leetcode.com/problems/remove-vowels-from-a-string/) :lock: | Easy | 1/10 | 91.3% | [ ] |
| 1108 | [Defanging an IP Address](https://leetcode.com/problems/defanging-an-ip-address/) | Easy | 1/10 | 90.0% | [ ] |
| 3794 | [Reverse String Prefix](https://leetcode.com/problems/reverse-string-prefix/) | Easy | 1/10 | 89.5% | [ ] |
| 1816 | [Truncate Sentence](https://leetcode.com/problems/truncate-sentence/) | Easy | 1/10 | 86.8% | [ ] |
| 2000 | [Reverse Prefix of Word](https://leetcode.com/problems/reverse-prefix-of-word/) | Easy | 1/10 | 86.5% | [ ] |
| 1662 | [Check If Two String Arrays are Equivalent](https://leetcode.com/problems/check-if-two-string-arrays-are-equivalent/) | Easy | 1/10 | 86.1% | [ ] |
| 709 | [To Lower Case](https://leetcode.com/problems/to-lower-case/) | Easy | 1/10 | 84.8% | [ ] |
| 557 | [Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/) | Easy | 1/10 | 84.0% | [ ] |
| 1844 | [Replace All Digits with Characters](https://leetcode.com/problems/replace-all-digits-with-characters/) | Easy | 1/10 | 82.7% | [ ] |
| 521 | [Longest Uncommon Subsequence I](https://leetcode.com/problems/longest-uncommon-subsequence-i/) | Easy | 1/10 | 62.2% | [ ] |
| 58 | [Length of Last Word](https://leetcode.com/problems/length-of-last-word/) | Easy | 1/10 | 58.8% | [ ] |
| 1556 | [Thousand Separator](https://leetcode.com/problems/thousand-separator/) | Easy | 1/10 | 53.7% | [ ] |
| 1694 | [Reformat Phone Number](https://leetcode.com/problems/reformat-phone-number/) | Easy | 2/10 | 67.7% | [ ] |
| 1427 | [Perform String Shifts](https://leetcode.com/problems/perform-string-shifts/) :lock: | Easy | 2/10 | 56.0% | [ ] |
| 541 | [Reverse String II](https://leetcode.com/problems/reverse-string-ii/) | Easy | 2/10 | 53.7% | [ ] |
| 1790 | [Check if One String Swap Can Make Strings Equal](https://leetcode.com/problems/check-if-one-string-swap-can-make-strings-equal/) | Easy | 2/10 | 49.5% | [ ] |
| 482 | [License Key Formatting](https://leetcode.com/problems/license-key-formatting/) | Easy | 2/10 | 46.0% | [ ] |
| 1592 | [Rearrange Spaces Between Words](https://leetcode.com/problems/rearrange-spaces-between-words/) | Easy | 2/10 | 44.2% | [ ] |
| 151 | [Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/) | Medium | 3/10 | 56.3% | [ ] |
| 1417 | [Reformat The String](https://leetcode.com/problems/reformat-the-string/) | Easy | 3/10 | 52.2% | [ ] |
| 859 | [Buddy Strings](https://leetcode.com/problems/buddy-strings/) | Easy | 3/10 | 34.0% | [ ] |
| 3722 | [Lexicographically Smallest String After Reverse](https://leetcode.com/problems/lexicographically-smallest-string-after-reverse/) | Medium | 4/10 | 54.8% | [ ] |
| 1181 | [Before and After Puzzle](https://leetcode.com/problems/before-and-after-puzzle/) :lock: | Medium | 4/10 | 51.9% | [ ] |
| 833 | [Find And Replace in String](https://leetcode.com/problems/find-and-replace-in-string/) | Medium | 4/10 | 50.8% | [ ] |

## prefix_suffix

**What it is** — The prefix/suffix pattern involves checking, extracting, or comparing the beginning or end portions of strings. Recognize it when the problem asks whether a string starts or ends with another string, or when you need to find the longest common leading/trailing segment across a set of strings.

**Common steps**
1. Clarify whether you need a prefix (start), suffix (end), or both.
2. For single-pair checks, use direct slicing (`s[:len(p)] == p`) or language built-ins (`startswith`/`endswith`).
3. For finding the longest common prefix across multiple strings, use the first string as a baseline and progressively shrink it by comparing character-by-character with each remaining string.
4. For splitting problems (e.g., maximize a score at a split point), iterate over all valid split indices and track the best result.
5. Return the found prefix/suffix or the computed result.

**Key variations**
- Single prefix/suffix check vs. finding the longest common prefix across an array.
- Counting all pairs where one string is a prefix/suffix of another.
- Score-based splitting at a prefix boundary.
- Palindrome detection that leverages prefix/suffix structure (unique length-3 palindromic subsequences).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1455 | [Check If a Word Occurs As a Prefix of Any Word in a Sentence](https://leetcode.com/problems/check-if-a-word-occurs-as-a-prefix-of-any-word-in-a-sentence/) | Easy | 1/10 | 68.8% | [ ] |
| 1961 | [Check If String Is a Prefix of Array](https://leetcode.com/problems/check-if-string-is-a-prefix-of-array/) | Easy | 1/10 | 52.8% | [ ] |
| 3042 | [Count Prefix and Suffix Pairs I](https://leetcode.com/problems/count-prefix-and-suffix-pairs-i/) | Easy | 2/10 | 77.8% | [ ] |
| 1422 | [Maximum Score After Splitting a String](https://leetcode.com/problems/maximum-score-after-splitting-a-string/) | Easy | 2/10 | 65.1% | [ ] |
| 14 | [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/) | Easy | 2/10 | 47.5% | [ ] |
| 1930 | [Unique Length-3 Palindromic Subsequences](https://leetcode.com/problems/unique-length-3-palindromic-subsequences/) | Medium | 5/10 | 73.8% | [ ] |

## string_simulation

**What it is** — String simulation means stepping through a process step-by-step and tracking state as you go, rather than deriving a formula. Recognize this pattern when the problem describes a sequence of rules or operations that must be applied in order, and the output depends on the intermediate state of the string at each step.

**Common steps**
1. Model the state you need to track (current string, counters for each character/token, current position).
2. Iterate through the string (or through each step/round) in the specified order.
3. Apply the rule for each character or segment (e.g., group consecutive identical characters, perform run-length encoding, simulate a physical layout like zigzag rows).
4. Accumulate the result into a list or output structure.
5. Handle termination conditions and edge cases (empty input, single element, overflow of state counters).
6. Convert the accumulated state back to the required output format.

**Key variations**
- Run-length / group encoding: group consecutive equal characters and output count + character.
- Physical layout simulation: map character positions onto a grid or row structure (zigzag, spiral).
- Multi-round simulation: apply the same transformation repeatedly for k rounds.
- State machine simulation: track multiple concurrent counters (e.g., frogs croaking through c-r-o-a-k states).
- Encoded string decoding: reverse-engineer the original string from a compressed or transformed version.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 293 | [Flip Game](https://leetcode.com/problems/flip-game/) :lock: | Easy | 1/10 | 65.0% | [ ] |
| 1869 | [Longer Contiguous Segments of Ones than Zeros](https://leetcode.com/problems/longer-contiguous-segments-of-ones-than-zeros/) | Easy | 1/10 | 62.5% | [ ] |
| 1446 | [Consecutive Characters](https://leetcode.com/problems/consecutive-characters/) | Easy | 1/10 | 60.4% | [ ] |
| 830 | [Positions of Large Groups](https://leetcode.com/problems/positions-of-large-groups/) | Easy | 1/10 | 53.9% | [ ] |
| 944 | [Delete Columns to Make Sorted](https://leetcode.com/problems/delete-columns-to-make-sorted/) | Easy | 2/10 | 78.1% | [ ] |
| 1945 | [Sum of Digits of String After Convert](https://leetcode.com/problems/sum-of-digits-of-string-after-convert/) | Easy | 2/10 | 74.8% | [ ] |
| 824 | [Goat Latin](https://leetcode.com/problems/goat-latin/) | Easy | 2/10 | 70.0% | [ ] |
| 1078 | [Occurrences After Bigram](https://leetcode.com/problems/occurrences-after-bigram/) | Easy | 2/10 | 63.9% | [ ] |
| 67 | [Add Binary](https://leetcode.com/problems/add-binary/) | Easy | 2/10 | 58.0% | [ ] |
| 1796 | [Second Largest Digit in a String](https://leetcode.com/problems/second-largest-digit-in-a-string/) | Easy | 2/10 | 54.3% | [ ] |
| 1784 | [Check if Binary String Has at Most One Segment of Ones](https://leetcode.com/problems/check-if-binary-string-has-at-most-one-segment-of-ones/) | Easy | 2/10 | 49.1% | [ ] |
| 3775 | [Reverse Words With Same Vowel Count](https://leetcode.com/problems/reverse-words-with-same-vowel-count/) | Medium | 3/10 | 66.8% | [ ] |
| 38 | [Count and Say](https://leetcode.com/problems/count-and-say/) | Medium | 3/10 | 62.8% | [ ] |
| 1933 | [Check if String Is Decomposable Into Value-Equal Substrings](https://leetcode.com/problems/check-if-string-is-decomposable-into-value-equal-substrings/) :lock: | Easy | 3/10 | 51.0% | [ ] |
| 6 | [Zigzag Conversion](https://leetcode.com/problems/zigzag-conversion/) | Medium | 4/10 | 54.1% | [ ] |
| 1419 | [Minimum Number of Frogs Croaking](https://leetcode.com/problems/minimum-number-of-frogs-croaking/) | Medium | 5/10 | 51.1% | [ ] |
| 880 | [Decoded String at Index](https://leetcode.com/problems/decoded-string-at-index/) | Medium | 6/10 | 37.3% | [ ] |
| 68 | [Text Justification](https://leetcode.com/problems/text-justification/) | Hard | 7/10 | 51.0% | [ ] |

## frequency_count

**What it is** — Frequency counting uses a hash map or fixed-size array (size 26 for lowercase letters) to tally how often each character appears, then draws conclusions from those counts. Recognize this pattern when the problem involves anagrams, character balance, or conditions that depend on how many times characters appear rather than their positions.

**Common steps**
1. Create a frequency map (dictionary or array of size 26) for the relevant string(s).
2. Populate the map by iterating over each character.
3. If comparing two strings, either subtract one map from another or compare counts directly.
4. Evaluate the condition on the counts (e.g., all even, at most one odd, sum of differences, odd-count characters vs. k).
5. Return the result based on whether the count condition is satisfied.

**Key variations**
- Anagram checks: two strings have identical frequency maps.
- Minimum operations to make anagrams: sum of absolute differences in counts divided by 2.
- Palindrome construction: count characters with odd frequency — at most one is allowed.
- Substrings with all vowels: sliding window combined with frequency tracking.
- Beauty/score metrics: comparing max and min counts within every possible substring.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1935 | [Maximum Number of Words You Can Type](https://leetcode.com/problems/maximum-number-of-words-you-can-type/) | Easy | 1/10 | 82.9% | [ ] |
| 1704 | [Determine if String Halves Are Alike](https://leetcode.com/problems/determine-if-string-halves-are-alike/) | Easy | 1/10 | 78.8% | [ ] |
| 1347 | [Minimum Number of Steps to Make Two Strings Anagram](https://leetcode.com/problems/minimum-number-of-steps-to-make-two-strings-anagram/) | Medium | 2/10 | 82.5% | [ ] |
| 2186 | [Minimum Number of Steps to Make Two Strings Anagram II](https://leetcode.com/problems/minimum-number-of-steps-to-make-two-strings-anagram-ii/) | Medium | 2/10 | 73.0% | [ ] |
| 2062 | [Count Vowel Substrings of a String](https://leetcode.com/problems/count-vowel-substrings-of-a-string/) | Easy | 3/10 | 73.1% | [ ] |
| 1400 | [Construct K Palindrome Strings](https://leetcode.com/problems/construct-k-palindrome-strings/) | Medium | 3/10 | 68.5% | [ ] |
| 1781 | [Sum of Beauty of All Substrings](https://leetcode.com/problems/sum-of-beauty-of-all-substrings/) | Medium | 4/10 | 73.9% | [ ] |
| 1737 | [Change Minimum Characters to Satisfy One of Three Conditions](https://leetcode.com/problems/change-minimum-characters-to-satisfy-one-of-three-conditions/) | Medium | 6/10 | 37.9% | [ ] |

## string_parsing

**What it is** — String parsing means extracting structured information (numbers, tokens, fields) from raw text by scanning through it and applying format rules. Recognize this pattern when the input is a string that encodes data in a defined format — like dates, IP addresses, equations, or code — and you must validate or decode it.

**Common steps**
1. Identify the tokens or delimiters that separate meaningful parts of the string (spaces, brackets, colons, `#`, etc.).
2. Split or scan the string to isolate each token or field.
3. Validate or convert each token according to the format rules (digit check, range check, type check).
4. Handle edge cases: leading zeros, empty tokens, mixed alphanumeric content, ambiguous boundaries.
5. Accumulate the decoded output or return a boolean validity result.

**Key variations**
- Format validation: check if the entire string matches a strict grammar (IP address, valid number, email).
- Decoding/mapping: translate each token to a value using a lookup (alphabet-to-integer, entity name to symbol).
- Extraction with filtering: pull out only specific token types (numbers, words, brackets) and ignore the rest.
- Multi-pass parsing: strip comments or markup in one pass, then evaluate the cleaned string in a second pass.
- State machine parsing: track whether you are inside a bracket, comment block, or quoted section.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1678 | [Goal Parser Interpretation](https://leetcode.com/problems/goal-parser-interpretation/) | Easy | 1/10 | 88.1% | [ ] |
| 1880 | [Check if Word Equals Summation of Two Words](https://leetcode.com/problems/check-if-word-equals-summation-of-two-words/) | Easy | 1/10 | 75.3% | [ ] |
| 2042 | [Check if Numbers Are Ascending in a Sentence](https://leetcode.com/problems/check-if-numbers-are-ascending-in-a-sentence/) | Easy | 1/10 | 73.1% | [ ] |
| 520 | [Detect Capital](https://leetcode.com/problems/detect-capital/) | Easy | 1/10 | 56.6% | [ ] |
| 434 | [Number of Segments in a String](https://leetcode.com/problems/number-of-segments-in-a-string/) | Easy | 1/10 | 37.3% | [ ] |
| 1309 | [Decrypt String from Alphabet to Integer Mapping](https://leetcode.com/problems/decrypt-string-from-alphabet-to-integer-mapping/) | Easy | 2/10 | 80.6% | [ ] |
| 1507 | [Reformat Date](https://leetcode.com/problems/reformat-date/) | Easy | 2/10 | 68.5% | [ ] |
| 929 | [Unique Email Addresses](https://leetcode.com/problems/unique-email-addresses/) | Easy | 2/10 | 67.9% | [ ] |
| 551 | [Student Attendance Record I](https://leetcode.com/problems/student-attendance-record-i/) | Easy | 2/10 | 50.2% | [ ] |
| 1805 | [Number of Different Integers in a String](https://leetcode.com/problems/number-of-different-integers-in-a-string/) | Easy | 2/10 | 40.3% | [ ] |
| 1807 | [Evaluate the Bracket Pairs of a String](https://leetcode.com/problems/evaluate-the-bracket-pairs-of-a-string/) | Medium | 3/10 | 69.5% | [ ] |
| 831 | [Masking Personal Information](https://leetcode.com/problems/masking-personal-information/) | Medium | 3/10 | 55.0% | [ ] |
| 1410 | [HTML Entity Parser](https://leetcode.com/problems/html-entity-parser/) | Medium | 3/10 | 50.1% | [ ] |
| 2047 | [Number of Valid Words in a Sentence](https://leetcode.com/problems/number-of-valid-words-in-a-sentence/) | Easy | 3/10 | 31.1% | [ ] |
| 722 | [Remove Comments](https://leetcode.com/problems/remove-comments/) | Medium | 5/10 | 40.1% | [ ] |
| 468 | [Validate IP Address](https://leetcode.com/problems/validate-ip-address/) | Medium | 5/10 | 28.3% | [ ] |
| 8 | [String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/) | Medium | 5/10 | 20.9% | [ ] |
| 816 | [Ambiguous Coordinates](https://leetcode.com/problems/ambiguous-coordinates/) | Medium | 6/10 | 56.4% | [ ] |
| 65 | [Valid Number](https://leetcode.com/problems/valid-number/) | Hard | 7/10 | 22.9% | [ ] |

## subsequence_matching

**What it is** — Subsequence matching checks whether the characters of one string appear in another string in order, but not necessarily contiguously. Recognize this pattern when the problem asks if one string can be "embedded" in another by only skipping characters, or when you need to find the longest string from a set that satisfies this property.

**Common steps**
1. Use two pointers: one for the candidate subsequence `s` and one for the source string `t`.
2. Advance the pointer in `t` one character at a time; when `t[j] == s[i]`, advance `i` as well.
3. If `i` reaches `len(s)`, `s` is a subsequence of `t`.
4. For "longest word" problems, sort candidates by length (descending), then apply the two-pointer check to each; return the first match.
5. For "uncommon subsequence" problems, leverage the insight that a string is its own longest uncommon subsequence relative to any string it is not equal to.

**Key variations**
- Simple is-subsequence check between two strings.
- Finding the longest word in a dictionary that is a subsequence of a target string (sort by length, then check).
- Uncommon subsequences: the answer is often the longer of two unequal strings, or -1 if they are equal.
- Multiple candidates: batch the two-pointer check across an array of strings.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 524 | [Longest Word in Dictionary through Deleting](https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/) | Medium | 4/10 | 52.7% | [ ] |
| 522 | [Longest Uncommon Subsequence II](https://leetcode.com/problems/longest-uncommon-subsequence-ii/) | Medium | 4/10 | 44.8% | [ ] |

## greedy_construction

**What it is** — Greedy construction builds the output string one character or segment at a time, always making the locally optimal choice (e.g., smallest character, most balanced distribution) without backtracking. Recognize this pattern when the goal is to produce a string that satisfies a constraint (no consecutive repeats, lexicographically smallest/largest, odd counts) and a local decision at each step is sufficient.

**Common steps**
1. Identify the objective (lexicographically smallest/largest, no consecutive repeats, specific character parity).
2. Determine what information governs each choice (remaining character counts, last character appended, current position parity).
3. At each position, greedily select the best valid character given the current state.
4. Update the state (decrement counts, record last appended character).
5. Repeat until the output is complete; verify the final string meets any global constraints.

**Key variations**
- Avoiding consecutive repeats: if the best character equals the last appended one, use the second-best instead.
- Lexicographically smallest: always pick the smallest available character that does not violate constraints.
- Parity enforcement: adjust character counts by ±1 to ensure all counts are odd.
- Sorted cycling: repeatedly pick characters in sorted order (ascending then descending) until exhausted.
- Merging strings: greedily absorb one string as a suffix/prefix of another to minimize total length.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1374 | [Generate a String With Characters That Have Odd Counts](https://leetcode.com/problems/generate-a-string-with-characters-that-have-odd-counts/) | Easy | 1/10 | 78.5% | [ ] |
| 1370 | [Increasing Decreasing String](https://leetcode.com/problems/increasing-decreasing-string/) | Easy | 2/10 | 77.3% | [ ] |
| 1957 | [Delete Characters to Make Fancy String](https://leetcode.com/problems/delete-characters-to-make-fancy-string/) | Easy | 2/10 | 74.1% | [ ] |
| 1576 | [Replace All ?'s to Avoid Consecutive Repeating Characters](https://leetcode.com/problems/replace-all-s-to-avoid-consecutive-repeating-characters/) | Easy | 2/10 | 45.3% | [ ] |
| 681 | [Next Closest Time](https://leetcode.com/problems/next-closest-time/) :lock: | Medium | 5/10 | 47.0% | [ ] |
| 3403 | [Find the Lexicographically Largest String From the Box I](https://leetcode.com/problems/find-the-lexicographically-largest-string-from-the-box-i/) | Medium | 5/10 | 40.9% | [ ] |
| 2207 | [Maximize Number of Subsequences in a String](https://leetcode.com/problems/maximize-number-of-subsequences-in-a-string/) | Medium | 6/10 | 36.0% | [ ] |
| 2800 | [Shortest String That Contains Three Strings](https://leetcode.com/problems/shortest-string-that-contains-three-strings/) | Medium | 6/10 | 31.7% | [ ] |
| 3474 | [Lexicographically Smallest Generated String](https://leetcode.com/problems/lexicographically-smallest-generated-string/) | Hard | 8/10 | 53.5% | [ ] |

## interval_merging

**What it is** — Interval merging on strings maps each substring match to a [start, end] interval, then merges overlapping intervals so that operations (like adding bold tags) are applied to the correct combined ranges. Recognize this pattern when the problem involves marking or annotating overlapping regions of a string based on multiple keyword matches.

**Common steps**
1. For each keyword or pattern, find all occurrences in the target string and record their [start, end) intervals.
2. Sort all intervals by start index.
3. Merge overlapping or adjacent intervals: if the current interval's start is within the previous interval's end, extend the previous interval's end to the maximum of the two ends.
4. Using the merged intervals, construct the output by interleaving the original string characters with the required markers (e.g., `<b>` and `</b>` tags).
5. Append any remaining characters after the last interval.

**Key variations**
- Multiple keywords to match: find intervals for each word, then merge all of them together.
- Tag insertion vs. boolean marking: some problems want the annotated string; others want a boolean array indicating bold positions.
- Overlapping vs. adjacent merging: decide whether touching intervals (end of one equals start of next) should be merged.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 758 | [Bold Words in String](https://leetcode.com/problems/bold-words-in-string/) :lock: | Medium | 4/10 | 52.5% | [ ] |
| 616 | [Add Bold Tag in String](https://leetcode.com/problems/add-bold-tag-in-string/) :lock: | Medium | 5/10 | 51.4% | [ ] |

## sorting_and_ordering

**What it is** — Sorting and ordering problems require rearranging words or characters within a string according to a custom rule — by embedded index, by word length, by a reference order, or by a custom comparator. Recognize this pattern when the problem's output is a permutation of the input tokens sorted by some criterion other than simple lexicographic order.

**Common steps**
1. Tokenize the string into the units to be sorted (words, characters, log entries).
2. Define the sort key: extract the embedded ordering field, compute a numeric property (word length), or build a comparator from a reference string.
3. Apply a stable sort using the key (use Python's `sorted` with a `key` argument, or implement a custom comparator with `functools.cmp_to_key`).
4. For multi-criteria sorts (e.g., letter-logs before digit-logs, then lexicographic), compose the key as a tuple.
5. Reconstruct the output string by joining the sorted tokens with the appropriate separator.

**Key variations**
- Index-embedded sort: each word contains a trailing number that indicates its position; strip the number and sort by it.
- Length-based sort: sort words by length, then alphabetically for ties.
- Reference-order sort: given a custom alphabet or priority string, remap characters and sort.
- Partial sort: separate items into two groups (letter logs vs. digit logs), sort one group, and preserve the order of the other.
- Next-permutation: find the lexicographically next arrangement via a sequence of swaps (useful for "kth smallest" problems).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1859 | [Sorting the Sentence](https://leetcode.com/problems/sorting-the-sentence/) | Easy | 1/10 | 84.1% | [ ] |
| 791 | [Custom Sort String](https://leetcode.com/problems/custom-sort-string/) | Medium | 3/10 | 72.3% | [ ] |
| 1451 | [Rearrange Words in a Sentence](https://leetcode.com/problems/rearrange-words-in-a-sentence/) | Medium | 3/10 | 67.0% | [ ] |
| 937 | [Reorder Data in Log Files](https://leetcode.com/problems/reorder-data-in-log-files/) | Medium | 3/10 | 56.8% | [ ] |
| 1850 | [Minimum Adjacent Swaps to Reach the Kth Smallest Number](https://leetcode.com/problems/minimum-adjacent-swaps-to-reach-the-kth-smallest-number/) | Medium | 6/10 | 71.8% | [ ] |
| 3406 | [Find the Lexicographically Largest String From the Box II](https://leetcode.com/problems/find-the-lexicographically-largest-string-from-the-box-ii/) :lock: | Hard | 7/10 | 49.2% | [ ] |
| 3735 | [Lexicographically Smallest String After Reverse II](https://leetcode.com/problems/lexicographically-smallest-string-after-reverse-ii/) :lock: | Hard | 9/10 | 46.2% | [ ] |

## pattern_matching_kmp

**What it is** — Pattern matching finds all positions where a pattern string occurs inside a text string, in O(n + m) time using the Knuth-Morris-Pratt (KMP) algorithm or the Z-algorithm. Recognize this pattern when the problem involves substring search, detecting repeated structure, or rotating/concatenating strings and checking containment — especially when brute-force O(n*m) would be too slow.

**Common steps**
1. Build the failure function (also called the prefix function or LPS array) for the pattern: for each position `i`, compute the length of the longest proper prefix of `pattern[:i+1]` that is also a suffix.
2. Use two pointers `i` (text) and `j` (pattern): advance both when characters match; on mismatch, fall back `j` using the failure function without resetting `i`.
3. When `j` reaches `len(pattern)`, a match is found at index `i - j`; reset `j = failure[j-1]` to continue searching.
4. For rotation problems, check if `pattern` is a substring of `text + text`.
5. For repeated-substring problems, check if `len(s) % (len(s) - failure[-1]) == 0`.

**Key variations**
- Basic substring search: find the first or all occurrences of a pattern in text.
- Rotation detection: `s2` is a rotation of `s1` iff `s2` is a substring of `s1 + s1`.
- Repeated substring pattern: use the failure function's last value to determine the smallest repeating unit.
- Longest happy prefix: the failure function directly gives the answer (longest prefix that is also a suffix).
- Z-function variant: compute the Z-array for direct prefix matching; useful for scoring/counting prefix matches.
- Edit-distance matching: problems where up to k edits are allowed require a modified matching strategy.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1967 | [Number of Strings That Appear as Substrings in Word](https://leetcode.com/problems/number-of-strings-that-appear-as-substrings-in-word/) | Easy | 1/10 | 82.5% | [ ] |
| 1408 | [String Matching in an Array](https://leetcode.com/problems/string-matching-in-an-array/) | Easy | 2/10 | 69.8% | [ ] |
| 796 | [Rotate String](https://leetcode.com/problems/rotate-string/) | Easy | 2/10 | 66.6% | [ ] |
| 1668 | [Maximum Repeating Substring](https://leetcode.com/problems/maximum-repeating-substring/) | Easy | 3/10 | 41.6% | [ ] |
| 2452 | [Words Within Two Edits of Dictionary](https://leetcode.com/problems/words-within-two-edits-of-dictionary/) | Medium | 4/10 | 73.5% | [ ] |
| 1016 | [Binary String With Substrings Representing 1 To N](https://leetcode.com/problems/binary-string-with-substrings-representing-1-to-n/) | Medium | 4/10 | 58.5% | [ ] |
| 459 | [Repeated Substring Pattern](https://leetcode.com/problems/repeated-substring-pattern/) | Easy | 4/10 | 48.2% | [ ] |
| 28 | [Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/) | Easy | 4/10 | 46.6% | [ ] |
| 686 | [Repeated String Match](https://leetcode.com/problems/repeated-string-match/) | Medium | 4/10 | 38.8% | [ ] |
| 3006 | [Find Beautiful Indices in the Given Array I](https://leetcode.com/problems/find-beautiful-indices-in-the-given-array-i/) | Medium | 6/10 | 40.8% | [ ] |
| 1392 | [Longest Happy Prefix](https://leetcode.com/problems/longest-happy-prefix/) | Hard | 7/10 | 53.0% | [ ] |
| 2301 | [Match Substring After Replacement](https://leetcode.com/problems/match-substring-after-replacement/) | Hard | 7/10 | 43.3% | [ ] |
| 2223 | [Sum of Scores of Built Strings](https://leetcode.com/problems/sum-of-scores-of-built-strings/) | Hard | 8/10 | 48.3% | [ ] |
| 214 | [Shortest Palindrome](https://leetcode.com/problems/shortest-palindrome/) | Hard | 8/10 | 42.4% | [ ] |
| 3008 | [Find Beautiful Indices in the Given Array II](https://leetcode.com/problems/find-beautiful-indices-in-the-given-array-ii/) | Hard | 8/10 | 27.8% | [ ] |
| 3455 | [Shortest Matching Substring](https://leetcode.com/problems/shortest-matching-substring/) | Hard | 9/10 | 24.1% | [ ] |

## palindrome

**What it is** — Palindrome problems check or construct strings that read the same forwards and backwards, most commonly using the expand-around-center technique or Manacher's algorithm. Recognize this pattern when the problem mentions substrings or subsequences that are symmetric, or when you need to find the longest/shortest palindromic structure.

**Common steps**
1. For single-string palindrome checks, use two pointers from both ends moving inward, comparing characters.
2. For finding the longest palindromic substring, try expanding around each center: iterate over each index as an odd-length center and each pair of adjacent indices as an even-length center.
3. Track the maximum length and the corresponding start index as you expand.
4. For palindrome construction problems (e.g., shortest palindrome by prepending), use KMP to find the longest palindromic prefix, then prepend the reversed remainder.
5. For advanced problems requiring O(n) time across all substrings, apply Manacher's algorithm to compute the radius of the longest palindrome centered at every position.

**Key variations**
- Palindrome check: simple two-pointer or slicing (`s == s[::-1]`).
- Longest palindromic substring: expand-around-center in O(n^2), or Manacher's in O(n).
- Palindromic subsequences: count or remove subsequences using frequency analysis (not continuity).
- Palindrome permutation: check if any rearrangement of the characters forms a palindrome (at most one odd-frequency character).
- Constructive palindromes: given constraints, build the lexicographically smallest/largest valid palindrome.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 2108 | [Find First Palindromic String in the Array](https://leetcode.com/problems/find-first-palindromic-string-in-the-array/) | Easy | 1/10 | 84.0% | [ ] |
| 1332 | [Remove Palindromic Subsequences](https://leetcode.com/problems/remove-palindromic-subsequences/) | Easy | 2/10 | 77.0% | [ ] |
| 5 | [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) | Medium | 6/10 | 37.8% | [ ] |
| 3734 | [Lexicographically Smallest Palindromic Permutation Greater Than Target](https://leetcode.com/problems/lexicographically-smallest-palindromic-permutation-greater-than-target/) | Hard | 8/10 | 25.1% | [ ] |
| 1960 | [Maximum Product of the Length of Two Palindromic Substrings](https://leetcode.com/problems/maximum-product-of-the-length-of-two-palindromic-substrings/) | Hard | 9/10 | 31.0% | [ ] |

## hashing_and_deduplication

**What it is** — Hashing and deduplication use hash maps or hash sets to detect duplicate strings, group equivalent strings, or efficiently look up whether a substring has been seen before. Recognize this pattern when the problem requires fast equality checks across many strings, or when counting distinct substrings would be too slow without a hash-based approach.

**Common steps**
1. Choose a hash structure: a set for membership/deduplication, a map for grouping or counting.
2. Define the key: the raw string, a normalized form (lowercase, sorted characters), or a rolling hash value for substrings.
3. For substring problems, use a rolling hash (polynomial hashing) to compute the hash of each substring in O(1) after O(n) preprocessing.
4. Insert each string or substring hash into the set; check for collisions with actual string comparison to avoid false positives.
5. Return the count of distinct entries, the grouped result, or the answer derived from the deduplicated set.

**Key variations**
- Simple deduplication: insert strings into a set and return its size.
- Case-insensitive or normalized grouping: normalize each string before hashing (e.g., lowercase, strip punctuation).
- Rolling hash for substring distinctness: enumerate all substrings via two nested loops, hash each, and add to a set.
- Double hashing: use two independent hash functions to reduce collision probability for large inputs.
- Longest common extension: combine hashing with binary search to find the longest matching prefix between two strings.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 2451 | [Odd String Difference](https://leetcode.com/problems/odd-string-difference/) | Easy | 3/10 | 61.9% | [ ] |
| 966 | [Vowel Spellchecker](https://leetcode.com/problems/vowel-spellchecker/) | Medium | 4/10 | 61.4% | [ ] |
| 2168 | [Unique Substrings With Equal Digit Frequency](https://leetcode.com/problems/unique-substrings-with-equal-digit-frequency/) :lock: | Medium | 6/10 | 64.6% | [ ] |
| 3135 | [Equalize Strings by Adding or Removing Characters at Ends](https://leetcode.com/problems/equalize-strings-by-adding-or-removing-characters-at-ends/) :lock: | Medium | 6/10 | 56.2% | [ ] |
| 1316 | [Distinct Echo Substrings](https://leetcode.com/problems/distinct-echo-substrings/) | Hard | 7/10 | 53.2% | [ ] |
| 3529 | [Count Cells in Overlapping Horizontal and Vertical Substrings](https://leetcode.com/problems/count-cells-in-overlapping-horizontal-and-vertical-substrings/) | Medium | 8/10 | 27.3% | [ ] |
| 3292 | [Minimum Number of Valid Strings to Form Target II](https://leetcode.com/problems/minimum-number-of-valid-strings-to-form-target-ii/) | Hard | 9/10 | 20.5% | [ ] |

## contribution_counting

**What it is** — Contribution counting avoids enumerating all substrings explicitly by computing, for each character (or element), how many substrings it contributes to the answer. Recognize this pattern when the problem asks for a sum over all substrings of some per-character property, and a direct O(n^2) or O(n^3) enumeration would be too slow.

**Common steps**
1. For each position `i`, determine the range of substrings in which character `s[i]` contributes uniquely (or contributes at all) to the target metric.
2. Find the previous occurrence of the same character to the left (`left[i]`) and the next occurrence to the right (`right[i]`), using a monotonic scan or a last-seen array.
3. The number of substrings where `s[i]` is the unique representative is `(i - left[i]) * (right[i] - i)`.
4. Multiply this count by the per-character contribution value (e.g., 1 for uniqueness, the character's value, etc.) and add to the running total.
5. Sum contributions for all characters and return the total.

**Key variations**
- Unique character contribution: each character contributes 1 for every substring where it appears exactly once (use left/right boundary arrays).
- First/last occurrence boundary: left boundary is the previous index of the same character (or -1); right boundary is the next index (or n).
- Weighted contribution: multiply the count by a weight derived from the character (e.g., its numeric value or frequency rank).
- Two-pointer reduction: for some variants, reformulate as "count substrings with at most k distinct" minus "count substrings with at most k-1 distinct."

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 828 | [Count Unique Characters of All Substrings of a Given String](https://leetcode.com/problems/count-unique-characters-of-all-substrings-of-a-given-string/) | Hard | 7/10 | 53.6% | [ ] |
