# Math

129 problems across 11 patterns.

## big_integer_arithmetic

**What it is** — Big integer arithmetic problems require you to perform addition or multiplication on numbers that are too large to fit in a standard integer type, so the numbers are represented as strings or digit arrays. You recognize this pattern when the problem gives you numeric strings and asks you to compute a sum or product without converting to a native integer.

**Common steps**
1. Initialize two pointers at the end of each input string/array (least significant digit).
2. Iterate from right to left, processing one digit from each operand per step.
3. Compute the current digit sum (or product contribution) plus any carry from the previous step.
4. Append `sum % 10` (or the appropriate base) to a result buffer and set `carry = sum // 10`.
5. After the loop, if a carry remains, append it.
6. Reverse the result buffer and return it as a string.

**Key variations**
- Addition of two strings: straightforward two-pointer approach with carry propagation.
- Addition of a single integer to an array-form number: add the integer to the lowest digit and propagate carry leftward.
- Multiplication of two strings: requires an intermediate result array of size `m + n`; each pair of digits contributes to two positions.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 415 | [Add Strings](https://leetcode.com/problems/add-strings/) | Easy | 3/10 | 52.2% | [ ] |
| 989 | [Add to Array-Form of Integer](https://leetcode.com/problems/add-to-array-form-of-integer/) | Easy | 3/10 | 45.5% | [ ] |
| 43 | [Multiply Strings](https://leetcode.com/problems/multiply-strings/) | Medium | 6/10 | 44.1% | [ ] |

## number_base_conversion

**What it is** — Number base conversion problems ask you to convert a number between two positional numeral systems (e.g., decimal to base 7, or a column title string to a base-26 number). The core idea is that each digit position represents a power of the target base, so you either repeatedly divide (for encoding) or accumulate a weighted sum (for decoding).

**Common steps**
1. Handle the edge case of zero or negative input explicitly if needed.
2. For encoding (decimal to base B): repeatedly take `n % B` for the current digit, then set `n = n // B`; collect digits in reverse order.
3. For decoding (base B to decimal): iterate left to right, maintaining a running total as `total = total * B + digit_value`.
4. Map digit values to their character representations (e.g., 0-9 then A-Z for hex, or A-Z for Excel columns).
5. Watch for 1-indexed bases like Excel columns where there is no zero digit — subtract 1 before taking the modulus.
6. Return the assembled result string, reversing if you built it from least significant to most significant digit.

**Key variations**
- Straight base conversion (Base 7, hex): standard repeated-division approach.
- 1-indexed alphabetic bases (Excel column): must adjust by subtracting 1 before each modulo to handle the absence of a "0" digit.
- Binary search on the base (Smallest Good Base): the exponent count is bounded by log, so try all possible lengths and solve for the base mathematically.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 171 | [Excel Sheet Column Number](https://leetcode.com/problems/excel-sheet-column-number/) | Easy | 2/10 | 67.7% | [ ] |
| 504 | [Base 7](https://leetcode.com/problems/base-7/) | Easy | 2/10 | 54.5% | [ ] |
| 1271 | [Hexspeak](https://leetcode.com/problems/hexspeak/) :lock: | Easy | 3/10 | 58.4% | [ ] |
| 2802 | [Find The K-th Lucky Number](https://leetcode.com/problems/find-the-k-th-lucky-number/) :lock: | Medium | 4/10 | 76.0% | [ ] |
| 168 | [Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/) | Easy | 4/10 | 46.4% | [ ] |
| 483 | [Smallest Good Base](https://leetcode.com/problems/smallest-good-base/) | Hard | 9/10 | 46.0% | [ ] |

## number_representation_conversion

**What it is** — Number representation conversion problems require translating between a standard integer and a symbolic/linguistic notation system (Roman numerals, English words). You recognize this pattern when the mapping rules between symbols and values are fixed and finite, and the conversion follows a greedy or lookup-table approach.

**Common steps**
1. Build a lookup table of value-to-symbol (or symbol-to-value) mappings, ordered from largest to smallest.
2. For integer-to-symbol: greedily subtract the largest possible value from the number, appending the corresponding symbol, until the number reaches zero.
3. For symbol-to-integer: scan left to right; if the current symbol is less than the next, subtract it; otherwise add it.
4. For English words: break the number into groups of three digits (ones, thousands, millions, billions) and convert each group independently, then concatenate with the group label.
5. Handle edge cases such as subtractive notation in Roman numerals (IV, IX, XL, etc.) by including those pairs in the lookup table.

**Key variations**
- Simple symbol-to-integer (Roman to Integer): single left-to-right pass with subtraction logic.
- Integer-to-symbol (Integer to Roman): greedy subtraction from a value-symbol table including subtractive pairs.
- Recursive chunking (Integer to English Words): handle groups of thousands recursively, with special cases for 0 and teens (11-19).

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 13 | [Roman to Integer](https://leetcode.com/problems/roman-to-integer/) | Easy | 2/10 | 66.6% | [ ] |
| 12 | [Integer to Roman](https://leetcode.com/problems/integer-to-roman/) | Medium | 4/10 | 70.9% | [ ] |
| 273 | [Integer to English Words](https://leetcode.com/problems/integer-to-english-words/) | Hard | 7/10 | 35.0% | [ ] |

## simulation

**What it is** — Simulation problems ask you to directly model a process or set of rules step by step, rather than derive a closed-form solution. You recognize this pattern when the problem describes a sequence of operations (moves, switches, rounds) and asks for the state after all operations are applied, or when it checks a cyclical or repeating property.

**Common steps**
1. Carefully parse the problem's rules and identify what state you need to track (position, value, count, etc.).
2. Implement the operations exactly as described, iterating over each step or instruction.
3. Look for mathematical shortcuts or invariants (e.g., a robot's path is bounded if and only if it returns to origin or faces a non-north direction after one cycle).
4. Apply modular arithmetic or period detection to avoid simulating an astronomically large number of steps.
5. Return the final state or the answer derived from it.

**Key variations**
- Direct state simulation (Fizz Buzz, Complex Number Multiplication): apply each rule to update state.
- Cycle/period detection (Robot Bounded In Circle, Bulb Switcher II): simulate one period and check if the pattern repeats.
- Calendar and date math (Day of the Year, Number of Days Between Two Dates): precompute days-per-month arrays and account for leap years.
- Equation solving via simulation (Solve the Equation): parse and accumulate coefficients on each side, then solve algebraically.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1812 | [Determine Color of a Chessboard Square](https://leetcode.com/problems/determine-color-of-a-chessboard-square/) | Easy | 1/10 | 79.8% | [ ] |
| 412 | [Fizz Buzz](https://leetcode.com/problems/fizz-buzz/) | Easy | 1/10 | 75.5% | [ ] |
| 1399 | [Count Largest Group](https://leetcode.com/problems/count-largest-group/) | Easy | 2/10 | 74.7% | [ ] |
| 800 | [Similar RGB Color](https://leetcode.com/problems/similar-rgb-color/) :lock: | Easy | 3/10 | 67.9% | [ ] |
| 1360 | [Number of Days Between Two Dates](https://leetcode.com/problems/number-of-days-between-two-dates/) | Easy | 3/10 | 52.7% | [ ] |
| 1154 | [Day of the Year](https://leetcode.com/problems/day-of-the-year/) | Easy | 3/10 | 50.0% | [ ] |
| 537 | [Complex Number Multiplication](https://leetcode.com/problems/complex-number-multiplication/) | Medium | 4/10 | 73.5% | [ ] |
| 1904 | [The Number of Full Rounds You Have Played](https://leetcode.com/problems/the-number-of-full-rounds-you-have-played/) | Medium | 4/10 | 43.4% | [ ] |
| 1006 | [Clumsy Factorial](https://leetcode.com/problems/clumsy-factorial/) | Medium | 5/10 | 61.3% | [ ] |
| 1041 | [Robot Bounded In Circle](https://leetcode.com/problems/robot-bounded-in-circle/) | Medium | 5/10 | 56.5% | [ ] |
| 423 | [Reconstruct Original Digits from English](https://leetcode.com/problems/reconstruct-original-digits-from-english/) | Medium | 5/10 | 52.9% | [ ] |
| 672 | [Bulb Switcher II](https://leetcode.com/problems/bulb-switcher-ii/) | Medium | 6/10 | 50.1% | [ ] |
| 640 | [Solve the Equation](https://leetcode.com/problems/solve-the-equation/) | Medium | 6/10 | 46.2% | [ ] |
| 843 | [Guess the Word](https://leetcode.com/problems/guess-the-word/) | Hard | 8/10 | 36.8% | [ ] |
| 3680 | [Generate Schedule](https://leetcode.com/problems/generate-schedule/) | Medium | 8/10 | 24.5% | [ ] |
| 972 | [Equal Rational Numbers](https://leetcode.com/problems/equal-rational-numbers/) | Hard | 9/10 | 46.1% | [ ] |

## digit_analysis

**What it is** — Digit analysis problems require you to examine the individual digits of numbers rather than the numbers themselves as whole values. You recognize this pattern when the problem involves counting digits, checking digit properties, or working across a range of numbers where digit-level structure determines the answer.

**Common steps**
1. Determine how to extract digits from a number (repeated `% 10` and `// 10`, or string conversion for simplicity).
2. For range-based counting, identify the digit position you are analyzing and count contributions mathematically using division and modulo.
3. For property checks on a range, iterate through the range and apply the digit-level predicate per number.
4. Use frequency maps or sets when the problem involves uniqueness or digit composition.
5. Watch for boundary conditions at each digit position (leading zeros, the current digit itself, higher digits).

**Key variations**
- Digit sum grouping (Maximum Number of Balls in a Box): compute digit sum per number, bucket results in a hash map.
- Digit property check over a range (Rotated Digits): iterate the range and validate each number's digit set against allowed/disallowed digits.
- Positional digit counting (Number of Digit One, Nth Digit): use mathematical formulas per digit position to count occurrences without iterating every number.
- Balanced digit composition (Next Greater Numerically Balanced Number): brute-force upward from n, checking digit frequency equals digit value for each candidate.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 3032 | [Count Numbers With Unique Digits II](https://leetcode.com/problems/count-numbers-with-unique-digits-ii/) :lock: | Easy | 2/10 | 87.2% | [ ] |
| 1742 | [Maximum Number of Balls in a Box](https://leetcode.com/problems/maximum-number-of-balls-in-a-box/) | Easy | 2/10 | 74.9% | [ ] |
| 788 | [Rotated Digits](https://leetcode.com/problems/rotated-digits/) | Medium | 5/10 | 63.9% | [ ] |
| 2048 | [Next Greater Numerically Balanced Number](https://leetcode.com/problems/next-greater-numerically-balanced-number/) | Medium | 5/10 | 63.1% | [ ] |
| 400 | [Nth Digit](https://leetcode.com/problems/nth-digit/) | Medium | 6/10 | 38.2% | [ ] |
| 233 | [Number of Digit One](https://leetcode.com/problems/number-of-digit-one/) | Hard | 8/10 | 38.6% | [ ] |

## randomized_algorithms

**What it is** — Randomized algorithm problems require you to sample uniformly at random from a data structure, often with constraints like weighted probability or an excluded blacklist. The core idea is to map a random number in `[0, N)` to a valid element, using techniques like reservoir sampling or prefix-sum binary search.

**Common steps**
1. Understand the sample space: what are all valid items, and what probability should each item have?
2. For uniform sampling from an unknown-length stream, use reservoir sampling: keep the current item with probability `1/count` seen so far.
3. For weighted sampling, build a prefix sum array of weights and use binary search to find which bucket a random float falls into.
4. For blacklist exclusion, map each blacklisted index in `[0, N)` to a valid index in `[N-k, N)` using a hash map, then sample from `[0, N-k)`.
5. Always use the language's built-in random functions and seed appropriately for reproducibility in tests.

**Key variations**
- Reservoir sampling (Linked List Random Node, Random Pick Index): single-pass over a stream where size is unknown.
- Prefix-sum weighted sampling (Random Pick with Weight): precompute cumulative weights, binary search on a random value.
- Area-weighted 2D sampling (Random Point in Non-overlapping Rectangles): weight rectangles by area, pick a rectangle, then a point within it uniformly.
- Blacklist remapping (Random Pick with Blacklist): compress the valid range and use a map to redirect invalid indices.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 398 | [Random Pick Index](https://leetcode.com/problems/random-pick-index/) | Medium | 4/10 | 65.1% | [ ] |
| 384 | [Shuffle an Array](https://leetcode.com/problems/shuffle-an-array/) | Medium | 4/10 | 59.7% | [ ] |
| 382 | [Linked List Random Node](https://leetcode.com/problems/linked-list-random-node/) | Medium | 5/10 | 64.8% | [ ] |
| 528 | [Random Pick with Weight](https://leetcode.com/problems/random-pick-with-weight/) | Medium | 5/10 | 49.1% | [ ] |
| 497 | [Random Point in Non-overlapping Rectangles](https://leetcode.com/problems/random-point-in-non-overlapping-rectangles/) | Medium | 6/10 | 39.7% | [ ] |
| 710 | [Random Pick with Blacklist](https://leetcode.com/problems/random-pick-with-blacklist/) | Hard | 8/10 | 35.0% | [ ] |

## geometry

**What it is** — Geometry problems require reasoning about points, lines, areas, or shapes in 2D (or 3D) space using coordinate math. You recognize this pattern when the problem involves distances, slopes, intersections, areas, or spatial relationships between coordinates, and the key insight is typically a geometric formula or property (cross product, collinearity, convex hull).

**Common steps**
1. Identify the geometric objects involved (points, line segments, rectangles, polygons) and choose an appropriate representation.
2. Use integer arithmetic wherever possible (cross products, squared distances) to avoid floating-point precision errors.
3. For collinearity or slope comparisons, represent slope as a reduced fraction `(dy/gcd, dx/gcd)` rather than a float.
4. For area and intersection problems, apply the Shoelace formula or inclusion-exclusion on axis-aligned rectangles.
5. For convex hull problems, use the Graham scan or Andrew's monotone chain algorithm.
6. Validate edge cases: duplicate points, vertical lines, zero-area shapes.

**Key variations**
- Area computation (Largest Triangle Area, Surface Area of 3D Shapes): apply closed-form geometric formulas.
- Collinearity and line grouping (Max Points on a Line): group points by slope using reduced-fraction keys in a hash map.
- Convex hull (Erect the Fence): Andrew's monotone chain; sort by x then build lower and upper hulls using cross products.
- Rectangle validation (Perfect Rectangle): use a set to track corners; a perfect tiling has exactly 4 unique corners and total area equals bounding rectangle area.
- Self-intersection detection (Self Crossing): enumerate the limited cases where a spiral path crosses itself.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 883 | [Projection Area of 3D Shapes](https://leetcode.com/problems/projection-area-of-3d-shapes/) | Easy | 2/10 | 76.0% | [ ] |
| 598 | [Range Addition II](https://leetcode.com/problems/range-addition-ii/) | Easy | 2/10 | 58.7% | [ ] |
| 812 | [Largest Triangle Area](https://leetcode.com/problems/largest-triangle-area/) | Easy | 3/10 | 71.6% | [ ] |
| 892 | [Surface Area of 3D Shapes](https://leetcode.com/problems/surface-area-of-3d-shapes/) | Easy | 3/10 | 70.7% | [ ] |
| 789 | [Escape The Ghosts](https://leetcode.com/problems/escape-the-ghosts/) | Medium | 4/10 | 63.7% | [ ] |
| 573 | [Squirrel Simulation](https://leetcode.com/problems/squirrel-simulation/) :lock: | Medium | 5/10 | 57.4% | [ ] |
| 2249 | [Count Lattice Points Inside a Circle](https://leetcode.com/problems/count-lattice-points-inside-a-circle/) | Medium | 5/10 | 56.7% | [ ] |
| 296 | [Best Meeting Point](https://leetcode.com/problems/best-meeting-point/) :lock: | Hard | 6/10 | 61.4% | [ ] |
| 469 | [Convex Polygon](https://leetcode.com/problems/convex-polygon/) :lock: | Medium | 6/10 | 40.2% | [ ] |
| 391 | [Perfect Rectangle](https://leetcode.com/problems/perfect-rectangle/) | Hard | 8/10 | 37.9% | [ ] |
| 149 | [Max Points on a Line](https://leetcode.com/problems/max-points-on-a-line/) | Hard | 8/10 | 30.7% | [ ] |
| 587 | [Erect the Fence](https://leetcode.com/problems/erect-the-fence/) | Hard | 9/10 | 53.0% | [ ] |
| 335 | [Self Crossing](https://leetcode.com/problems/self-crossing/) | Hard | 9/10 | 34.8% | [ ] |

## greedy_math

**What it is** — Greedy math problems ask you to optimize a numerical outcome (minimize cost, maximize value) by making locally optimal choices that can be justified mathematically — often through an invariant, a closed-form formula, or an insight that eliminates the need for dynamic programming. You recognize this pattern when a greedy choice (e.g., always pick the median, always break 3s from a number) can be proven to lead to the global optimum.

**Common steps**
1. Identify the quantity being optimized and what choices are available at each step.
2. Derive or recall the key mathematical insight (e.g., the median minimizes absolute deviation; breaking into 3s maximizes products).
3. Sort or preprocess the input if the greedy choice depends on relative ordering.
4. Apply the greedy strategy in a single pass or with a simple formula, avoiding unnecessary simulation.
5. Handle edge cases and boundary conditions (small inputs, remainders, off-by-one errors).

**Key variations**
- Median-based minimization (Minimum Moves to Equal Array Elements II, Minimum Operations to Make a Uni-Value Grid): sort the array, target the median value.
- Product maximization via factoring (Integer Break): break n into as many 3s as possible, adjusting for remainder.
- Game theory / parity arguments (Divisor Game, Stone Game IX): determine the winner from an invariant without simulating play.
- Digit manipulation (Maximum Swap, Find the Closest Palindrome): find the first position where swapping or adjusting a digit yields the largest improvement.
- Probability / expectation (Airplane Seat Assignment Probability): recognize the recursive structure collapses to a constant.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 908 | [Smallest Range I](https://leetcode.com/problems/smallest-range-i/) | Easy | 2/10 | 73.5% | [ ] |
| 1217 | [Minimum Cost to Move Chips to The Same Position](https://leetcode.com/problems/minimum-cost-to-move-chips-to-the-same-position/) | Easy | 2/10 | 72.9% | [ ] |
| 1025 | [Divisor Game](https://leetcode.com/problems/divisor-game/) | Easy | 2/10 | 71.8% | [ ] |
| 2396 | [Strictly Palindromic Number](https://leetcode.com/problems/strictly-palindromic-number/) | Medium | 3/10 | 90.3% | [ ] |
| 1884 | [Egg Drop With 2 Eggs and N Floors](https://leetcode.com/problems/egg-drop-with-2-eggs-and-n-floors/) | Medium | 4/10 | 74.8% | [ ] |
| 1227 | [Airplane Seat Assignment Probability](https://leetcode.com/problems/airplane-seat-assignment-probability/) | Medium | 4/10 | 67.4% | [ ] |
| 462 | [Minimum Moves to Equal Array Elements II](https://leetcode.com/problems/minimum-moves-to-equal-array-elements-ii/) | Medium | 4/10 | 61.9% | [ ] |
| 453 | [Minimum Moves to Equal Array Elements](https://leetcode.com/problems/minimum-moves-to-equal-array-elements/) | Medium | 4/10 | 58.7% | [ ] |
| 2591 | [Distribute Money to Maximum Children](https://leetcode.com/problems/distribute-money-to-maximum-children/) | Easy | 4/10 | 20.6% | [ ] |
| 1104 | [Path In Zigzag Labelled Binary Tree](https://leetcode.com/problems/path-in-zigzag-labelled-binary-tree/) | Medium | 5/10 | 75.7% | [ ] |
| 2033 | [Minimum Operations to Make a Uni-Value Grid](https://leetcode.com/problems/minimum-operations-to-make-a-uni-value-grid/) | Medium | 5/10 | 70.7% | [ ] |
| 553 | [Optimal Division](https://leetcode.com/problems/optimal-division/) | Medium | 5/10 | 63.0% | [ ] |
| 539 | [Minimum Time Difference](https://leetcode.com/problems/minimum-time-difference/) | Medium | 5/10 | 62.6% | [ ] |
| 343 | [Integer Break](https://leetcode.com/problems/integer-break/) | Medium | 5/10 | 62.3% | [ ] |
| 396 | [Rotate Function](https://leetcode.com/problems/rotate-function/) | Medium | 5/10 | 54.0% | [ ] |
| 670 | [Maximum Swap](https://leetcode.com/problems/maximum-swap/) | Medium | 5/10 | 52.0% | [ ] |
| 667 | [Beautiful Arrangement II](https://leetcode.com/problems/beautiful-arrangement-ii/) | Medium | 6/10 | 61.1% | [ ] |
| 754 | [Reach a Number](https://leetcode.com/problems/reach-a-number/) | Medium | 6/10 | 45.1% | [ ] |
| 2834 | [Find the Minimum Possible Sum of a Beautiful Array](https://leetcode.com/problems/find-the-minimum-possible-sum-of-a-beautiful-array/) | Medium | 6/10 | 35.0% | [ ] |
| 3649 | [Number of Perfect Pairs](https://leetcode.com/problems/number-of-perfect-pairs/) | Medium | 6/10 | 34.0% | [ ] |
| 899 | [Orderly Queue](https://leetcode.com/problems/orderly-queue/) | Hard | 7/10 | 67.0% | [ ] |
| 3495 | [Minimum Operations to Make Array Elements Zero](https://leetcode.com/problems/minimum-operations-to-make-array-elements-zero/) | Hard | 7/10 | 60.3% | [ ] |
| 1927 | [Sum Game](https://leetcode.com/problems/sum-game/) | Medium | 7/10 | 49.3% | [ ] |
| 2029 | [Stone Game IX](https://leetcode.com/problems/stone-game-ix/) | Medium | 8/10 | 30.2% | [ ] |
| 2005 | [Subtree Removal Game with Fibonacci Tree](https://leetcode.com/problems/subtree-removal-game-with-fibonacci-tree/) :lock: | Hard | 9/10 | 57.5% | [ ] |
| 1739 | [Building Boxes](https://leetcode.com/problems/building-boxes/) | Hard | 9/10 | 52.3% | [ ] |
| 564 | [Find the Closest Palindrome](https://leetcode.com/problems/find-the-closest-palindrome/) | Hard | 9/10 | 31.9% | [ ] |
| 3260 | [Find the Largest Palindrome Divisible by K](https://leetcode.com/problems/find-the-largest-palindrome-divisible-by-k/) | Hard | 10/10 | 17.0% | [ ] |

## modular_arithmetic

**What it is** — Modular arithmetic problems exploit the property that `(a * b) % m = ((a % m) * (b % m)) % m`, allowing you to compute results on very large numbers by tracking only their remainder. You recognize this pattern when the problem involves divisibility, large exponents, or asks whether a value is divisible by some modulus — often without computing the value explicitly.

**Common steps**
1. Identify the modulus `m` and the operation being performed (addition, multiplication, exponentiation).
2. Maintain a running remainder rather than the full value; update it with each digit or step.
3. For modular exponentiation, use fast exponentiation (repeated squaring): `pow(base, exp, mod)` in Python or implement it manually.
4. For "find the smallest N such that N % k == 0", recognize that remainders cycle and use early termination when a remainder repeats (pigeonhole principle guarantees a cycle of length at most k).
5. Apply the identity `(a - b) % m = (a % m - b % m + m) % m` to handle subtraction correctly.

**Key variations**
- Streaming remainder (Binary Prefix Divisible By 5): update remainder digit by digit as you read a binary string.
- Finding a specific remainder (Smallest Integer Divisible by K): track seen remainders to detect a cycle and conclude no solution exists.
- Modular exponentiation with large exponent arrays (Super Pow): apply the exponent digit by digit using `pow(a, b, mod)` properties.
- Units-digit patterns (Sum of Numbers With Units Digit K): count how many sums achieve the target units digit by analyzing the pattern mod 10.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1018 | [Binary Prefix Divisible By 5](https://leetcode.com/problems/binary-prefix-divisible-by-5/) | Easy | 3/10 | 53.7% | [ ] |
| 2598 | [Smallest Missing Non-negative Integer After Operations](https://leetcode.com/problems/smallest-missing-non-negative-integer-after-operations/) | Medium | 6/10 | 55.9% | [ ] |
| 1015 | [Smallest Integer Divisible by K](https://leetcode.com/problems/smallest-integer-divisible-by-k/) | Medium | 6/10 | 54.3% | [ ] |
| 372 | [Super Pow](https://leetcode.com/problems/super-pow/) | Medium | 6/10 | 36.9% | [ ] |
| 2310 | [Sum of Numbers With Units Digit K](https://leetcode.com/problems/sum-of-numbers-with-units-digit-k/) | Medium | 6/10 | 28.2% | [ ] |
| 1969 | [Minimum Non-Zero Product of the Array Elements](https://leetcode.com/problems/minimum-non-zero-product-of-the-array-elements/) | Medium | 7/10 | 37.6% | [ ] |

## number_theory

**What it is** — Number theory problems rely on properties of integers such as divisibility, prime factorization, and the greatest common divisor (GCD). You recognize this pattern when the problem involves primes, GCD/LCM relationships, coprimality, or asks questions that reduce to factoring or the Sieve of Eratosthenes.

**Common steps**
1. Determine whether the problem needs primes (use the Sieve of Eratosthenes for range queries), GCD (use Euclid's algorithm: `gcd(a, b) = gcd(b, a % b)`), or LCM (`lcm(a, b) = a * b // gcd(a, b)`).
2. For prime checking of a single number, trial-divide up to `sqrt(n)`.
3. For GCD-based problems, reduce fractions or group values by their GCD to find structure.
4. For problems involving pairs or subsets, look for GCD/LCM relationships that reduce the search space (e.g., two numbers whose GCD is 1 can make any sufficiently large integer — Chicken McNugget theorem).
5. Use the Sieve of Eratosthenes to precompute smallest prime factors for fast factorization across a range.
6. Apply inclusion-exclusion or Mobius inversion for advanced counting problems involving divisors.

**Key variations**
- Missing number via sum formula (Missing Number): use `n*(n+1)/2` or XOR — technically number theory but often grouped here.
- GCD of strings (Greatest Common Divisor of Strings): use Euclid's algorithm on lengths, then verify.
- Prime sieve (Count Primes, Most Frequent Prime): precompute with the Sieve; extend with smallest-prime-factor sieve for factorization.
- Fraction arithmetic (Fraction Addition and Subtraction, Simplified Fractions): always reduce fractions using GCD after each operation.
- Coprimality and Bezout's theorem (Water and Jug Problem): solvable iff the target is a multiple of `gcd(a, b)`.
- Divisor counting and GCD aggregation (Sorted GCD Pair Queries, Sum of Floored Pairs): precompute divisor frequencies and apply prefix sums for O(n log n) solutions.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 268 | [Missing Number](https://leetcode.com/problems/missing-number/) | Easy | 2/10 | 71.9% | [ ] |
| 1071 | [Greatest Common Divisor of Strings](https://leetcode.com/problems/greatest-common-divisor-of-strings/) | Easy | 2/10 | 53.7% | [ ] |
| 2614 | [Prime In Diagonal](https://leetcode.com/problems/prime-in-diagonal/) | Easy | 3/10 | 37.7% | [ ] |
| 914 | [X of a Kind in a Deck of Cards](https://leetcode.com/problems/x-of-a-kind-in-a-deck-of-cards/) | Easy | 3/10 | 30.3% | [ ] |
| 1447 | [Simplified Fractions](https://leetcode.com/problems/simplified-fractions/) | Medium | 4/10 | 69.8% | [ ] |
| 2979 | [Most Expensive Item That Can Not Be Bought](https://leetcode.com/problems/most-expensive-item-that-can-not-be-bought/) :lock: | Medium | 5/10 | 80.2% | [ ] |
| 592 | [Fraction Addition and Subtraction](https://leetcode.com/problems/fraction-addition-and-subtraction/) | Medium | 5/10 | 66.4% | [ ] |
| 869 | [Reordered Power of 2](https://leetcode.com/problems/reordered-power-of-2/) | Medium | 5/10 | 65.9% | [ ] |
| 2001 | [Number of Pairs of Interchangeable Rectangles](https://leetcode.com/problems/number-of-pairs-of-interchangeable-rectangles/) | Medium | 5/10 | 52.6% | [ ] |
| 365 | [Water and Jug Problem](https://leetcode.com/problems/water-and-jug-problem/) | Medium | 5/10 | 45.6% | [ ] |
| 204 | [Count Primes](https://leetcode.com/problems/count-primes/) | Medium | 5/10 | 36.0% | [ ] |
| 3044 | [Most Frequent Prime](https://leetcode.com/problems/most-frequent-prime/) | Medium | 6/10 | 46.0% | [ ] |
| 3012 | [Minimize Length of Array Using Operations](https://leetcode.com/problems/minimize-length-of-array-using-operations/) | Medium | 6/10 | 35.8% | [ ] |
| 625 | [Minimum Factorization](https://leetcode.com/problems/minimum-factorization/) :lock: | Medium | 6/10 | 34.0% | [ ] |
| 3867 | [Sum of GCD of Formed Pairs](https://leetcode.com/problems/sum-of-gcd-of-formed-pairs/) | Medium | 7/10 | 65.7% | [ ] |
| 2344 | [Minimum Deletions to Make Array Divisible](https://leetcode.com/problems/minimum-deletions-to-make-array-divisible/) | Hard | 7/10 | 61.3% | [ ] |
| 2607 | [Make K-Subarray Sums Equal](https://leetcode.com/problems/make-k-subarray-sums-equal/) | Medium | 7/10 | 38.5% | [ ] |
| 1201 | [Ugly Number III](https://leetcode.com/problems/ugly-number-iii/) | Medium | 7/10 | 31.4% | [ ] |
| 2941 | [Maximum GCD-Sum of a Subarray](https://leetcode.com/problems/maximum-gcd-sum-of-a-subarray/) :lock: | Hard | 8/10 | 38.4% | [ ] |
| 2183 | [Count Array Pairs Divisible by K](https://leetcode.com/problems/count-array-pairs-divisible-by-k/) | Hard | 8/10 | 30.7% | [ ] |
| 1862 | [Sum of Floored Pairs](https://leetcode.com/problems/sum-of-floored-pairs/) | Hard | 9/10 | 30.9% | [ ] |
| 3312 | [Sorted GCD Pair Queries](https://leetcode.com/problems/sorted-gcd-pair-queries/) | Hard | 10/10 | 22.9% | [ ] |

## combinatorics

**What it is** — Combinatorics problems ask you to count the number of ways to arrange, select, or partition objects — typically using formulas involving factorials, binomial coefficients, or multiplicative principles. You recognize this pattern when the answer is a count of configurations and the structure of the problem allows you to decompose it into independent choices or use a formula rather than enumerating all possibilities.

**Common steps**
1. Identify the combinatorial structure: is it permutations (ordered), combinations (unordered), or a product of independent choices?
2. Check whether the answer requires modular arithmetic (large outputs) and precompute factorials and modular inverses up to the needed range.
3. Use the multiplication rule: if choices at each step are independent, multiply the counts.
4. For "number of substrings/subarrays with property X", look for a contribution-by-position argument: for each element, count how many valid ranges include it.
5. Use Pascal's triangle (or `comb(n, k)`) for binomial coefficient lookups; use Stirling numbers or Catalan numbers if the structure matches.
6. Verify with small examples to confirm your formula handles edge cases (empty sets, single elements, all elements identical).

**Key variations**
- Contiguous run counting (Count Substrings with Only One Distinct Letter, Count Number of Homogenous Substrings): a run of length L contributes `L*(L+1)/2` substrings.
- Contribution per element (Vowels of All Substrings, Sum of Subsequence Widths): for each element, count how many subarrays/subsequences include it as the relevant element (first, last, or just any vowel).
- Permutation with constraints (Count All Valid Pickup and Delivery Options, Minimum Number of Operations to Make String Sorted): apply factorial math with inclusion-exclusion or modular inverses.
- Information-theoretic counting (Poor Pigs): model the problem as a base-B number where each pig encodes one digit across T rounds — answer is `ceil(log_B(buckets))` where `B = T + 1`.
- Exponential enumeration (Powerful Integers, Super Palindromes): enumerate bounded powers, collect results in a set to avoid duplicates.

| # | Problem | Difficulty | Score | Acceptance | Status |
|---|---------|------------|-------|------------|--------|
| 1180 | [Count Substrings with Only One Distinct Letter](https://leetcode.com/problems/count-substrings-with-only-one-distinct-letter/) :lock: | Easy | 2/10 | 80.9% | [ ] |
| 2083 | [Substrings That Begin and End With the Same Letter](https://leetcode.com/problems/substrings-that-begin-and-end-with-the-same-letter/) :lock: | Medium | 3/10 | 74.4% | [ ] |
| 2475 | [Number of Unequal Triplets in Array](https://leetcode.com/problems/number-of-unequal-triplets-in-array/) | Easy | 3/10 | 73.3% | [ ] |
| 1513 | [Number of Substrings With Only 1s](https://leetcode.com/problems/number-of-substrings-with-only-1s/) | Medium | 4/10 | 57.4% | [ ] |
| 1759 | [Count Number of Homogenous Substrings](https://leetcode.com/problems/count-number-of-homogenous-substrings/) | Medium | 4/10 | 57.4% | [ ] |
| 357 | [Count Numbers with Unique Digits](https://leetcode.com/problems/count-numbers-with-unique-digits/) | Medium | 5/10 | 55.6% | [ ] |
| 2063 | [Vowels of All Substrings](https://leetcode.com/problems/vowels-of-all-substrings/) | Medium | 5/10 | 55.4% | [ ] |
| 970 | [Powerful Integers](https://leetcode.com/problems/powerful-integers/) | Medium | 5/10 | 44.6% | [ ] |
| 2750 | [Ways to Split Array Into Good Subarrays](https://leetcode.com/problems/ways-to-split-array-into-good-subarrays/) | Medium | 6/10 | 35.0% | [ ] |
| 1573 | [Number of Ways to Split a String](https://leetcode.com/problems/number-of-ways-to-split-a-string/) | Medium | 6/10 | 34.6% | [ ] |
| 1359 | [Count All Valid Pickup and Delivery Options](https://leetcode.com/problems/count-all-valid-pickup-and-delivery-options/) | Hard | 7/10 | 64.9% | [ ] |
| 458 | [Poor Pigs](https://leetcode.com/problems/poor-pigs/) | Hard | 7/10 | 59.1% | [ ] |
| 1735 | [Count Ways to Make Array With Product](https://leetcode.com/problems/count-ways-to-make-array-with-product/) | Hard | 8/10 | 54.0% | [ ] |
| 1643 | [Kth Smallest Instructions](https://leetcode.com/problems/kth-smallest-instructions/) | Hard | 8/10 | 44.8% | [ ] |
| 891 | [Sum of Subsequence Widths](https://leetcode.com/problems/sum-of-subsequence-widths/) | Hard | 8/10 | 40.5% | [ ] |
| 906 | [Super Palindromes](https://leetcode.com/problems/super-palindromes/) | Hard | 8/10 | 40.0% | [ ] |
| 2681 | [Power of Heroes](https://leetcode.com/problems/power-of-heroes/) | Hard | 8/10 | 31.6% | [ ] |
| 2842 | [Count K-Subsequences of a String With Maximum Beauty](https://leetcode.com/problems/count-k-subsequences-of-a-string-with-maximum-beauty/) | Hard | 8/10 | 30.3% | [ ] |
| 3855 | [Sum of K-Digit Numbers in a Range](https://leetcode.com/problems/sum-of-k-digit-numbers-in-a-range/) | Hard | 9/10 | 50.7% | [ ] |
| 1830 | [Minimum Number of Operations to Make String Sorted](https://leetcode.com/problems/minimum-number-of-operations-to-make-string-sorted/) | Hard | 9/10 | 50.2% | [ ] |
