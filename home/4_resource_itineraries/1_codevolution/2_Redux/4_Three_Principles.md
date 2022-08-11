# 4. Three Principles
Created Thursday 11 August 2022

How should we write code that implements the 3 core concepts of Reacts?

### Three Principles
1. The global state of the application is stored as object inside a single store. Example:
	```js
	// example app store
	{
		theme: "dark",
		numberOfWindows: 5,
	}
	```
2. The only way to change the state (i.e. store) is to dispatch an action. Example of an action:
	```js
	{
		type: 'INCREASE_BY',
		payload: 10,
	}
	```
3. All reducers should be pure functions that return the new state - i.e. they should be synchronous and free of side-effects (including direct mutation of state). Example of a reducer:
	```js
	function storeReducer(state, action) {
		switch(action.type) {
			case 'INCREASE': return {...state, count: state.count + 1};
			case 'DECREASE': return {...state, count: state.count - 1};
			case 'INCREASE_BY': return {...state, count: state.count + action.payload};

			default: return state;
		}
	}
	```

![[Pasted image 20220811193147.png]]