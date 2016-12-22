[github](https://github.com/auroboros/signal-z) :: [mvn central](https://mvnrepository.com/artifact/org.auroboros/signalz_2.11)

If you're using SBT, add the following line to your build file:

```scala
libraryDependencies += "org.auroboros" %% "signalz" % "0.0.1"
```

### so what is signal-z?
A generic signal-processing “core”, this library aims to abstract the fundamental algebra of DSP into an implementation-agnostic framework. Implementors may then extend its types for use with any signal medium (audio, video, pure data, anything else?). Having an abstracted core also allows implementing libraries to be decorated with a number of different processing models (purely functional, streams, perhaps reactive streams) which can be updated and enhanced without necessarily even requiring any refactoring to the implementing libraries. One of the upcoming goals of this library will also be to normalize the time-domain for simultaneously using multiple mediums that operate at independent rates.

### how do I use signal-z?
Many users will not directly depend on signal-z, as it is a a transitived dependency of both scalaudio & scalim. An implementor of a signal processing library for another medium (market data, for example) may build their implemenation atop signal-z. However, implementors of custom signal processing units for scalaudio or scalim will probably want to extend signal-z's types, as they provide a variety of decorator functions for initializing signal processing units within a variety of signal processing paradigms.

### what exactly are these signal processing paradigms?
Currently there are 2 models: functional and streaming. 

#### Functional
The functional model involves composing signal processing units using pretty vanilla Scala function composition (this can be achieved using .andThen, but typically I prefer to add [scalaz](https://github.com/scalaz/scalaz) as an additional dependency to do functor-based composition. This model is really simplistic and neat because basically the whole "state" of the processing chain is baked into the function via closures and then we can produce a sequence of frames just by calling the function over & over.

#### Streaming
"Streaming" in this context refers to Scala streams from the standard Scala collections API. Streaming units in signal-z are also based off of processing functions, but use them as stream producers/consumers (transforming via "map" and other memory-leak "safe" functions). Streams can be difficult to manage in that standard Scala streams can cause memory leaks if a reference to the head is held, and typically there is only 1 point at which stream consumption can take place. To alleviate this, signal-z always defines streams as methods and passes them by-name rather than by value. Nevertheless, they are pretty neat (a signal processing unit produces a stream, which is given as an input stream to the next unit, etc.) and a very linear sort of analogy for signal processing especially when it comes to normalizing the time domain. Imagine it, if a stream is pattern-matched correctly within a unit that processes on signal history, it could even alleviate the need for having an internal buffer in that unit at all.

#### Possible future models...
Due to the issues mentioned above in streaming (maybe I will post some links but there are many articles that go in depth into them but they are pretty easy to find) I am considering exploring other streaming models.

1. EphemeralStream
  * scalaz provides "EphemeralStream" which does not memoize and therefore solves memory leak issues (but then isn't much more powerful than iterator then, is it?). However, I've heard it mentioned that EphemeralStream performance is 3+ times slower than the standard lib stream (need to verify).
2. Akka streams
  * Akka streams are pretty cool in that they provide a model for graph-building (composing partial graphs) can have multiple sinks, back pressure, throttling, etc. etc.
  * Need to investigate performance implications
