# Segment Tree

## Definition

A **Segment Tree** is a binary tree data structure used to efficiently answer **range queries** and perform **point/range updates** on an array.

It is mainly used when:

- Frequent updates are performed on the array.
- Multiple range queries need to be answered efficiently.

---

# Applications

- Range Sum Query
- Range Minimum Query (RMQ)
- Range Maximum Query
- GCD of a Range
- XOR of a Range
- Range Updates (with Lazy Propagation)

---

# Structure

For an array

```
[2, 5, 1, 4]
```

Segment Tree

```
                12
              /    \
             7      5
           /  \    / \
          2    5  1   4
```

Each node stores information about a segment.

Example:

```
Root -> [0...3]
Left -> [0...1]
Right -> [2...3]
```

---

# Array Representation

Instead of building an actual tree, store it in an array.

```
Root = 0

Left Child  = 2*i + 1
Right Child = 2*i + 2
```

Example

```
Index

0
├──1
│  ├──3
│  └──4
└──2
   ├──5
   └──6
```

---

# Tree Size

Allocate

```java
int segTree[] = new int[4 * n];
```

`4*n` is sufficient for all cases.

---

# Build Tree

### Recurrence

```
Leaf:
tree[node] = arr[index]

Internal Node:
tree[node] =
merge(leftChild, rightChild)
```

For Range Sum

```
merge = +
```

### Java

```java
void build(int node,int l,int r){

    if(l==r){
        segTree[node]=arr[l];
        return;
    }

    int mid=l+(r-l)/2;

    build(2*node+1,l,mid);
    build(2*node+2,mid+1,r);

    segTree[node]=
        segTree[2*node+1]
        +segTree[2*node+2];
}
```

---

# Point Update

Update one index.

Example

```
arr[5]=10
```

Only nodes containing index 5 are updated.

### Java

```java
void update(int idx,int val,int node,int l,int r){

    if(l==r){
        segTree[node]=val;
        return;
    }

    int mid=l+(r-l)/2;

    if(idx<=mid)
        update(idx,val,2*node+1,l,mid);
    else
        update(idx,val,2*node+2,mid+1,r);

    segTree[node]=
        segTree[2*node+1]
        +segTree[2*node+2];
}
```

---

# Range Query

Find

```
Query(left,right)
```

There are three cases.

---

## 1. No Overlap

```
Current Segment

|------|

Query

              |------|
```

Return

```
Identity Element
```

For

- Sum → 0
- Min → +∞
- Max → -∞
- GCD → 0

```java
return 0;
```

---

## 2. Complete Overlap

```
Current Segment

|--------------|

Query

   |------|
```

Return stored value.

```java
return segTree[node];
```

---

## 3. Partial Overlap

Split into both children.

```java
leftAnswer
+
rightAnswer
```

### Java

```java
int query(int ql,int qr,int node,int l,int r){

    if(qr<l || ql>r)
        return 0;

    if(ql<=l && r<=qr)
        return segTree[node];

    int mid=l+(r-l)/2;

    return query(ql,qr,2*node+1,l,mid)
         + query(ql,qr,2*node+2,mid+1,r);
}
```

---

# Complexity

| Operation | Time |
|-----------|------|
| Build | **O(n)** |
| Point Update | **O(log n)** |
| Range Query | **O(log n)** |
| Space | **O(4n)** ≈ **O(n)** |

---

# Why Build is O(n)?

Although the tree has height `log n`, every node is visited exactly once.

A Segment Tree has at most

```
2n-1
```

nodes.

Hence,

```
O(2n)=O(n)
```

---

# Why Query is O(log n)?

At every level,

- only a constant number of nodes are explored.
- height of tree is `log n`.

Therefore

```
O(log n)
```

---

# Generic Merge Function

Instead of storing only sums,

replace

```java
tree[node]=left+right;
```

with

```java
tree[node]=merge(left,right);
```

Examples

| Query | Merge |
|--------|--------|
| Sum | + |
| Min | Math.min |
| Max | Math.max |
| GCD | gcd |
| XOR | ^ |

---

# Segment Tree Template

```java
build(node,l,r)

if(l==r)
    return

mid=(l+r)/2

build(left)
build(right)

tree[node]=merge(left,right)
```

---

# Update Template

```java
update(idx,val,node,l,r)

if(l==r){
    tree[node]=val;
    return;
}

if(idx<=mid)
    go left
else
    go right

tree[node]=merge(left,right)
```

---

# Query Template

```java
query(ql,qr,node,l,r)

No Overlap
    return identity

Complete Overlap
    return tree[node]

Partial Overlap
    return merge(left,right)
```

---

# Identity Elements

| Operation | Identity |
|------------|----------|
| Sum | 0 |
| Product | 1 |
| Minimum | +∞ |
| Maximum | -∞ |
| XOR | 0 |
| GCD | 0 |

---




