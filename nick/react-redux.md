# REACT REDUX

https://github.com/happypoulp/redux-tutorial
(put together a shortened version of this ^^ repo tutorial)
*Flux*:
-is the application architecture that Facebook uses for building client-side web applications. It complements React's composable view components by utilizing a unidirectional data flow. It's more of a pattern rather than a formal framework, and you can start using Flux immediately without a lot of new code.
https://facebook.github.io/flux/img/flux-simple-f8-diagram-with-client-action-1300w.png

Web aplications are made of:
 1) Templates / html = View
 2) Data that will populate our views = Models
 3) Logic to retrieve data, glue all views together and to react accordingly to user events,
    data modifications, etc. = Controller

 This is the very classic MVC that we all know about. But it actually looks like concepts of flux,
 just expressed in a slightly different way:
 - Models look like stores
 - user events, data modifications and their handlers look like
   "action creators" -> action -> dispatcher -> callback
 - Views look like React views (or anything else as far as flux is concerned)
  instead of having handlers for those
 actions directly modify Models or Views, flux ensures all actions go first through something called
 a dispatcher, then through our stores, and finally all watchers of stores are notified.
 ________________________
 **SIMPLE ACTION CREATOR**
 action creator is just a function...
 
    var actionCreator = function() {
      return {
          type: 'AN_ACTION'
      }
    }

...that creates an action (yeah, the name action creator is pretty obvious now) and returns it

 However, one thing to note is the format of the action. This is kind of a convention in flux
 that the action is an object that contains a "type" property. This type allows for further
 handling of the action. Of course, the action can also contain other properties to
 pass any data you want.
 
  We can call this action creator and get an action as expected:
  
    console.log(actionCreator())

 Output: { type: 'AN_ACTION' }
 
 Read more about actions and action creators here:
http://redux.js.org/docs/recipes/ReducingBoilerplate.html
____________________________________________________
**ABOUT STATE AND GREET**
A big challenge in any app is--

  *-Where do I keep all the data regarding my application along its lifetime?*
*    You keep it the way you want (JS object, array,        Immutable structure, ...).
 *    Data of your application will be called state.       This makes sense since we're talking about all the application's data that will evolve over time, it's really the application's state. (Redux is a "state container").
     
  *-How do I handle modification of such data?*
*  Using reducers (called "stores" in traditional flux).
 *    A reducer is a subscriber to actions.
  *   A reducer is just a function that receives the current state of your application, the action, and returns a new state modified (or reduced as they call it)
  
  -How do I propagate modifications to all parts of my application?
