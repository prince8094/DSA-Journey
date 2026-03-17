# Prime Numbers

## Method 1: Brute Force
### Intuition
A number is prime if it has exactly two factors: 1 and itself. The simplest way is to count all divisors from 1 to $N$.

## Method 2: Optimal (Square Root Method)
### Intuition
As seen in my notes, factors always appear in pairs. If $N = 36$, and $4$ is a factor, then $36/4 = 9$ is also a factor. One factor in the pair is always $\le \sqrt{N}$.

### Implementation (C++)
```cpp
bool isPrimeBrute(int n) {
    int cnt = 0;
    for (int i = 1; i <= n; i++) {
        if (n % i == 0) cnt++; // **Checking every number up to N**
    }
    return (cnt == 2);
}

// Second approch
bool isPrimeOptimal(int n) {
    int cnt = 0;
    for (int i = 1; i * i <= n; i++) { // **Only iterate up to sqrt(N)**
        if (n % i == 0) {
            cnt++; 
            if ((n / i) != i) cnt++; // **Count the paired factor**
        }
    }
    return (cnt == 2);
}
