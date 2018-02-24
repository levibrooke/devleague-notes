Topic: Redux
Date: 2/22/18
***

slides: https://devleague.slides.com/devleague/redux/

links:
https://redux.js.org/

## Three Principles
- Single source of truth
- State is read-only
- Changes are made w/ pure functions

## Actions
- Payloads of information that send data from app to store.
- Send actions to the store using `store.dispatch()`

```javascript
const ADD_TODO = 'ADD_TODO'
{
  type: ADD_TODO,
  text: 'Build my first Redux app'
}
```

## Reducers
- Actions describe the fact that something happened, but doesn't specify how the app's state changes in response.
- Takes the payload off the action and return the state w/ payload applied.

## Store
- Store is the object that brings actions and reducers together.
- Responsibilities:
  - Holds application state
  - Allows access to 


## Data Flow 
- Redux architecture revolves around a strict unidirectional data flow.

### When adding redux to a react app...
`npm install --save redux react-redux`