*  Using subscribers to state's modifications.

 Redux (https://github.com/reactjs/redux) is a "predictable state container for JavaScript apps"
 
  To sum up, Redux will provide you:
     1. a place to put your application state
     2. a mechanism to dispatch actions to modifiers of your application state, AKA reducers
     3. a mechanism to subscribe to state updates
 
 The Redux instance is called a store and can be created like this:
 
     import { createStore } from 'redux'

    var store = createStore(() => {})
  
  ___________________________________
  **SIMPLE REDUCER**
  
  *How exactly do Store and Reducer differ?*
*  A Store keeps your data in it while a Reducer doesn't. So in traditional flux, stores hold state in them while in Redux, each time a reducer is called, it is passed the state that needs to be updated. This way, Redux's stores became "stateless stores" and were renamed reducers.
=======================================
*  When called, a reducer is given those parameters: (state, action)
*  When the state is not being initialized yet it is "undefined"
___________________________________________________
**GET_STATE**
 *How do we retrieve the state from our Redux instance?*
 
       import { createStore } from 'redux'

      var reducer_0 = function (state, action) {
          console.log('reducer_0 was called with state', state, 'and action', action)
      }

    var store_0 = createStore(reducer_0)

* Output: reducer_0 was called with state undefined and action { type: '@@redux/INIT' }

* To get the state that Redux is holding for us, you call getState

      console.log('store_0 state after initialization:', store_0.getState())

* Output: store_0 state after initialization: undefined

 So the state of our application is still undefined because our reducer is not doing anything... 
     "A reducer is just a function that receives the current state of your application, the action, and returns a new state modified (or reduced as they call it)." Our reducer is not returning anything right now so the state of our application is what reducer() returns, hence "undefined".
     
  Let's try to send an initial state of our application if the state given to reducer is undefined:
  
      var reducer_2 = function (state = {}, action) {
        console.log('reducer_2 was called with state', state, 'and action', action)

        return state;
    }

    var store_2 = createStore(reducer_2)

 Output: reducer_2 was called with state {} and action { type: '@@redux/INIT' }

      console.log('store_2 state after initialization:', store_2.getState())

 Output: store_2 state after initialization: {}

 Let's now recall that a reducer is only called in response to an action dispatched and
 let's fake a state modification in response to an action type 'SAY_SOMETHING'

    var reducer_3 = function (state = {}, action) {
        console.log('reducer_3 was called with state', state, 'and action', action)

        switch (action.type) {
            case 'SAY_SOMETHING':
                return {
                    ...state,
                    message: action.value
                }
            default:
                return state;
        }
    }

    var store_3 = createStore(reducer_3)

 Output: reducer_3 was called with state {} and action { type: '@@redux/INIT' }

    console.log('store_3 state after initialization:', store_3.getState())

 Output: store_3 state after initialization: {}
 ________________________________________________
 **COMBINE REDUCERS**
  ... but before going further, we should start wondering what our reducer will look like when we'll have tens of actions:

    var reducer_1 = function (state = {}, action) {
        console.log('reducer_1 was called with state', state, 'and action', action)

        switch (action.type) {
            case 'SAY_SOMETHING':
                return {
                    ...state,
                    message: action.value
                }
            case 'DO_SOMETHING':
                // ...
            case 'LEARN_SOMETHING':
                // ...
            case 'HEAR_SOMETHING':
                // ...
            case 'GO_SOMEWHERE':
                // ...
            // etc.
            default:
                return state;
        }
    }
    
 while redux *can* hold all of these actions, it is not very maintainable.
 
 // Let's declare 2 reducers

    var userReducer = function (state = {}, action) {
        console.log('userReducer was called with state', state, 'and action', action)

        switch (action.type) {
            // etc.
            default:
                return state;
        }
    }
    var itemsReducer = function (state = [], action) {
        console.log('itemsReducer was called with state', state, 'and action', action)

        switch (action.type) {
            // etc.
            default:
                return state;
        }
    }
    
  userReducer got an initial state in the form of a literal object ({}) while
 itemsReducer got an initial state in the form of an array ([]). This is just to
 make clear that a reducer can actually handle any type of data structure. It's really
 up to you to decide which data structure suits your needs (an object literal, an array,
 a boolean, a string, an immutable structure, ...).

*So how do we combine our reducers? And how do we tell Redux that each reducer will only handle a slice of our state?*
We use Redux combineReducers helper function. combineReducers takes a hash and returns a function that, when invoked, will call all our reducers, retrieve the new slice of state and reunite them in a state object (a simple hash {}) that Redux is holding.
ex.

    import { createStore, combineReducers } from 'redux'

    var reducer = combineReducers({
        user: userReducer,
        items: itemsReducer
    })
 Output:
* userReducer was called with state {} and action { 8type: '@@redux/INIT' }
* userReducer was called with state {} and action { type: '@@redux/PROBE_UNKNOWN_ACTION_9.r.k.r.i.c.n.m.i' }
* itemsReducer was called with state [] and action { type: '@@redux/INIT' }
* itemsReducer was called with state [] and action { type: '@@redux/PROBE_UNKNOWN_ACTION_4.f.i.z.l.3.7.s.y.v.i' }

          var store_0 = createStore(reducer)
 Output:
* userReducer was called with state {} and action { type: '@@redux/INIT' }
* itemsReducer was called with state [] and action { type: '@@redux/INIT' }
 ___________________________
 **DISPATCH-ACTION**
 So far we've focused on building our reducer(s) and we haven't dispatched any of our own actions.
 We'll keep the same reducers from our previous tutorial and handle a few actions:

      var userReducer = function (state = {}, action) {
          console.log('userReducer was called with state', state, 'and action', action)

          switch (action.type) {
              case 'SET_NAME':
                  return {
                      ...state,
                      name: action.name
                  }
              default:
                  return state;
          }
      }
      var itemsReducer = function (state = [], action) {
          console.log('itemsReducer was called with state', state, 'and action', action)

          switch (action.type) {
              case 'ADD_ITEM':
                  return [
                      ...state,
                      action.item
                  ]
              default:
                  return state;
          }
      }

      import { createStore, combineReducers } from 'redux'

      var reducer = combineReducers({
          user: userReducer,
          items: itemsReducer
      })
      var store_0 = createStore(reducer)


      console.log("\n", '### It starts here')
      console.log('store_0 state after initialization:', store_0.getState())
 Output:
 store_0 state after initialization: { user: {}, items: [] }

 Let's dispatch our first action... Remember in 'simple-action-creator.js' we said:
     "To dispatch an action we need... a dispatch function." Captain obvious

 The dispatch function we're looking for is provided by Redux and will propagate our action
 to all of our reducers! The dispatch function is accessible through the Redux
 instance property "dispatch"

 To dispatch an action, simply call:

store_0.dispatch({
    type: 'AN_ACTION'
})
 Output:
 userReducer was called with state {} and action { type: 'AN_ACTION' }
 itemsReducer was called with state [] and action { type: 'AN_ACTION' }

 Each reducer is effectively called but since none of our reducers care about this action type,
 the state is left unchanged:

console.log('store_0 state after action AN_ACTION:', store_0.getState())
 Output: store_0 state after action AN_ACTION: { user: {}, items: [] }

 But, wait a minute! Aren't we supposed to use an action creator to send an action? We could indeed
 use an actionCreator but since all it does is return an action it would not bring anything more to
 this example. But for the sake of future difficulties let's do it the right way according to
 flux theory. And let's make this action creator send an action we actually care about:

    var setNameActionCreator = function (name) {
        return {
            type: 'SET_NAME',
            name: name
        }
    }
    

    store_0.dispatch(setNameActionCreator('bob'))
 Output:
 userReducer was called with state {} and action { type: 'SET_NAME', name: 'bob' }
 itemsReducer was called with state [] and action { type: 'SET_NAME', name: 'bob' }

      console.log('store_0 state after action SET_NAME:', store_0.getState())

 Output:
 store_0 state after action SET_NAME: { user: { name: 'bob' }, items: [] }

 We just handled our first action and it changed the state of our application!

 But this seems too simple and not close enough to a real use-case. For example,
 what if we'd like do some async work in our action creator before dispatching
 the action? We'll talk about that in the next tutorial "dispatch-async-action.js"

 So far here is the flow of our application
 ActionCreator -> Action -> dispatcher -> reducer
 
 ______________________________________
 **DISPATCH ASYNC ACTION**
  We previously saw how we can dispatch actions and how those actions will modify
 the state of our application thanks to reducers.

 But so far we've only considered synchronous actions or, more exactly, action creators
 that produce an action synchronously: when called an action is returned immediately.

 Let's now imagine a simple asynchronous use-case:
 1) user clicks on button "Say Hi in 2 seconds"
 2) When button "A" is clicked, we'd like to show message "Hi" after 2 seconds have elapsed
 3) 2 seconds later, our view is updated with the message "Hi"

 Of course this message is part of our application state so we have to save it
 in Redux store. But what we want is to have our store save the message
 only 2 seconds after the action creator is called (because if we were to update our state
 immediately, any subscriber to state's modifications - like our view - would be notified right away
 and would then react to this update 2 seconds too soon).

 If we were to call an action creator like we did until now...

