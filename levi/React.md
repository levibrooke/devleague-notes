Topic: React
Date: 2/20/18
***

slides: http://devleague.slides.com/devleague/reactjs

## What is React?
- Component based library from Facebook
- Only handles front-end UI
- Different from angularJS dirty checking in that it handles updates with virtual DOM diffs.
- Component heirarchy of data flows downwards to children. (see Prop)

## Setting up
- react (core)
- react-dom (render components to DOM)
- babel (to transpile es6 to es5)

## Creating Components
- We can extend the React.Component class
```javascript
class SimpleComponent extends React.Component {
  // render() is required and will only return one element
  render() {
    return (
      React.createElement('h1', {className: 'hello'}, 'Hello React!!')
      );
  }
}
```
- React-dom gives us the render() method

## JSX
- XML language that looks like Javascript but is not
- You can only return one parent element, any number of children though.

## Props
- React uses props to pass values from the parent component to its children.
- this.props.data
- this.props.children

## Component State
- Setting the *state* object allows us to store values in memory on the component that we can use or pass to children.


## PropTypes & Refs
https://reactjs.org/docs/typechecking-with-proptypes.html
https://reactjs.org/docs/refs-and-the-dom.html