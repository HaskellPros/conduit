## 1.2.4.1

* Some documentation improvements

## 1.2.4

* [fuseBothMaybe](https://github.com/snoyberg/conduit/issues/199)

__1.2.3__ Expose `connect` and `fuse` as synonyms for `$$` and `=$=`, respectively.

__1.2.2__ Lots more stream fusion.

__1.2__ Two performance optimizations added. (1) A stream fusion framework. This is a non-breaking change. (2) Codensity transform applied to the `ConduitM` datatype. This only affects users importing the `.Internal` module. Both changes are thoroughly described in the following to blog posts: [Speeding up conduit](https://www.fpcomplete.com/blog/2014/08/iap-speeding-up-conduit), and [conduit stream fusion](https://www.fpcomplete.com/blog/2014/08/conduit-stream-fusion).

__1.1__ Refactoring into conduit and conduit-extra packages. Core functionality is now in conduit, whereas most common helper modules (including Text, Binary, Zlib, etc) are in conduit-extra. To upgrade to this version, there should only be import list and conduit file changes necessary.

__1.0__ Simplified the user-facing interface back to the Source, Sink, and Conduit types, with Producer and Consumer for generic code. Error messages have been simplified, and optional leftovers and upstream terminators have been removed from the external API. Some long-deprecated functions were finally removed.

__0.5__ The internals of the package are now separated to the .Internal module, leaving only the higher-level interface in the advertised API. Internally, switched to a `Leftover` constructor and slightly tweaked the finalization semantics.

__0.4__ Inspired by the design of the pipes package: we now have a single unified type underlying `Source`, `Sink`, and `Conduit`. This type is named `Pipe`. There are type synonyms provided for the other three types. Additionally, `BufferedSource` is no longer provided. Instead, the connect-and-resume operator, `$$+`, can be used for the same purpose.

__0.3__ ResourceT has been greatly simplified, specialized for IO, and moved into a separate package. Instead of hard-coding ResourceT into the conduit datatypes, they can now live around any monad. The Conduit datatype has been enhanced to better allow generation of streaming output. The SourceResult, SinkResult, and ConduitResult datatypes have been removed entirely.

__0.2__ Instead of storing state in mutable variables, we now use CPS. A `Source` returns the next `Source`, and likewise for `Sink`s and `Conduit`s. Not only does this take better advantage of GHC\'s optimizations (about a 20% speedup), but it allows some operations to have a reduction in algorithmic complexity from exponential to linear. This also allowed us to remove the `Prepared` set of types. Also, the `State` functions (e.g., `sinkState`) use better constructors for return types, avoiding the need for a dummy state on completion.

__0.1__ `BufferedSource` is now an abstract type, and has a much more efficient internal representation. The result was a 41% speedup on microbenchmarks (note: do not expect speedups anywhere near that in real usage). In general, we are moving towards `BufferedSource` being a specific tool used internally as needed, but using `Source` for all external APIs.

__0.0__ Initial release.
