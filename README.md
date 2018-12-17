# Reactive Spring: In a Nutshell

## Motivation
It took me quite a while to wrap my head around all the new terminology and all the new hype around the development paradigm of **Reactive Programming**, this was specially hard when it was introduced in the **Spring Framework**. Being an engineer with over 6 years of working with Java and Spring, I thought this would be just an increment to how we write usual Spring code with not much change.

But just as **Spring Boot** was a radical change to how we design-develop-deploy our **Java** apps, reactive programming was nothing short of that.

## What does Reactive mean?

With the rise of the **microservices** architecture pattern, and real-time updates becoming the norm, traditional synchronous development or even traditional asynchronous development were no longer acceptable. We need to process millions of records and get updates in near-real-time fashion without destroying the user experience. We now can't keep polling for updates and scanning records of data hoping to find a change.

We also want our apps to be able to handle a lot requests without wasting a lot of time being idle while waiting for I/O requests.

Enter Reactive Programming. And as always nothing new discovered, we have been using the reactive programming pattern in all of our apps, just not at this scale and not with this broader definition. If you have ever stumbled upon an `Observer` and an `Observable`, and if you have seen the method `notifyObservers(event)`, then you most likely already know how reactive programming works.

Reactive Programming is simply laying the resposiblity of publishing the data updates to the data handlers and not the data listeners, what this means is that instead of asking for data, we can _subscribe_ as _observers_ to a data _stream_ or _flux_ and get notified anytime the data has changed. The word **Reactive** or the notion of _reacting_ stems from that idea, we no longer ask for updates, we _react_ to changes by listening to events.
