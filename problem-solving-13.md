> Problem Solving - 13

# Lefted things from Mathematics to LinkedList - I

## Mathematics

### Prime factors

```
void primeFactors(int n){
    if(n <= 1)
        return;
    
    while(n%2 == 0){
        print(2);
        n /= 2;
    }
    
    while(n%3 == 0){
        print(3);
        n /= 3;
    }
    
    for(int i = 5;i*i<=n;i = i+6){
        while(n%i == 0){
            print(i);
            n /= i;
        }
        
        while(n%(i+2) == 0){
            print(i+2);
            n /= (i+2);
        }
    }
    
    if(i > 3)
        print(n);
}
```

### All divisors of a number

```
void printDivisors(int num) { //print divisors in sorted order
    int i;
    for(i = 1;i*i<n;i++)
        if(n%i == 0)
            print(i);

    for(;i>=1;i--)
        if(n%i == 0)
            print(n/i);
}
```

### Sieve of Eratosthenes

```
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;

class GFG {

	
	static void sieve(int n)
	{
		if(n <= 1)
			return;

		boolean isPrime[] = new boolean[n+1];

		Arrays.fill(isPrime, true);

		for(int i=2; i*i <= n; i++)
		{
			if(isPrime[i])
			{
				for(int j = 2*i; j <= n; j = j+i)
				{
					isPrime[j] = false;
				}
			}
		}

		for(int i = 2; i<=n; i++)
		{
			if(isPrime[i])
				System.out.print(i+" ");
		}
	}

	public static void main (String[] args) {
		
		int n = 18;

		sieve(n);

	}
}
```

### Finding digits in n factorial

```
class Solution{
    public int digitsInFactorial(int n){
        
    double digits = 0;
    
    for(int i = 1;i<=n;i++){
        digits += Math.log10(i);
    }
    
    return ((int)Math.floor(digits) + 1);
    
    }
}
```

```
n factorial can be written as n * (n-1) * ... 1;
digits in the number n will be Math.floor(log10(n))+1.
Digirs in the number n! will be Math.floor(log10(n*(n-1) ... 1)+1. 
according to log(AB) = log(A) + log(B) principle, we derived the above solution
```

