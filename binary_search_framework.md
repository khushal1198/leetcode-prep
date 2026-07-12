# Binary Search Framework

**Universal core:** every binary search = *look at `mid`, decide which half to discard, repeat.*
What changes between problems is only the **decision rule**. There are 3 families.

---

## The 3 families

### Flavor 1 — Exact search
"Does `target` exist / where is it?" in a sorted array. `mid == target` means **done**.
```python
if nums[mid] == target: return mid
elif nums[mid] < target: left = mid + 1
else: right = mid - 1
```

### Flavor 2 — Boundary / predicate search  ← the framework (most common, trickiest)
"Find the **first / last / min / max** value that satisfies a condition."

> **Is `mid` valid? → record it, move toward a *better* one.
> Not valid? → move toward where valid ones live.**

- Record with a `result` var; keep going in the "better" direction (record-and-keep-going).
- The last recorded value is the answer. No boundary special-cases needed.
- "Better" direction is the ONLY thing that changes per problem (left for first, right for last, smaller for "min that works," larger for "largest ≤ query").

```python
result = -1
while left <= right:
    mid = (left + right) // 2
    if is_valid(mid):          # candidate
        result = mid
        # move toward BETTER: right = mid-1 (leftward) OR left = mid+1 (rightward)
    elif too_small:
        left = mid + 1
    else:
        right = mid - 1
return result
```

### Flavor 3 — Rotated / "which half is sorted"
Decision rule isn't a validity predicate — it's *"which half is sorted, and could the answer be there?"*
```python
if nums[mid] > nums[right]: left = mid + 1   # (Find Min) answer in right half
else: right = mid                            # answer in left half (incl. mid)
```

---

## How to pick the flavor — ask "what am I asking at `mid`?"
- "Is this *the* element?" → **Flavor 1** (exact)
- "Is this a valid candidate, and could a better one exist?" → **Flavor 2** (boundary/predicate)
- "Which side is sorted / which side holds the answer?" → **Flavor 3** (rotated/peak/converge)

---

## The 2 mechanical templates (family → template)

**Template A** — `while left <= right`, move `mid ± 1`, use a `result` var, `return result`.
```python
while left <= right:
    mid = (left + right) // 2
    if valid(mid):
        result = mid
        # move toward better: right = mid-1  OR  left = mid+1
    elif too_small: left = mid + 1
    else: right = mid - 1
return result
```

**Template B** — `while left < right`, move `left = mid+1` / `right = mid` (NOT mid-1), `return left`.
```python
while left < right:
    mid = (left + right) // 2
    if go_right(mid): left = mid + 1
    else: right = mid      # keep mid — it might BE the answer
return left                # left == right = the answer
```
Template B's `left < right` guarantees `mid+1` is in bounds → no boundary guards needed.

| Family | Template | Decision at `mid` |
|---|---|---|
| 1. Exact | A | `mid == target` → return |
| 2. Boundary/predicate | A | valid? → record + move toward better |
| 3. Rotated / peak / converge | **B** | which side holds the answer → move there |

**The don't-think procedure:** (1) name the family by the question at `mid`, (2) grab its template, (3) fill in the one decision rule.

---

## Problem log (tag every binary-search problem with its family)

| # | Problem | Family | "Valid / decision rule" | Better direction |
|---|---------|--------|-------------------------|------------------|
| 704 | Binary Search | 1 exact | `nums[mid] == target` | — |
| 35 | Search Insert Position | 2 boundary | first index with `nums[mid] >= target` | left |
| 33 | Search in Rotated Sorted Array | 3 rotated | which half is sorted, is target in it | — |
| 153 | Find Min in Rotated Array | 3 rotated | `nums[mid]` vs `nums[right]` | toward smaller |
| 875 | Koko Eating Bananas | 2 boundary (on answer) | speed finishes in ≤ h hours | smaller (min that works) |
| 981 | Time Based Key-Value Store | 2 boundary | `timestamp[mid] <= query` | larger (largest ≤ query) |
| 34 | Find First and Last Position | 2 boundary | `nums[mid] == target` | first→left, last→right |
| 162 | Find Peak Element | 3 converge (Template B) | `nums[mid] < nums[mid+1]`? uphill→right, else `right=mid` | toward higher neighbor |
