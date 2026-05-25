# Instructions append
## Arturo-specific Instructions

Unlike most Arturo exercises, `src/grep.art` will not be directly imported by the test suite.
Instead, your solution will be run as a standalone Arturo script, receiving a series of command-line arguments.
You can use `arg`[arg] or `args`[args] to access these command-line arguments, which contain zero or more flags, a search pattern, and one or more filenames.
These files are created and populated by the test suite at runtime.
Your solution will need to read the requested file and write the expected output to standard output.

[arg]: https://arturo-lang.io/documentation/library/system/arg
[args]: https://arturo-lang.io/documentation/library/system/args
