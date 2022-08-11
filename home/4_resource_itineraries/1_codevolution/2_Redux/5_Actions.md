# 5. Actions
Created Thursday 11 August 2022

- Actions carry signals along with an optional payload from the app to the Redux system (i.e. reducer and store).
- They are plain objects that generally have a `type` attribute which is a string and an optional properties which can be of any type. Generally, everything except the `type` is nested into an object inside a `payload` property.
  
- Action types are stored in variable named as themselves. Reason: eliminate typos while triggering actions. So, the code like the following is generally found in a codebase using Redux:
	```js
	const CAKE_ORDERED = 'CAKE_ORDERED';
	const CAKE_ORDER_CANCELLED = 'CAKE_ORDER_CANCELLED';
	```

- An "action creator" is a function that return an action. Example:
	```js
	const CAKE_ORDERED = 'CAKE_ORDERED';
	
	function orderCake() {
		return {
			type: CAKE_ORDERED,
			payload: 1
		};
	}
	```
	Why have an action creator? We'll see. (FIXME)