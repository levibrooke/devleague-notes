Topic: Apply, Bind, Call
Date: 1/10/18
***
slides: http://devleague.slides.com/devleague/call-apply-bind-oh-my

## call()
- Takes in the arguments the traditional way.
- First argument sets the context (_this_).


## apply()
- Takes in an array of arguments.
- First argument sets the context (_this_).

## bind()
- Binds a function to an element to be executed on a future event (click, hover, etc...).
- Takes in arguments the traditional way.
- Sets the context on a permanent basis.
- Allows you to call the function anywhere and it'll still have the bound context.

```javascript
function createVehicle(type, engine) {
  console.log(arguments);
  return this.brand + ' ' + type + ' ' + engine;
}

let subaru = { brand: 'subaru' };

let createCar = createVehicle.bind(subaru);
console.log(createCar('car', 'flat 6'));

let createCar2 = createVehicle.bind(subaru, 'sports car');
console.log(createCar2('v6'));
```


## Utility to convert arguments into an array

```javascript
let args = Array.prototype.slice.call(arguments);
```