### Question

Reagent looks terrific.  Why do I need re-frame?  Does it add extra layers and
conceptual overhead for not much benefit?

### Answer 

First, I agree, Reagent is terrific. If your application is small and simple, 
then standalone Reagent is absolutely a fine choice.

But it does only supply the V part of the traditional MVC triad. As a result, when
your application starts to get bigger and more complicated, you will need to 
find solutions to questions in the M and C realms - like "where does the control logic go?".  And, 
"how do I manage state".  And, coordination issues like "How do I put up a spinner
when waiting for the database, and take it down correctly?".  How do I ensure 
efficient view updates?  How do I write my control logic in a way that's testable. 

These questions accumulate. Reagent, by itself,
provides little guidance and, so, you'll need to
come up with your own solutions. The choices you make will accumulate too and,
over time, will become baked into into your code base,
becoming increasingly difficult to revisit. 

Now, any decision which is hard to revisit later is an architecture decision - that's 
pretty much the definition of architecture.  So, as you proceed, baking your
decisions into your code base, you will be incrementally growing an architecture.

So, then, the question becomes: is your architecture better than re-frame's?  Because 
that's what re-frame gives you ... an architecture ... answers to the
various questions you'll face when developing your app.  

Now, in response, some will enthusiastically say "yes, I want to grow my own architecture". 
Fair enough - its a fun ride!

I think the only danger arises if this process is not conscious and purposeful - if
someone gets going quickly with Reagent and has a bunch of enjoyable early wins, but
ends up in the weeds because they didn't understand the road they were driving as
their application got bigger.

I've had many people (20?) privately say to me that's what happened to them. The real
number would obviously be much higher. And that's pretty much the reason for
this FAQ - this happens a bit too often.  

So, my advice is ... if your application is a little more complicated,
be sure to make a conscious choice around architecture, because one way or
another you'll be using one.  If your application is beyond a few thousands lines
of code, and you are using only Reagent, you **will** end up creating your own "alternative re-frame".

### Some Choices Made By re-frame

1. Events as data  (which means they are loggable, and can be queued, etc)
2. Events are handled async  (critical, requires carefully engineering, no core.async!)
3. For efficiency, subscriptions (reactions) should be layered and de-duplicated
4. Views are never imperative or side effecting
4. Unidirectional data flow only, ever
5. Interceptors over middleware. Provide cross cutting concerns like logging and debugging. 
6. Event handlers capture control and contain key code. Ensure purity via coeffects and effects. 
7. State is stored in one place and is committed-to transactionally. 

Hmm. I feel like I'm missing a couple, but that's certainly indicative. 

### What Reagent Does Provide

Above I said:
> Reagent, by itself, provides little guidance ...

which is true but, it does provide useful building blocks. If you do want to create 
your own architecture, then be sure to check out Reagent's `track`, `reaction` and `rswap`. 

There's also other Reagent-based architectures like [keechma](https://github.com/keechma/keechma) and 
[carry](https://github.com/metametadata/carry) which make different choices - ones which may 
suit your needs better.

***

Up:  [FAQ Index](README.md)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
<!-- END doctoc generated TOC please keep comment here to allow auto update -->