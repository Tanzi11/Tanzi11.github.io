---
layout: post
title:      "How To Keep A Promise: A Look at Structure"
date:       2019-12-18 20:19:40 -0500
permalink:  how_to_keep_a_promise_a_look_at_structure
---


Jumping from JavaScript to React, I retained many things, but I blanked out on everything related to promises. (But, in real life, I am good at keeping promises.) Although it appeared simple, I decided to take a deeper dive. 

According to Mozilla documentation, a promise "object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value." What does that even mean? Well, why do we need a promise? Let's go back to the usage of the fetch() method which essentially deals with responses and requests through promises. 

Here's how it looks like in my React/Redux Final Project in the projectActions.js file:

```
export const getProjects = () => {
  return dispatch => {
    return fetch("http://localhost:3001/projects")
      .then(response => response.json())
      .then(data => dispatch({type: GET_PROJECTS_SUCCESS, payload: data }))
      .catch(err => dispatch({type: GET_PROJECTS_FAILURE, payload: 'Unable to fetch projects'}))
  }
}
```

This is my getProjects() method which is invoked in my ProjectList component in the componentDidMount() method.
```
  componentDidMount() {
    this.props.getProjects();
  }
```

So, to render my ProjectList component, in my action file, this method gets invoked which returns the dispatch method that triggers the action that will fetch the backend URL we are working with. And that's when our promises come in the form of .then, which gets a response in the form of a json object(that needs to be unwrapped) and does not return anything until the data is retrieved from the projectReducer.js file: 

```
const projectReducer = (state = initialValues, action) => {
  switch (action.type) {
    case actions.GET_PROJECTS_SUCCESS:
      return { ...state, allProjects: action.payload }
    case actions.GET_PROJECTS_FAILURE:
      return { ...state, error: action.payload}
    case actions.ADD_PROJECT_SUCCESS:
      return { ...state, allProjects: state.allProjects.concat(action.payload) }
    case actions.ADD_PROJECT_FAILURE:
      return { ...state, error: action.payload}
    case actions.DELETE_PROJECT_SUCCESS:
      return {...state, allProjects: state.allProjects.filter(p => p.id !== action.payload)}
    case actions.DELETE_PROJECT_FAILURE:
      return {...state, error: action.payload}
    default: {
      return state
    }
  }
}
```

And by the grace of the tech gods, if the action.type matches and all goes well, we should then state returned. But until then, essentially a promise just holds everything in a pending state until it is either resolved or rejected. 

