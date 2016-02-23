# redux-deferred
![NPM](https://david-dm.org/wyvernnot/redux-deferred.svg)
[![Build Status](https://travis-ci.org/wyvernnot/redux-deferred.svg?branch=master)](https://travis-ci.org/wyvernnot/redux-deferred)

Redux middleware for jQuery Deferred object. Insipied by [redux-promise](https://github.com/acdlite/redux-promise).

[![NPM](https://nodei.co/npm/npm2dot.png)](https://nodei.co/npm/npm2dot/)

## Preface

To create an AJAX request in jQuery is easy.

```js
$.get('some.url',function(result){
  // do things with result
})
```

It is not known by everyone thar all AJAX method in jQuery will return an [Deferred](http://api.jquery.com/category/deferred-object/)
 object for you to use. So the code above can be rewriten like this:

```js
let deferredObject = $.get('some.url');
deferredObject.done(function(result){
  // do things with result
})
```

Using this middleware you can wrap it into an action and dispatch it like any normal actions.

```js
let action = {
   type:'LOAD_SOME',
   payload: deferredObject
}

store.dispatch(action);
```

Since Deferred is often async, it will not be actually dispatched until it is resolved or rejected.

```js
(state={},action)=>{
  switch(action.type){
    case 'LOAD_SOME':
      if(action.error){
        return Object.assign({},state,{
          error:action.payload
        });
      }else{
        return Object.assign({},state,{
          data:action.payload
        });
      }
   default:
      return state;
  }
}
```

## Usage

**Install**
```sh
npm install redux-deferred
```
**ES6**

```js
import DeferredMiddleware from 'redux-deferred';
let reducers= YOUR_REDUCER_DEFINITION;
let store = createStore(reducers,applyMiddleware(DeferredMiddleware));
```

## Reference

- [promisejs.org](https://www.promisejs.org/)
- [redux-promise](https://github.com/acdlite/redux-promise)

## License

MIT
