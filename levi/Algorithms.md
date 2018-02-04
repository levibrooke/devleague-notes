Topic: Algorithms
Date: 1/8/18
***

slides: http://devleague.slides.com/devleague/big-o

## Bubble sort 

```
let numbers = [4, 2, 1, 9, 3, 27, 12, 23];

function bubblesort(arr) {
  let swapped;

  // outer loop: check if any numbers were swampped
  do {
    // reset swapped value to false
    swapped = false;
    console.log('restarting');

    // iterate through array and swamp numbers as necessary
    for (let i = 0; i < arr.length - 1; i++) {
      console.log(arr);
      // check if left is greater than right
      if (arr[i] > arr[i+1]) {
        // set swapped to true because we are swapping numbers!
        swapped = true;

        // swap values
        let temp = arr[i];
        arr[i] = arr[i + 1];
        arr[i + 1] = temp;
      }
    }
  }
  while (swapped);
  return;
}

bubblesort(numbers);
```

## Big-O Notation

Stack Overflow - https://stackoverflow.com/questions/2307283/what-does-olog-n-mean-exactly

- Describes performance or complexity of an algorithm.
- Big O specifically describes the worst-case scenario.

O(1) - constant time
O(n) - linear time
O(n^2)
O(n^3)
O(n^n)
O(log n) - binary trees or binary search
O(2^n) - exponential time (fork bomb)

Call stack in CPU - has a finite amount of memory. It keeps track of where the processor is at in performing a function. If you have a Big O you can fill up the call stack (fork bomb).

## Sorting Algorithms

### Bubble sort

### Insertion 
