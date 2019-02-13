---
title: "State Management in Javascript"
date: 2019-02-12T13:34:46-06:00
draft: false
---

I've gotten a bit tired of dependencies. Perhaps that's a bit ironic for somebody who does most of his work using javascript frameworks. But after spending yet another chunk of hours trying to upgrade [Angular](https://angularjs.org/) I've come to think there must be a better way of building software that doesn't involve 1000s of <span class="inlineCode">node_modules</span> dependencies.

At the same time I've been thinking about programming games in Javascript. This isn't exactly a new idea in 2019, but after 10 years of web development I still haven't made a game. Games are the reason computers were invented, so it makes sense to start creating my own.

A basic component of any software is a state management system. We all know things like [Redux](https://redux.js.org/), [MobX](https://mobx.js.org/), [VueX](https://vuex.vuejs.org/) exist and do the job of state management well. But after years of front-end dev and [Drupal](https://www.drupal.org/) work, I'm sick of sorting out errors deep within the guts of a framework or the tedium of coming back to a project and needing to upgrade all the dependencies to get started working. So I decided a first step in making games would be to roll my own [state management library](https://github.com/tmbritton/state-manager).

I wanted two things in a state management system, a pubsub component for events and a centralized data store. Also, to completely contradict my opening statement about dependencies, I wrote it in [Typescript](https://www.typescriptlang.org/). I've been using it at work recently and I find I really like the autocomplete features it provides to the text editor when you define your types.

I first created the [PubSub module](https://github.com/tmbritton/state-manager/blob/master/src/pubsub/PubSub.ts). As you can see in the link to the code I provided, there are just a few methods. The meat of it are the <span class="inlineCode">publish()</span> and <span class="inlineCode">subscribe()</span> methods. A basic use of this module is in the tests. Yes, I actually tested a personal project!

    test("Publishing an event", () => {
        const type = "test";

        PubSub.subscribe(type, (payload) => {
            expect(payload.test).toBe(2);
        });

        PubSub.publish(type, {test: 2});
    });

Basically you subscribe to an event type, this case the type is "test". Then you publish an event of the same type with a payload object. This object is then passed to the callback provided to the subscribe method and it acts on the payload. Simple, right?