import { createStore, combineReducers } from 'redux'

var reducer = combineReducers({
    speaker: function (state = {}, action) {
        console.log('speaker was called with state', state, 'and action', action)

        switch (action.type) {
            case 'SAY':
                return {
                    ...state,
                    message: action.message
                }
            default:
                return state;
        }
    }
})
var store_0 = createStore(reducer)

var sayActionCreator = function (message) {
    return {
        type: 'SAY',
        message
    }
}

console.log("\n", 'Running our normal action creator:', "\n")

console.log(new Date());
store_0.dispatch(sayActionCreator('Hi'))

console.log(new Date());
console.log('store_0 state after action SAY:', store_0.getState())
 Output (skipping initialization output):
     Sun Aug 02 2015 01:03:05 GMT+0200 (CEST)
     speaker was called with state {} and action { type: 'SAY', message: 'Hi' }
     Sun Aug 02 2015 01:03:05 GMT+0200 (CEST)
     store_0 state after action SAY: { speaker: { message: 'Hi' } }


 ... then we see that our store is updated immediately.

 What we'd like instead is an action creator that looks a bit like this:

var asyncSayActionCreator_0 = function (message) {
    setTimeout(function () {
        return {
            type: 'SAY',
            message
        }
    }, 2000)
}

 But then our action creator would not return an action, it would return "undefined". So this is not
 quite the solution we're looking for.

 Here's the trick: instead of returning an action, we'll return a function. And this function will be the
 one to dispatch the action when it seems appropriate to do so. But if we want our function to be able to
 dispatch the action it should be given the dispatch function. Then, this should look like this:

