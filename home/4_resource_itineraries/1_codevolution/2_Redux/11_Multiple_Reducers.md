# 11. Multiple Reducers
Created Friday 12 August 2022

We wish to add a second count to the store. Assume it is completely unrelated to the first count and has different actions that it.

How do we code this? There are two ways:
1. Add all required properties of secondCount as an object to the store, and add it's reducer logic in the existing reducer.
2. Create two different reducers, each of which work on firstCount and secondCount, and don't interfere. Next we'll use `combineReducers` function to combine all reducers (2 in this case). `combineReducers` takes in an object of key and reducer pairs and outputs the combined reducer which can be used to create the store.
   
	The created store will now be a partitioned one, i.e. each part of the store will be an object with key same as that specified in the `combineReducers` function.

	Note that although the store is partitioned now (appropriate code should be written when accessing store), reducers are not paritioned - i.e. they see only their part of the store.

	Example:
	```js
	const { combineReducers, createStore } = require('redux');
	
	const cakeInitialState = { numOfCakes: 10 };

	const CAKE_ORDERED = 'CAKE_ORDERED';
	const CAKE_RESTOCKED = 'CAKE_RESTOCKED';
	
	function cakeReducer(state = cakeInitialState, action) {
		switch(action.type) {
			case CAKE_ORDERED: return {...state, numOfCakes: state.numOfCakes - 1};
			case CAKE_RESTOCKED: return {...state, numOfCakes: state.numOfCakes + action.payload };

			default: return state;
		}
	}

	
	const iceCreamInitialState = { numOfIceCreams: 20 };

	const ICECREAM_ORDERED = 'ICECREAM_ORDERED';
	const ICECREAM_RESTOCKED = 'ICECREAM_RESTOCKED';
	
	function iceCreamReducer(state = iceCreamInitialState, action) {
		switch(action.type) {
			case ICECREAM_ORDERED: return {...state, numOfIceCreams: state.numOfIceCreams - 1};
			case ICECREAM_RESTOCKED: return {...state, numOfIceCreams: state.numOfIceCreams + action.payload };

			default: return state;
		}
	}


	const rootReducer = combineReducers({ cake: cakeReducer, iceCream: iceCreamReducer });

	const store = createStore(rootReducer);


	console.log(store.getState());
	
	store.dispatch({type: CAKE_ORDERED}); 
	console.log(store.getState());
	
	store.dispatch({type: ICECREAM_RESTOCKED, payload: 20});
	console.log(store.getState());
	```
	The output is, verify by running [this](https://github.com/exemplar-codes/redux-demo-codevolution/blob/93576ac6d7c21cd464882c8dc57f3add896f23e7/multipleReducers.js):
	```js
	{ cake: { numOfCakes: 10 }, iceCream: { numOfIceCreams: 20 } };
	{ cake: { numOfCakes: 9 }, iceCream: { numOfIceCreams: 20 } };
	{ cake: { numOfCakes: 9 }, iceCream: { numOfIceCreams: 40 } };
	```

	When a dispatch is done, all reducers are run with their part of the state, but only those execute which have the emitted action. In short, all actions should be unique.
