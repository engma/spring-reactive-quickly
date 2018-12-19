# Reactive Spring In a Nutshell

## Motivation
It took me quite a while to wrap my head around all the new terminology and all the new hype around the development paradigm of **Reactive Programming**, this was especially hard when it was introduced in the **Spring Framework**. Being an engineer with over 6 years of working with Java and Spring, I thought this would be just an increment to how we write usual Spring code with not much change.

But just as **Spring Boot** was a radical change to how we design-develop-deploy our **Java** apps, reactive programming was nothing short of that.

## What does "Reactive" mean?

With the rise of the **microservices** architecture pattern and real-time updates becoming the norm, traditional synchronous development or even traditional asynchronous development was no longer acceptable. We need to process millions of records and get updates in near-real-time fashion without destroying the user experience. We now can't keep polling for updates and scanning records of data hoping to find a change.

We also want our apps to be able to handle a lot of requests without wasting a lot of time being idle while waiting for I/O.

Enter Reactive Programming. And as always nothing new discovered, we have been using the reactive programming pattern in all of our apps, just not at this scale and not with this broader definition. If you have ever stumbled upon an `Observer` and an `Observable`, and if you have seen the method `notifyObservers(action)`, then you most likely already know how reactive programming works.

Reactive Programming is simply laying the responsibility of publishing the data updates to the data handlers and not the data listeners, what this means is that instead of asking for data, we can _subscribe_ as _observers_ to a data _stream_ or _flux_ and get notified anytime the data has changed. The word **Reactive** or the notion of _reacting_ stems from that idea, we no longer ask for updates, we _react_ to changes by subscribing to event publishers.

For Example:
```
The user loads the page
ListUserPage --GetUserListRequest--> ReactiveUserController
The controller then calls the
UserController --LoadUsers--> ReactiveDatabaseDriver
Then releases the thread for other requests to be processed
When the database loads the data it notifies the controller
Database --UsersFlux--> UserController
The controller then returns the data to the waiting request
UserController --UsersFlux--> ListUserPage
```

## Reactive Programming in Spring

Spring implements the reactive paradigm using [Reactive Streams](https://github.com/reactive-streams/reactive-streams-jvm#reactive-streams) methodology, it uses the [Reactor](https://projectreactor.io/) project internally to provide 
the reactive functionality.

The main components of **Spring**'s reactive model are the `Mono<>` and the `Flux<>`. The `Mono<>` can be considered as a data stream that will only emit one element. In other words, consider it an open connection or a factory that is processing something and when that is ready, it will emit it. The `Flux<>` on the other hand is a stream of one or more elements of data. It could 1 or it could be an infinite number. Consider this an open connection or a factory that is constantly processing and producing things until it's source runs out or closes.

An example of a `Mono<>` is a `Mono<User>`, this is a `Mono` that will is expected to return at most one user. A method return this `Mono` is equivalent to a method returning a `User` directly, except this one is _non blocking_ and _async_. Think of it as a `CompletableFuture` but with a better interface and more tools.

A `Flux<User>` will emit users until the source of data terminates, which means that if the source never terminates, the `Flux` will keep emitting users
