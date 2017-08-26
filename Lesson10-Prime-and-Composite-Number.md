# Lesson10 Prime and Composite Number

## MinPrimeterRectangle

Very easy, simply loop through all the numbers less than or equal to the square root of the give area(N), since the length and width comes up in pairs and for the length/width smaller than square root of N, we will have its coresponding length/width bigger than square root of N. Sowe can simply loop throught every number from 1 to square root of N(if it is not integer we will take the ceiling value) which gives as the time compexity as question required. During the process we will calculate the perimeter only if N is divisible by `i` and compare it with our stored the `minPerim` value, and change its current value to `minPerim` if the current value is bigger than the previously stored one.

In essence it is sort of like the question of finding all the factors of a given integer.

```javascript
function solution(N) {
    var minPerim = Infinity;
    var curPerim;
    for (var i = 1; i < Math.sqrt(N) + 1; i++) {
        if (N % i === 0) {
            curPerim = (i + (N/i))*2
        }
        if (curPerim < minPerim) {
            minPerim = curPerim;
        }
    }
    return minPerim;
}
```

## CountFactors
Very similar to the previous question. 

```javascript
function solution(N) {
    var counter = 0;
    // loop through all the element smaller than square root of N
    for (var i = 1; i < Math.sqrt(N); i++) {
        if(N%i === 0) {
            counter += 2;
        }
    }
    // check if the value of the square root of N is Integer
    if (Math.sqrt(N) === parseInt(Math.sqrt(N))) {// This is the method to check integer in JavaScript
        counter += 1;
    }
    return counter;
}
```
## Peaks(Need further notice)

A Harder Problem. 

```javascript
function solution(A) {
    var storage = [], counter = 0;
    // 1. So first I used a loop to find all the peaks and stored them all into an array called storage
    for(var i = 1; i < A.length - 1; i++) {
        if (A[i] > A[i-1] && A[i] > A[i+1]) {
            storage.push(i);
        }
    }
    // 2. Go and write the function canBeSeparatedInto
    // 3. Use the for loop to check the counter
    for(var j = 1; j < A.length; j++) {
        if (canBeSeparatedInto(j, A, storage)) {
            counter = j;
        }
    }
    return counter;
}

/* this function basically tells you if it is possible to divide the given array into given parts
 * we will be passing our function with parameters: 
 * @param parts[number]: number of parts that we intend to divide the array into
 * @param array[array]: the original array
 * @param peaks[array]: an storage array that store all the index of the peaks
 * @return [boolean]: true if the given array can be divided into given parts, false otherwise
 */
function canBeSeparatedInto(parts, array, peaks) {
    var i = 1, result = false;
    var blockSize = array.length / parts;
    peaks.forEach(function(elem) {
    // test to see if there is an element in the array belongs to the ith part
        if ((elem+1)/blockSize <= i && (elem+1)/blockSize> i-1) {
            i++;
        }
    });
    // set the result to true if there are indeed peaks for every parts
    if (i > parts) {
        result = true;
    }
    return result;
}

```
As you can see this is not the correct answer, I only get 45% in the codility, but I noted it down anyway.

## Flags

