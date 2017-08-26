# Lesson 11 Sieve of Eratosthenes
Sieve of Eratosthenes is an algorithm to find the prime number within a given range, below is it's JavaScript Implementation:
```javascript
/*
 * @param upperbound{number} the upperbound for the number range
 * @return {array} an array contains boolean value, for an array like 
 * [,,ture,ture, false, ...], it means 2 is prime, 3 is prime, 4 is not prime 
 */
function sieve(upperbound) {
	var isPrimes = [], index = 2, k; //initiate the array
	isPrimes[2] = true;
	while (index < upperbound) {
		if (isPrimes[index] !== false) {
			isPrimes[index] = true;
		}
		k = index*index;
		while(k < upperbound) {
			isPrimes[k] = false;
			k += index;
		}
		index++;
	}
}
```

## CountSemiprimes

```javascript
function solution(N, P, Q) {
    // write your code in JavaScript (Node.js 6.4.0)
    var isPrime = [], primes = [];
    isPrime[2] = true;
    var index = 2, k;
    while(index <= N/2) {//don't need to get to N, N/2 is enough since a number bigger than N/2 times 2 will be bigger than N, which is beyond our range
        if(isPrime[index] !== false) {
            isPrime[index] = true
        }
        k = index * index;
        while(k <= N) {
            isPrime[k] = false;
            k += index;
        }
        index++;
    }
    
    isPrime.forEach(function(elem, idx) {
        if (elem === true) {
            primes.push(idx);
        }
    });
    
    var semiPrimes = [];
    for (var i = 0; i < primes.length; i++){
        for (var j = i; j < primes.length; j++) {
            var product = primes[i]*primes[j];
            if (semiPrimes.indexOf(product) === -1 && product <= N) {
                semiPrimes.push(primes[i]*primes[j]);
            }
            if (product > N) {
                break;
            }
        }
    }
    
    var semiCounts = []
    for (var idx = 0; idx< P.length; idx++) {
        semiCounts.push(countElementWithin(semiPrimes, P[idx], Q[idx]))
    }
    
    return semiCounts;   
}

function countElementWithin(array, lower, upper) {
    var counter = 0;
    array.forEach(function(elem) {
        if (elem >=lower && elem <= upper) {
            counter++;
        }
    });
    return counter;
}
```

The correctness is 100%, but the performance is only 20%. So more work needs to be done!