var asyncSayActionCreator_1 = function (message) {
    return function (dispatch) {
        setTimeout(function () {
            dispatch({
                type: 'SAY',
                message
            })
        }, 2000)
    }
}

 Again you'll notice that our action creator is not returning an action, it is returning a function.
 So there is a high chance that our reducers won't know what to do with it. But you never know, so let's
 try it out and find out what happens...
___________________________________________
**DISPATCH ASYNC ACTION 2**
 Let's try to run the first async action creator that we wrote in dispatch-async-action-1.js.

      import { createStore, combineReducers } from 'redux'

      var reducer = combineReducers({
          speaker: function (state = {}, action) {
              console.log('speaker was called with state', state, 'and action', action)

              switch (action.type) {
                  case 'SAY':
                      return {
                          ...state,
                          message: action.message
                      }
                  default:
                      return state;
              }
          }
      })
      var store_0 = createStore(reducer)

      var asyncSayActionCreator_1 = function (message) {
          return function (dispatch) {
              setTimeout(function () {
                  dispatch({
                      type: 'SAY',
                      message
                  })
              }, 2000)
          }
      }
-
      console.log("\n", 'Running our as-ync action creator:', "\n")
      store_0.dispatch(asyncSayActionCreator_1('Hi'))

 Output:
     ...
     /Users/classtar/Codes/redux-tutorial/node_modules/redux/node_modules/invariant/invariant.js:51
         throw error;
               ^
     Error: Invariant Violation: Actions must be plain objects. Use custom middleware for async actions.
     ...

 It seems that our function didn't even reach our reducers. But Redux has been kind enough to give us a
 tip: "Use custom middleware for async actions.". It looks like we're on the right path but what is this
 "middleware" thing?

___________________________________________________
**MIDDLEWARE**

