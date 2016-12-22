auroboros is an organization founded by [John McGill](https://github.com/fat0wl) to provide a coherent set of libraries dedicated to signal processing. Currently these libraries are written in Scala, but an auxiliary goal of the project is to provide a set of very basic components to make it fundamentally easier to work with audio on the JVM (allowing library developers to provide higher-level syntax in the language of their choice built on top of these core utilities).

auroboros' libraries are:

### [signal-z](/signal-z)

A generic signal-processing "core", this library aims to abstract the fundamental algebra of DSP into an implementation-agnostic framework. Implementors may then extend its types for use with any signal medium (audio, video, pure data, anything else?). Having an abstracted core also allows implementing libraries to be decorated with a number of different processing models (purely functional, streams, perhaps reactive streams) which can be updated and enhanced without necessarily even requiring any refactoring to the implementing libraries. One of the upcoming goals of this library will also be to normalize the time-domain for simultaneously using multiple mediums that operate at independent rates.

### [scalaudio](/scalaudio)

An audio-processing library based on signal-z designed to wrap the Java Sound API in more productive syntax, resulting in an elegant DSL for audio synthesis & music composition in general.

### [scalim](/scalim)

A very experimental library for image/video processing.
