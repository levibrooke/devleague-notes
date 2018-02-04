Topic: This
Date: 1/10/18
***
slides: http://devleague.slides.com/devleague/like-this-and-like-that

_this_ refers to the object which the current function is associated or belongs to.


## Example
```javascript
let person = {
  firstName: '',
  lastName: '',
  fullName: function() {
    return this.firstName + ' ' + this.lastName; 
  }
};
person.firstName = 'Ed';
person.lastName = 'Kim';
console.log(person.fullName());
```