### status
signal-z & scalaudio are currently available as 0.1.0 releases.
This is considered the first semi-stable release, with a fairly complete feature set (basic unit gens, filters, IO, etc.) but there are holes. For example, analysis units are incomplete and many of the "mutable" (which will be the default) versions of the ugens are unimplemented. The syntax is also perhaps a bit verbose because several design choices are being actively compared (and usually proxied as factory methods) whereas in the future the library may become more opinionated, which will probably allow more terseness.
More details (release notes, discussion of pending design decisions) can be found with the docs for each respective library.

### where can I find auroboros' artifacts/code?
Artifacts are published to [Sonatype](https://oss.sonatype.org/#nexus-search;quick~auroboros) ([search](http://search.maven.org/#search%7Cga%7C1%7Cauroboros), view on [mvnrepository index](https://mvnrepository.com/search?q=auroboros)).

The code repos are all on [github](https://github.com/auroboros).

### build details
auroboros' libraries are currently built for Scala 2.11 only, but cross-compilation is planned for future releases.

### what about snapshots?
Snapshots are published pretty regularly during development (current snapshot version is 0.1.1).

To use the snapshot versions:

* Add the Sonatype snapshot repository as a resolver.

```scala
resolvers += "Sonatype OSS Snapshots" at "https://oss.sonatype.org/content/repositories/snapshots"
```

* Specify the snapshot version of each desired lib.

```scala
libraryDependencies += "org.auroboros" %% "scalaudio-amp" % "0.1.1-SNAPSHOT" changing()
```

The _changing()_ option is not required. It prompts SBT to check for updated versions of the library during project refreshes.
