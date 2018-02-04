Topic: Object Oriented Programming
Date: 1/11/18
***
slides: http://devleague.slides.com/devleague/es6-oop

## Why OOP?

- Organize code
- Easier to conceptualize how code relates
- Promotes DRY (don't repeat yourself)
- Promotes encapsulation


Inheritance
- Classes can have child classes that automatically have access to the properties of the parent.

Encapsulation
- Classes allow you to control the access to any properties contained inside.

Polymorphism
- Child class has ability to overwrite methods in a parent.

## Objects
- Holds state through properties.
- Can perform actions through methods.
- Constructor methods: functions
- Accessor methods: functions that accesss a property

## Creating Objects
- Use the `new` keyword to create an instance.
- The `constructor` method is invoked on creation.
- Constructor arguments can be passed in.
- __Classes cannot be invoked like normal functions.__

## Instance Properties
- Assign classes to variables.

## Accessor Methods
- Access properties through getter and setter methods.
- Assigning a new property to an object will implicity invoke it's `set` accessor method.

## Checking Instance Type
- You can use this to make sure the new instance of a class matches.
- Ex:
```javascript
var ed = new Person();
ed instanceof Person // true
```
