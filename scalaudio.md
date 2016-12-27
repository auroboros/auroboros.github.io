---
categories: scalaudio
---
[github](https://github.com/auroboros/scalaudio) :: [mvn central](https://mvnrepository.com/artifact/org.auroboros/scalaudio-amp_2.11)

If you're using SBT, add the following line to your build file:

```scala
libraryDependencies += "org.auroboros" %% "scalaudio-amp" % "{{ site.scalaudio-current-version }}"
```

## Quickstart
Add the line above to build.sbt and begin composing/synthesizing. The following examples use function composition via [scalaz](https://github.com/scalaz/scalaz) but if you are fluent in Scala you may know many more ways to achieve this (.andThen, for one), so scalaz is not a transitive dependency of scalaudio. Therefore, your build.sbt should look like this if you'd like to follow along.

```scala
libraryDependencies ++= Seq(
  "org.auroboros" %% "scalaudio-amp" % "{{ site.scalaudio-current-version }}",
  "org.scalaz" %% "scalaz-core" % "{{ site.scalaz-current-version }}"
)
```

#### Simple sine oscillator

```scala
import scalaz._
import Scalaz._

object MyFirstSynthComposition extends App with AmpSyntax {

    // Create audio context using all default settings except for specified single out channel
    implicit val audioContext = AudioContext(ScalaudioConfig(nOutChannels = 1))

    // Create a function that produces a "frame" (Array[Double] where array length is number of out channels)
    val frameFunc = Sine.asFunction(OscState(0, 440.Hz, 0)) // .asFunction is a convenience method from signalz that accepts initial state & produces a state-processing function
      .map(oscState => Array(oscState.sample))

    // a frameFunc or stream of frames can be played directly via implicit conversion to a "signal processing graph" type a la:
    // frameFunc.play(5 seconds)
    // but using the playback helper automatically appends speaker output to the function
    playback(frameFunc, 5 seconds)
}
```

## modules
scalaudio contains several modules but currently the only published modules are _scalaudio-amp_ and _scalaudio-core_. In a future release, these may be merged as the code is more and more simplified due to the framework provided by signal-z but for now the core contains most of the static utility code + context whereas _amp_ provides all of the audio signal processing units (unitgens, filters, etc.). At the time of writing, I don't see much chance of someone using _core_ without _amp_ and since _amp_ depends on _core_, I simply showed how to include _amp_ above. If someone is interested in making another audio processing library for the JVM, I would love to collaborate to make _core_ into a true set of utilities (or extract a utility module) for JVM audio access / byte-conversion / Midi parsing / etc. This could even be done in Java if it being in Scala is a hindrance to interoperability.
