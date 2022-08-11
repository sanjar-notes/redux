# 7. Store
Created Thursday 11 August 2022

- We should have only one store for the entire application.

Responsibilities of the store:
1. Hold the application state
2. Allow access to the latest state via `getState`
3. Allow state to be updated via `dispatch(action)`
4. Register listeners via `subscribe(listenerCallback)`
5. Handle unregistering of listeners via execution of the function returned by `subscribe(listener)` call. Example:
	```js
	function subscription1Callback() {}
	
	const unsubscribe1 = store.subscribe(subscription1Callback); // subscribed

	unsubscribe1(); // unsubscribed
	```