Generally Speaking middleware is something  is something that goes between parts A and B of an application to transfrom what A sends before passing it to B, So instead of having:
A ----> B
we end up having 
A --->middleware1--->middleware2--->...---> B
In Redux this would look like:
action-->dispatcher-->middleware1-->middleware2-->reducers
Our middleware will be called each time an action is dispatched and it wants to (or do nothing - this is a totally valid and some-times desired behavior). 


    var anyMiddleware = function ({ dispatch, getState }) {
        return function(next) {
            return function (action) {
                // your middleware-specific code goes here
            }
        }
    }


 As you can see above, a middleware is made of 3 nested functions (that will get called sequentially):
 1) The first level provides the dispatch function and a getState function (if your
     middleware or your action creator needs to read data from state) to the 2 other levels
 2) The second level provides the next function that will allow you to explicitly hand over
     your transformed input to the next middleware or to Redux (so that Redux can finally call all reducers).
 3) the third level provides the action received from the previous middleware or from your dispatch
     and can either trigger the next middleware (to let the action continue to flow) or process
     the action in any appropriate way.

Here is how you would integrate a middleware into your Redux store:

    import { createStore, combineReducers, applyMiddleware } from 'redux'

    const finalCreateStore = applyMiddleware(thunkMiddleware)(createStore)

// For multiple middlewares, write: applyMiddleware(middleware1, middleware2, ...)(createStore)


    var reducer = combineReducers({
        speaker: function (state = {}, action) {
            console.log('speaker was called with state', state, 'and action', action)

            switch (action.type) {
                case 'SAY':
                    return {
                        ...state,
                        message: action.message
                    }
                default:
                    return state
            }
        }
    })

    const store_0 = finalCreateStore(reducer)
 Output:
     speaker was called with state {} and action { type: '@@redux/INIT' }
     speaker was called with state {} and action { type: '@@redux/PROBE_UNKNOWN_ACTION_s.b.4.z.a.x.a.j.o.r' }
     speaker was called with state {} and action { type: '@@redux/INIT' }

 Now that we have our middleware-ready store instance, let's try again to dispatch our async action:

      var asyncSayActionCreator_1 = function (message) {
          return function (dispatch) {
              setTimeout(function () {
                  console.log(new Date(), 'Dispatch action now:')
                  dispatch({
                      type: 'SAY',
                      message
                  })
              }, 2000)
          }
      }

      console.log("\n", new Date(), 'Running our async action creator:', "\n")

      store_0.dispatch(asyncSayActionCreator_1('Hi'))
 Output:
     Mon Aug 03 2015 00:01:20 GMT+0200 (CEST) Running our async action creator:
     Mon Aug 03 2015 00:01:22 GMT+0200 (CEST) 'Dispatch action now:'
     speaker was called with state {} and action { type: 'SAY', message: 'Hi' }

See http://redux.js.org/docs/introduction/Ecosystem.html#middleware, section Middleware, to see other middleware examples.
________________________________________________
**STATE-SUBSCRIBER**
Adds a change listener. It will be called any time an action is dispatched, and some part of the state tree may potentially have changed. You may then call getState() to read the current state tree inside the callback.

    import { createStore, combineReducers } from 'redux'

    var itemsReducer = function (state = [], action) {
        console.log('itemsReducer was called with state', state, 'and action', action)

        switch (action.type) {
            case 'ADD_ITEM':
                return [
                    ...state,
                    action.item
                ]
            default:
                return state;
        }
    }

    var reducer = combineReducers({ items: itemsReducer })
    var store_0 = createStore(reducer)

    store_0.subscribe(function() {
        console.log('store_0 has been updated. Latest store state:', store_0.getState());
        // Update your views here
    })

    var addItemActionCreator = function (item) {
        return {
            type: 'ADD_ITEM',
            item: item
        }
    }

    store_0.dispatch(addItemActionCreator({ id: 1234, description: 'anything' }))
    
 Output:
     ...
     store_0 has been updated. Latest store state: { items: [ { id: 1234, description: 'anything' } ] }

 Our subscribe callback is correctly called and our store now contains the new item that we added.
 
 
   
 