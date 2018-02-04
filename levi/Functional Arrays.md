Topic: Functional Arrays
Date: 1/9/18
***
slides: http://devleague.slides.com/devleague/functional-arrays/

## Classes of array methods:
- Mutator methods - those that change the structure of an array
- Accessor methods - those that access the contents without changing it
- Iterator methods - those that iterate over the array

## forEach(callback[, arg])
Calls a function you provide for each element in the array. Callback function takes 3 params: 
- element - current element being iterated over
- index - current index of the element in array
- array - the array itself

```javascript
let myArray = [1, 2, 3];

function log(element, index, array) {
    console.log("Current element is " + element);
}

myArray.forEach(log);
```

## every(callback[, arg])
Returns true (boolean) if _every element_ in array passes the test you provide. Takes 3 params:
- element
- index
- array

## some(callback[, arg])
Returns true (boolean) if _any element_ in the array passes the test you provide. Takes 3 params:
- element
- index
- array

## filter(callback[, arg])
Returns a boolean that when true returns new array w/ all elements that pass true test (i.e. you're filtering out everything that doesn't pass the test). Takes 3 params:
- element
- index
- array

```javascript
// filter

const numbersArray = [2343, 23, 7654, 12, 'f45', 10, 'a665'];

const validNumbers = numbersArray.filter(function (element) {
  return !isNaN(parseInt(element));
});

if (validNumbers.length) {
}
console.log('Valid numbers: ', validNumbers);
```

## map(callback[, arg])
Creates / returns new array w/ all returned values from callback function.

## reduce(callback[, initalValue])
Returns a single value accumulated againsta all values from callback. Takes 4 params and 1 optional param:
- previousValue
- currentValue
- index
- array

initialValue is optional param to the reduce method.

*reduce() does not mutate the original array*

