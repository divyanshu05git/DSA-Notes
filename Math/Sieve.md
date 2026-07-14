# Sieve of Eratosthenes

## Complexity

- Time: O(n log log n)
- Space: O(n)

## Java Implementation

```java
import java.util.Arrays;

public class Sieve {

    public static boolean[] sieve(int n) {
        boolean[] prime = new boolean[n + 1];
        Arrays.fill(prime, true);

        if (n >= 0) prime[0] = false;
        if (n >= 1) prime[1] = false;

        for (int i = 2; i * i <= n; i++) {
            if (prime[i]) {
                for (int j = i * i; j <= n; j += i) {
                    prime[j] = false;
                }
            }
        }

        return prime;
    }
}
```

## Applications

- Checking primality in O(1)
- Prime counting
- DP on prime numbers
- Number theory problems
- Factorization preprocessing
