---
title: "State Management in Javascript"
date: 2019-02-12T13:34:46-06:00
draft: false
---

I've gotten a bit tired of dependencies. That's perhaps a bit ironic for somebody who does most of his programming in javascript. But after spending yet another chunk of hours trying to upgrade Angular in a project I've come to think there must be a better way of building software that doesn't involve 1000s of node_modules dependencies.

At the same time I've been thinking about programming games in Javascript. This isn't exactly a new idea in 2019, but after 10 years of web development I still haven't made a game. It was games that initally got me into computers, so it makes sense to return to my roots and start creating my own.

A basic component of any software is a state management system. We all know things like [Redux](https://redux.js.org/), [MobX](https://mobx.js.org/), [VueX](https://vuex.vuejs.org/) exist and do the job of state management well. But I'm tired of not knowing what all the code in my project does. After years of front-end dev and Drupal work, I'm sick of sorting out errors deep within the guts of a framework or the tedium of coming back to a project and needing to upgrade all the dependencies to get started working. So I decided a first step in making games would be to roll my own state management library.

