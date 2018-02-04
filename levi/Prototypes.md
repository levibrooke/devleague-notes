Topic: Prototypes in Javascript
Date: 1/12/18
***

slides: http://devleague.slides.com/devleague/prototypes-in-javascript

## First Class Functions
Languages that support first class functions:
- can create new functions rom pre-existing functions at run-time.
- store functions in collections.
- use functions as arguments to other functions.
- use functions as return values of other functions.

## Know these words and why they are different
- Class/function - a class is a template (technically it's just a function and an object).
- Object - a structure that stores data in key:value pairs.
- Instance - creation of a new object from a template (class).

# What are Prototypes
- Prototypes are just functions
    - `new` keywod is what depicts the difference b/t just a function and a constructor.
- Prototypes are singular
- Every object has a prototype

```javascript
function Song() {
    this.title = "";
    this.artist = "";
    
    this.prototype.play = function() {
        console.log("play");
    }
}

let song = new Song(); // using new keyword, call class
```

## The Prototype Inheritance Chain
- All objects that inherit from another object receive all prototype properties from all objects up the chain (i.e. from the parent objects).
- hasOwnProperty() will tell you if the method is defined on the current object or inherited.