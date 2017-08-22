# Lesson10 Prime and Composite Number

## MinPrimeterRectangle

Very easy, just simply loop through all the numbers less than or equal to the square root of the give area(N), since the length and width comes up in pairs and for the length/width smaller than square root of N, we will have its coresponding length/width bigger than square root of N. Sowe can simply loop throught every number from 1 to square root of N(if it is not integer we will take the ceiling value) which gives as the time compexity as question required. During the process we will calculate the perimeter only if N is divisible by `i` and compare it with our stored the `minPerim` value, and change its current value to `minPerim` if the current value is bigger than the previously stored one.

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
