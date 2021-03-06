# Trux (T-Rux) 🦖

> React Hooks State Mangement System

i can't publish it to the NPM, if any one can do this, fork and do it

## Usage

### 1. Create Storage (States, Actions)

> my store folder at [here](./App/Store)

Before anything, you should create to file, first state [or any name] (that contain you states and data objects),
then Actions [or any name] (this save your any action and method, you want to change state objects).

```js
	// ./Store/Actions.js

	// RULE 1 : every action functions should give {state} as first args, then other parameter.
	// RULE 2 : each action function would return an Object from old states and new State keyword with new Value as Object.
	// RULE 3 : for exporting and useing actions, you can use with any exporting, just, you would send actions as Object to `createTrux`

	// CREATE ACTIONS FUNCTION
	const ACTION_1 = ({state}, ...action_params) => ({...state, myKeyToChange: state.myKeyToChange + 1 });
	const OTHER_ACTION = ({state}, newName) => {
		let data = { ...state, name: newName };
		return data;
	};

	// EXPORT THEY
	export { ACTION_1, OTHER_ACTION };
```

### 2. Provider Creation

> this process should be in root component, alike `index.js` or `App.js` or any file you want to be.

then you importing `createTrux()` hook, then Send imported Object from Store Folder (state, actions) to them.
and it, return an Object, you should send it as `store` props to `Provider`. so, what is Provider?

Provider is an Component you would import it from Trux and use your node components as children for this Component.

```jsx
    // index.js //MyRootComponent.js
    ...
    import Children from './Component/index.js';
    import { Provider, createTrux } from 'trux';
    import State from './Store/state.js';
    import * as Actions from './Store/actions.js';
    ...
    const App = () => {
    	const Store = createTrux({ state: State, actions: Actions });
    	return(
    		<Provider store={Store}>
    			<Children />
    		</Provider>,
    	);
    };
    ...
```

### 3. `useTrux`

to this step, you want to use `states` and `actions`?

so, you use them, with importing `useTrux` from `trux`

```jsx
    // ./component/index.js MyChildNodeComponent
    ...
    import useTrux from 'trux';

    const Component = () => {
    	const { state, actions } = useTrux();
    	return (
    		<div>
    			<span>my state key name is { state['my-state-name'] }</span>
    			<button onClick={() => actions.MY_ACTION(...params)}>
    				button is clickable
    			</button>
    		</div>
    	);
    };
    ...
```
