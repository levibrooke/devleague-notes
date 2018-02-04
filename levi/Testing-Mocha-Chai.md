Topic: Testing w/ Mocha & Chai
Date: 1/19/18
***
slides: http://devleague.slides.com/devleague/mocha-chai

## Test Driven Development
- Write tests first, then you write code.
- Forces you to think about how you will use the code before you implement it.

## Red, Green, Refactor
![Screen Shot 2018-01-19 at 10.53.33 AM.png](/:storage/0.3azvnh03pep.png)

## Common pitfalls
- Forgetting to run tests frequently
- Writing too many tests at once
- Writing tests that are too large
- Writing overly trivial tests

## Mocha
- Javascript testing framework that runs on both node and in the browser.

### Two Important functions
- `describe()` - groups test cases into test suites.
- `it()` - individual test cases

### Hooks
- Allows you to set up both the state before and after you tests run.

```javascript
describe('hooks', function() {

  before(function() {
    // do this before all the it tests
  });
  afterEach(function() {
    // do this after each it test case
  });
  beforeEach(function() {
    // do this before each it test case
  });
  after(function() {
    // do this after all the it tests
  });
});
```

### Skipping Tests
- Use skip keyword: `it.skip('should be...');`

### File watcher support
- `$ mocha --watch`
- Automatically runs tests whenever a file is changed.

## Chai
docs - http://chaijs.com/api/bdd/

- An assertion library for node and the browser that can be paired w/ any Javascript testing framework.

### Should interface
- Extends each object w/ a `should` property to start your assertion chain.
- Should is a property on the object, while expect is a function that gets invoked.

### Expect interface
- `expect()` starts the assertion chain.
- Is a function.
- Epect works on values that may be undefined. Should does not.