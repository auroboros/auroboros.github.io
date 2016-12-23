### status
signal-z & scalaudio are currently available as 0.0.1 release (highly experimental messy).
They are now being prepped for an 0.1.0 release which will be stable, providing consistency throughout the codebase (refactored to be conceptually streamlined) and a fairly complete feature set (basic unit gens, filters, IO, etc.).

### where can I find auroboros' libaries?
Artifacts are published to [Sonatype](https://oss.sonatype.org/#nexus-search;quick~auroboros) ([search](http://search.maven.org/#search%7Cga%7C1%7Cauroboros), view on [mvnrepository index](https://mvnrepository.com/search?q=auroboros)).

The code repos are all on [github](https://github.com/auroboros).

### build details
auroboros' libraries are currently built for Scala 2.11 only, but cross-compilation is planned for future releases.

### what about snapshots?
Snapshots are published pretty regularly during development. At this time, it's actually recommended to use the 0.1.0-SNAPSHOT versions instead of 0.0.1 since those are pretty incoherent/legacy.

To use the snapshot versions:

* Add the Sonatype snapshot repository as a resolver.

```scala
resolvers += "Sonatype OSS Snapshots" at "https://oss.sonatype.org/content/repositories/snapshots"
```

* Specify the snapshot version of each desired lib.

```scala
libraryDependencies += "org.auroboros" %% "scalaudio-amp" % "0.1.0-SNAPSHOT" changing()
```

The _changing()_ option is not required. It prompts SBT to check for updated versions of the library during project refreshes.
