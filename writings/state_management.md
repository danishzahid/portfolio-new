---
title: "State Management in Java Script: Concept of Reduce and Reducers"
description: "This blog delves into JavaScript state management, elucidating array.reduce and its functionality. It distinguishes between useReduce and redux reducers, providing clear insights in a concise manner."
date: "2022-08-12"
---

# Introduction to State Management

State management is a fundamental concept in software development, especially concerning user interfaces. It involves the management and storage of data within an application, representing the current condition of the application. This includes user input, visibility of user interface elements, and data fetched from external sources.

In dynamic user interfaces, state management is crucial because interfaces are not static; they change based on user interactions, data loading, authentication status, and other dynamic factors.

State management contributes to dynamic UI in modern web apps in various ways:

1. **Dynamic Content Rendering:**

   - _Use Case:_ Displaying a list of items.
   - _Role of State:_ The state tracks the list of items. When the list updates, the state triggers UI re-rendering, ensuring the user sees the latest data.

2. **User Interactions:**

   - _Use Case:_ Handling form inputs, button clicks, and other user interactions.
   - _Role of State:_ State variables store form input values and interactive element statuses. When a user interacts with these elements, the state updates, triggering UI updates and component re-renders.

3. **Conditional Rendering:**

   - _Use Case:_ Displaying different UI components based on user roles or permissions.
   - _Role of State:_ State variables determine user roles or permissions. Components conditionally render UI elements based on state values, ensuring the correct components display for each user.

4. **Error Handling:**

   - _Use Case:_ Displaying error messages for failed data fetching or form submissions.
   - _Role of State:_ Error messages are stored in the state. When an error occurs, the state updates with the error message, causing the UI to display the appropriate error to the user.

5. **Real-time Data and WebSockets:**

   - _Use Case:_ Displaying real-time data updates (e.g., live chat messages, notifications).
   - _Role of State:_ State manages real-time data from APIs or WebSocket connections. When new data arrives, the state updates, and React components re-render to reflect the latest information in the UI.

6. **Authentication and Authorization:**

   - _Use Case:_ Managing user login status, user roles, and access permissions.
   - _Role of State:_ State variables store user authentication status and roles. Components check the state to determine if a user is logged in, redirect users based on authentication status, and show or hide UI elements based on user roles.

7. **Complex UI States:**
   - _Use Case:_ Managing multi-step forms, wizards, or other complex UI states.

> **Role of State:** State can store step numbers, form data, or any other complex UI state. By updating the state, components can navigate between steps, validate form inputs, and manage the overall flow of the user interface.

> Now let us dive into the crucial concept of state management widely used. The reducer functions and array.reduce() method.

# 1. Array.reduce():

Used to reduce the arr to a single value by executing a provided function(reducer) for each value of the arr from left to right and return value is stored in an accumulator.

```
array.reduce(function(accumulator, current val, current index, arr), initialValue);
```

Current index and arr obj are optional parameter, initialValue is also a optional parameter.
If you don't provide an initial value, the reduce function uses the first element of the array as the initial accumulator value and starts reducing from the second element onward.

```
array.reduce(reducer fn, initialValue)// reducerfn(accumulator,current Value).
```

Reducer fn is callback fn.a "callback," is a function that is passed as an argument to another function and is executed after the completion of that function.

```// Input array
let arr = [10, 20, 30, 40, 50, 60];
// Callback function for reduce method
function sumofArray(sum, num) {
    return sum + num;
}
//Fucntion to execute reduce method
function myGeeks(item) {
    // Display output
    console.log(arr.reduce(sumofArray));
}
Here's how you can use  array.reduce() to manage the state of the total price of items in the cart:

const cartItems = [
  { id: 1, name: 'Item 1', price: 20 },
  { id: 2, name: 'Item 2', price: 30 },
  { id: 3, name: 'Item 3', price: 15 }
];

const totalPrice = cartItems.reduce((accumulator, currentItem) => {
  return accumulator + currentItem.price;
}, 0);

console.log('Total Price:', totalPrice);
```

> **This is how we can implement our own reduce function in javascript**

