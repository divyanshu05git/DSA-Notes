## Partition DP

State

dp(i) = answer for suffix starting at i

Transition

```java

for(j=i;j<n;j++){
    maintain property

    if(valid)
        ans = combine(ans, dp(j+1))
}

```

Problems
- LC 2478
- Minimum Beautiful Substrings
- Equal Frequency Partition
- Meals Problem
