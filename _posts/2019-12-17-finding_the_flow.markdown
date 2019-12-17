---
layout: post
title:      "Finding the flow"
date:       2019-12-17 20:00:49 +0000
permalink:  finding_the_flow
---


For my final React/Redux project, I decided to do a simple portfolio that would showcase what I learned in the course and provide me an opportunity to experiment with more challenging aspects. 

In React, for the first step, I learned to think in terms of components. For me, because I had the obvious sections to in my portfolio: Navigation, Header, About, Resume, Contact and these were my functional/presentational components that I saw visually as my outline. From this understanding, I went on to create class components as the need arose in my project.

However, that's just structural. The essence is in grasping how redux and react work together. An instructor likened it to "if one is the body, the other is the brain." If React is the body, what does the brain look like? 

*The Redux Cycle*

To change the state, an action creator is called to produce an **action** (an object that has the information that details on to change the state) which is fed to the **dispatch** (makes copies of action to send to the reducer) that forwards the action to **reducers** (changes the data.type and data.payload and updates the data to the state) which creates a new state.
 
To begin the first step in the flow, a provider is created. A provider is a component that provides data from the store to the component it wraps. References are then provided to the store. The wrapped component interacts with the store and with connect. Just a reminder:  connect is a function that communicates with the provider. In the component that connect is wrapped, that component will be able to get the change in the store state from the provider. 

And if nothing made sense, just remember: Action -> Dispatch ->Reducer->Store->Changes (in view).
