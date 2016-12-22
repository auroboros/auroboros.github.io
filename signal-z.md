[github](https://github.com/auroboros/signal-z) :: [mvn central](https://mvnrepository.com/artifact/org.auroboros/signalz_2.11)

If you're using SBT, add the following line to your build file:

```scala
libraryDependencies += "org.auroboros" %% "signalz" % "0.0.1"
```

### so what is signal-z?
A generic signal-processing “core”, this library aims to abstract the fundamental algebra of DSP into an implementation-agnostic framework. Implementors may then extend its types for use with any signal medium (audio, video, pure data, anything else?). Having an abstracted core also allows implementing libraries to be decorated with a number of different processing models (purely functional, streams, perhaps reactive streams) which can be updated and enhanced without necessarily even requiring any refactoring to the implementing libraries. One of the upcoming goals of this library will also be to normalize the time-domain for simultaneously using multiple mediums that operate at independent rates.

### how do I use signal-z?
Many users will not directly depend on signal-z, as it is a a transitived dependency of both scalaudio & scalim. An implementor of a signal processing library for another medium (market data, for example) may build their implemenation atop signal-z. However, implementors of custom signal processing units for scalaudio or scalim will probably want to extend signal-z's types, as they provide a variety of decorator functions for initializing signal processing units within a variety of signal processing paradigms.

### so what exactly are these signal processing paradigms?
Currently there are 2 models: functional and streaming. The functional model involves composing signal processing units using pretty vanilla Scala function composition (this can be achieved using .andThen, but typically I prefer to add scalaz as an additional dependency to do functor-based composition.
