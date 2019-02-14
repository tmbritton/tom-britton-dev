---
title: "Simple State Management in Javascript"
date: 2019-02-12T13:34:46-06:00
draft: false
---

I've gotten a bit tired of dependencies. Perhaps that's a bit ironic for somebody who does most of his work using javascript frameworks. But after spending yet another chunk of hours trying to upgrade [Angular](https://angularjs.org/) I've come to think there must be a better way of building software that doesn't involve 1000s of <span class="inlineCode">node_modules</span> dependencies.

At the same time I've been thinking about programming games in Javascript. This isn't exactly a new idea in 2019, but after 10 years of web development I still haven't made a game. Games are the reason computers were invented, so it makes sense to start creating my own.

A basic component of any software is a state management system. We all know things like [Redux](https://redux.js.org/), [MobX](https://mobx.js.org/), [VueX](https://vuex.vuejs.org/) exist and do the job of state management well. But after years of front-end dev and [Drupal](https://www.drupal.org/) work, I'm sick of sorting out errors deep within the guts of a framework or the tedium of coming back to a project and needing to upgrade all the dependencies to get started working. So I decided a first step in making games would be to roll my own [state management library](https://github.com/tmbritton/state-manager).

I wanted two things in a state management system, a pubsub component for events and a centralized data store. Also, to completely contradict my opening statement about dependencies, I wrote it in [Typescript](https://www.typescriptlang.org/). I've been using it at work recently and I find I really like the autocomplete features it provides to the text editor when you define your types.

## PubSub

First I created the [PubSub module](https://github.com/tmbritton/state-manager/blob/master/src/pubsub/PubSub.ts). This is a good 'ole [IIFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE) module. I didn't use a class because we don't want multiple instantiations of the PubSub system in a codebase. That would break the functionality. You can see in the link to the code I provided, there are just a few methods. The meat of it are the <span class="inlineCode">publish()</span> and <span class="inlineCode">subscribe()</span> methods. A basic use of this module is in the tests. Yes, I actually tested a personal project!

    test("Publishing an event", () => {
        const type = "test";

        PubSub.subscribe(type, (payload) => {
            expect(payload.test).toBe(2);
        });

        PubSub.publish(type, {test: 2});
    });

Basically you subscribe to an event type, this case the type is "test". Then you publish an event of the same type with a payload object. This object is then passed to the callback provided to the subscribe method and it acts on the payload. Simple, right?

## Store

The [store module](https://github.com/tmbritton/state-manager/blob/master/src/store/Store.ts) is where the data is held. I did use a class here, but it's debatable whether you'd ever want multiple instantiations of the Store in the application. There may be use cases. ¯\\\_(ツ)\_/¯ The flow here is you call the <span class="inlineCode">commit()</span> function with a type of mutation as the first parameter and a payload for the mutation to act on as the second parameter. The change is then published by the PubSub component.

### Mutations

I lifted mutations directly from VueX. They are functions you define that accept a payload and make changes to state. You don't change state outside of mutations and you only call mutations via the <span class="inlineCode">commit()</span> function. None of this is strictly enforced since I'm making this library for myself. But that's how it's supposed to work.

## Summation

That was a brief introduction on how I put together a simple state management system. I plan to use it in upcoming game projects. It could be used in web development projects as well, but I'd probably want to roll my own 2-way binding and virtual dom to go along with it. If you'd like to read a better article with a similar take, <a href="https://css-tricks.com/build-a-state-management-system-with-vanilla-javascript/">check out this one on CSS Tricks</a>.

