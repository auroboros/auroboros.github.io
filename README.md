auroboros is an organization founded by [John McGill](https://github.com/fat0wl) to provide a coherent set of libraries dedicated to signal processing. Currently these libraries are written in Scala, but an auxiliary goal of the project is to provide a set of very basic components to make it fundamentally easier to work with audio on the JVM (allowing library developers to provide higher-level syntax in the language of their choice built on top of these core utilities).

auroboros' libraries are:

### [signal-z](/signal-z)

A generic signal-processing core providing fundamental type algebra related to signal processors. signal-z defines traits that can be extended to decorate very minimal classes (closures for state transformation functions, essentially) with various signal flow paradigms.

### [scalaudio](/scalaudio)

An audio-processing library based on signal-z designed to wrap the Java Sound API in more productive syntax, resulting in an elegant DSL for audio synthesis & music composition in general.

### [scalim](/scalim)

A very experimental library for image/video processing.
