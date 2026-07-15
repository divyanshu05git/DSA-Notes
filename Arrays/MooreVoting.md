# Moore's Voting Algorithm

## Problem

Find the element that appears **more than `n/2` times** in an array.

If the problem does **not** guarantee the existence of such an element, perform a second pass to verify the candidate.

---

## Key Observation

If an element occurs more than `n/2` times, then it cannot be completely canceled by all the remaining elements.

Think of repeatedly removing pairs of **different** elements.

The majority element will always survive.

---

## Intuition

Example:

```
2 2 1 1 1 2 2
```

Cancel different pairs:

```
2 1
2 1
```

Remaining:

```
1 2 2
```

Again,

```
1 2
```

Remaining:

```
2
```

The majority element always remains.

---

## Algorithm

Maintain two variables:

- `candidate`
- `count`

Initially

```java
candidate = 0;
count = 0;
```

Traverse the array.

- If `count == 0`, make the current element the new candidate.
- If the current element equals the candidate, increment `count`.
- Otherwise, decrement `count`.

---

## Java Implementation

```java
public int majorityElement(int[] nums) {

    int candidate = 0;
    int count = 0;

    for (int x : nums) {

        if (count == 0) {
            candidate = x;
            count = 1;
        }
        else if (candidate == x) {
            count++;
        }
        else {
            count--;
        }
    }

    return candidate;
}
```

---

## Verification Step (If Majority Is Not Guaranteed)

```java
int freq = 0;

for (int x : nums) {
    if (x == candidate)
        freq++;
}

return freq > nums.length / 2 ? candidate : -1;
```

---

## Why It Works

Whenever we encounter

- one occurrence of the candidate, and
- one occurrence of a different element,

they cancel each other.

Since the majority element appears **more than all the remaining elements combined**, it can never be completely canceled.

Hence, the final candidate must be the majority element.

---

## Complexity

- **Time:** `O(n)`
- **Space:** `O(1)`

---

# Extension: Majority Element II

Find all elements appearing more than

```
n / 3
```

times.

### Observation

There can be **at most two** such elements.

Maintain

- `candidate1`
- `candidate2`
- `count1`
- `count2`

After one pass, verify both candidates.

**Complexity**

- Time: `O(n)`
- Space: `O(1)`

---

# Generalization

Find all elements occurring more than

```
n / k
```

times.

### Observation

There can be at most

```
k - 1
```

such elements.

Maintain

- `k - 1` candidates
- `k - 1` counts

Verify all candidates in a second pass.

---

# Common Problems

- LeetCode 169 — Majority Element
- LeetCode 229 — Majority Element II
- Majority Element (> n/k)
- Streaming Majority Element

---

# Template

```java
int candidate = 0;
int count = 0;

for (int x : nums) {

    if (count == 0) {
        candidate = x;
        count = 1;
    }
    else if (candidate == x) {
        count++;
    }
    else {
        count--;
    }
}

// Verify if the problem does not guarantee a majority.
```

---

## Takeaway

> **Moore's Voting Algorithm works because every occurrence of a non-majority element can cancel at most one occurrence of the majority element, but the majority element still has occurrences left over.**
