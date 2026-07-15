# Comparing Very Large Numbers Stored as Strings (Java)

## Problem

When numbers are too large to fit into `int` or `long`, we cannot convert them into primitive data types for comparison or sorting.

Example:

```text
999999999999999999999999999999999999999
```

Instead, store the numbers as **Strings**.

---

# Does `String.compareTo()` Convert Strings to Integers?

**No.**

`compareTo()` compares strings **character by character** based on their Unicode values.

Example:

```java
System.out.println("123".compareTo("124")); // Negative
```

Comparison:

```text
1 == 1
2 == 2
3 < 4
```

Hence,

```text
123 < 124
```

---

# Why Can't We Directly Use `compareTo()`?

Consider:

```java
"100".compareTo("20");
```

Character comparison:

```text
1 < 2
```

So Java thinks:

```text
"100" < "20"
```

But numerically:

```text
100 > 20
```

Therefore,

> **`compareTo()` alone does NOT compare numbers correctly.**

---

# Correct Way to Compare Large Numbers

## Step 1: Remove Leading Zeros

Examples:

```text
00123  -> 123
00045  -> 45
00000  -> 0
```

If every character is `0`, store the number as `"0"`.

---

## Step 2: Compare Lengths

After removing leading zeros:

- More digits ⇒ Larger number

Example:

```text
99   (Length = 2)
100  (Length = 3)

100 > 99
```

---

## Step 3: If Lengths Are Equal

Use `compareTo()`.

Example:

```text
4567
8921
```

Comparison:

```text
4 < 8
```

Therefore,

```text
4567 < 8921
```

This is also numerically correct.

### Why does this work?

If two numbers have the **same number of digits**, lexicographical order and numerical order are identical.

Examples:

```text
12345 < 12346
54321 > 12345
99999 > 88888
```

---

# Java Comparator

```java
Collections.sort(list, (a, b) -> {
    if (a.length() != b.length())
        return a.length() - b.length();

    return a.compareTo(b);
});
```

---

# Time Complexity

Let:

- `N` = Number of extracted numbers
- `L` = Maximum number of digits

Comparison:

- Length comparison → **O(1)**
- `compareTo()` → **O(L)**

Sorting:

```text
O(N log N × L)
```

---

# Interview Tips

Whenever numbers can be arbitrarily large:

 Store them as `String`

 Remove leading zeros

 Compare lengths first

Use `compareTo()` only when lengths are equal

Avoid converting to:

- `int`
- `long`

unless the constraints explicitly guarantee they are sufficient.

---

# Key Takeaway

For large numeric strings:

```text
If length differs:
    Larger length ⇒ Larger number

Else:
    Use compareTo()
```

This technique is commonly used in OA and interview questions from companies like Amazon, Flipkart, Microsoft, Google, and Adobe when dealing with extremely large integers.