```
function myReduceFromIndex(array, callback, initialValue, startIndex) {
  let accumulator = initialValue !== undefined ? initialValue : array[startIndex];
  const start = initialValue !== undefined ? startIndex : startIndex + 1;

  for (let i = start; i < array.length; i++) {
    accumulator = callback(accumulator, array[i], i, array);
  }

  return accumulator;
}

// Example usage:
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Using myReduceFromIndex to sum elements from the 4th index till the end of the array
const startIndex = 3; // Index from where to start summing (4th index)
const sum = myReduceFromIndex(numbers, (accumulator, currentValue) => accumulator + currentValue, 0, startIndex);
console.log('Sum from 4th index till end:', sum); // Output: 55 (4 + 5 + 6 + 7 + 8 + 9 + 10)

```

The function loops through the array, starting from the appropriate index (either 0 or 1, based on whether an initial value is provided), and applies the callback function to each element. The result of the callback function becomes the new accumulator value for the next iteration. Finally, the function returns the accumulated result

# 2. Reducer in useReduce:

**1. Reduction Operation:**

Both the reducer function in `useReducer` and the callback function in `array.reduce()` perform reduction operations. They take an accumulator and the current element (or action in the case of `useReducer`) as arguments and return a new accumulator value.

**2. Accumulator and Current Value:**

The reducer function in `useReducer` and the callback function in `array.reduce()` both take an accumulator and a `currentValue` as parameters. The accumulator accumulates the values and changes its state as the reduction progresses.

While both concepts involve the idea of reducing data, the reducer function used with `useReducer` is specific to React and handles state management within components. It has no direct relationship with the `array.reduce()` method in JavaScript.

**Differences:**

**1. Purpose and Context:**

- `useReducer` in React is specifically designed for managing state in functional components. It is used to manage complex state logic where the next state depends on the previous state and some action.
- `array.reduce()` is a general-purpose method in JavaScript for reducing an array of values into a single value. It is used for various tasks such as summing numbers, finding maximum/minimum values, transforming data, and more.

**2. Action and State in useReducer:**

- In `useReducer`, the reducer function takes two parameters: `state` and `action`. The `action` parameter is an object describing the action to be performed, while the `state` parameter represents the current state.
- In `array.reduce()`, the callback function takes four parameters: `accumulator`, `currentValue`, `currentIndex`, and `array`. The `accumulator` accumulates the return values of the callback function, and there is no concept of an action or state.

**3. Return Value:**

- The reducer function in `useReducer` returns the new state based on the provided action. It must return a new state object or the current state if no changes are necessary.
- The callback function in `array.reduce()` returns the accumulated value after the reduction is complete. The return value can be of any type, depending on the specific use case.

```
// reducer function
const cartReducer = (state, action) => {
  switch (action.type) {
    case 'ADD_TO_CART':
      return {
        ...state,
        cartItems: [...state.cartItems, action.payload],
      };
    case 'REMOVE_FROM_CART':
      return {
        ...state,
        cartItems: state.cartItems.filter(item => item.id !== action.payload.id),
      };
    default:
      return state;
  }
};

```

In this example, the reducer handles two actions: 'ADD_TO_CART' and 'REMOVE_FROM_CART'. It adds items to the cart by appending them to the cartItems array and removes items by filtering them out based on their id.

Next, let's use the useReducer hook in a React component to manage the cart state:

```
import React, { useReducer } from 'react';

const initialCartState = {
  cartItems: [],
};

const ShoppingCart = () => {
  const [cartState, dispatch] = useReducer(cartReducer, initialCartState);

  const addToCart = (item) => {
    dispatch({ type: 'ADD_TO_CART', payload: item });
  };

  const removeFromCart = (item) => {
    dispatch({ type: 'REMOVE_FROM_CART', payload: item });
  };

  return (
    <div>
      <h2>Shopping Cart</h2>
      <ul>
        {cartState.cartItems.map(item => (
          <li key={item.id}>
            {item.name}
            <button onClick={() => removeFromCart(item)}>Remove</button>
          </li>
        ))}
      </ul>
      <button onClick={() => addToCart({ id: 1, name: 'Product 1' })}>Add Product 1</button>
      <button onClick={() => addToCart({ id: 2, name: 'Product 2' })}>Add Product 2</button>
    </div>
  );
};

export default ShoppingCart;

```

