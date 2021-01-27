---
layout: post
title:      "Stop, Think, React! and R-R-R-REDUX"
date:       2021-01-27 22:15:06 +0000
permalink:  stop_think_react_and_r-r-r-redux
---


This module's project involves using Javascript framework React to make a customizable web application composed of components, building blocks that when combined make easily customizable, very responsive web pages. Like the Javascript project this one also has a backend API that the frontend must communicate with to load persistant data and for the user to create\delete data. In order to effectively load data from the backend we need to have the ability to state when data is still loading since the webpage may have finished loading before all the data was fetched from the backend. In order to get this functionality we use a Middleware called `Redux Thunk`. With Thunk we can return a **function** in our actions.
See our action below, fetchUsers in UserAction.js vs importBudget in budgetAction.js:
```
// ./src/actions/userAction.js
export const fetchUsers = () => {
    return (dispatch) => {
        dispatch({ type: LOADING_USER });
        fetch('http://localhost:3001/users')
        .then(response => response.json())
        .then(userData => {
            dispatch({ type: ADD_USER, user: userData })
            dispatch({ type: ADD_ENTRY, user: userData.entries })
            dispatch({ type: ADD_ITEM, user: userData.items })
        })
    };
}
// vs
// ./src/actions/budgetAction.js
export const importBudget = (entries) => {
    return { type: IMPORT_ENTRIES, entries }
}
```
A normal action like `importBudget` just returns a Javascript object, in this case `{ type: IMPORT_ENTIRES, entries }` but as you can see `fetchUsers` looks much different. It returns a function that in itself can dispatch multiple actions. This power to return a function is what Rexux Thunk gives us. 

This Budget Buddy web application fetches the user information from the backend database, and while it is fetching the data it sets a loading state, once the user's info is fetched from the backend the web application populates the global state with the User's info, budget items, and wishlist items.

Wait, rewind... Did someone say a global state?! YES! Instead of having passdown functions and states from parent to child and on and on as props we can **store** them in a *global state* which we call a `store`. See what I did there--*I make joke!* 
With the power or Redux I can connect a component to the global store by putting `import { connect } from 'react-redux';` in the file I can pass global state values as props by making a `mapStateToProps` function and connecting it via the line`export default connect(mapStateToProps)(myApp)`
Let's take a look at my IncomeStatement.js file for a clearer understanding.
```
// ./src/containers/IncomeStatement.js
import React, { Component } from 'react'
import { connect } from 'react-redux'; //This gives us the ability to connect to the global store

// lots of code here

const mapStateToProps = state => {
    return { entries: state.budgetReducer.entries }
}
export default connect(mapStateToProps)(IncomeStatement);
```

As you can see above I import the ability to give us Redux connect, then dictate what I want from the global store, and how to store it as a local property for this component.

The idea of React using components, essentially ambiguous building blocks, and combinding them to create incredibly reactive, functional and easier to code\read web applications. Combined with Redux and it's toolbox, along with the many other npm packages out there the possiblities are endless.
