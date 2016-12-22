scalim is currently in pre-release (basic POCs, not available anywhere except github) but may have a snapshot release in the near future. 

The major issues with scalim are:

1. What is the fundamental data structure of audio/video processing? 
    * Assuming it would be some buffered RGBA plane, then must visual data always be normalized to this even if the applied processing doesn't necessarily require uniform access to the whole plane (lazy/eager loading)? 
    * Perhaps design should focus on advanced wrapper types to facilitate these lazy planes
2. [Processing](https://processing.org/) already does a fair job of image processing on the JVM. 
    * Should I just use their core data types but extend it with a scalaudio-like signal processing paradigm rather than replicating their core code?
    * scalaudio has some utility classes informed by JSyn's core but the surface area of these was much less and they lent themselves to rewrites as pure functions
    * Decision on this can be deferred until Processing & interaction with scalim is studied a bit more