In this example, the useReducer hook manages the cart state. The addToCart function dispatches an action to add items to the cart, and the removeFromCart function dispatches an action to remove items from the cart.

This is a basic implementation and can be expanded further to handle more complex cart operations in a real e-commerce application.

## useReducer in Short and Easy Terms:

`useReducer` is a React hook that helps manage state in a more complex manner. It's like `useState`, but for more advanced state management scenarios. It takes in a reducer function and an initial state, and it returns the current state and a dispatch function that you can use to update the state based on certain actions.

```
//codes
import React, { useReducer } from "react";

// Reducer function
const reducer = (state, action) => {
  switch (action.type) {
    case "INCREMENT":
      return { count: state.count + 1 };
    case "DECREMENT":
      return { count: state.count - 1 };
    default:
      return state;
  }
};

const Counter = () => {
  // useReducer returns current state and a dispatch function
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      Count: {state.count}
      <button onClick={() => dispatch({ type: "INCREMENT" })}>Increment</button>
      <button onClick={() => dispatch({ type: "DECREMENT" })}>Decrement</button>
    </div>
  );
};

export default Counter;
```

**Explanation of Concepts:**

**Reducer Function:**

A reducer is a pure function that takes the current state and an action as arguments and returns a new state. It specifies how the state should change in response to the action.
In the example, the reducer takes `state` and `action` as arguments and returns a new state object based on the action type.

**State:**

`useState` manages a single value as state. `useReducer` can manage more complex state structures.
In the example, the state is an object: `{ count: 0 }`.

**Dispatch and Action:**

`dispatch` is a function returned by `useReducer`. You call it with an action object to update the state.
An action is an object that describes what kind of operation you want to perform. It must have a `type` property that indicates the type of action.
In the example, when you click "Increment," it dispatches an action `{ type: 'INCREMENT' }`, and the reducer increases the count. Similarly, for "Decrement," it dispatches `{ type: 'DECREMENT' }`, and the reducer decreases the count.

**Redux Reducer:**

Redux is a state management library for JavaScript applications, commonly used with React. In Redux, a reducer is a pure function that specifies how the application's state changes in response to actions sent to the store. Redux's concepts are somewhat similar to useReducer, but there are key differences.

# 3. Redux Reducer: Basic Example

In Redux, you create a reducer that specifies how the state should change based on dispatched actions. Here's a basic example of a Redux reducer managing a counter:

```
// Reducer function
const counterReducer = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
};
```

In this example, the `counterReducer` takes the current state and an action, and it returns the new state based on the action type.

**Differences Between Redux Reducer and useReducer:**

1. **Single Store:**
   Redux operates with a single centralized store for the entire application. Reducers handle specific slices of this global state.

2. **Immutable State:**
   In Redux, state updates must be immutable. Reducers always return new state objects, never modify the existing state directly. This is a fundamental principle of Redux.

3. **Action Dispatch:**
   Actions in Redux are dispatched explicitly using the `dispatch` function provided by Redux. Actions are plain JavaScript objects with a `type` property that describes the type of action.

4. **Middleware and Side Effects:**
   Redux allows you to apply middleware (like Redux Thunk) for handling asynchronous actions and side effects, providing a more complex and robust state management solution.

5. **Predictable State Changes:**
   Redux ensures predictable state changes by following strict principles and patterns, leading to a more manageable and debuggable application state.

# Conclusion

Redux emphasizes predictability. Given the same initial state and a sequence of actions, a Redux reducer will always produce the same state.
In contrast, useReducer is a React hook used for local component state management. It operates at a component level and doesn't enforce immutability rules or handle global state like Redux does. While both concepts use the term "reducer," they serve different scopes and purposes within a JavaScript application. Redux's reducer is specifically tailored for managing global application state and follows strict principles for predictable state management. useReducer, on the other hand, is used for managing component-level state within React components.

> If you have any suggestions for improvement please reach out to me at [Twitter](https://twitter.com/danishzahid111)
