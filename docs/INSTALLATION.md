# Installation

Arturo comes with pre-built binaries for Linux, MacOS, and Windows in both `full` and `mini` build flavors.
For this track, we'll be using [the nightly `full` build release of Arturo][nightly] which includes the entire standard library and mostly notably package manager support.
This full build is only supported for `x86_64` Linux and Windows platforms.

## Downloading Nightly

On the [nightly Arturo build page][nightly], find the latest `full` release for your current platform (Linux or Windows only).
The page lists the pre-built releases as `arturo_<version>-<year>-<month>-<date>-<platform>-full`.
For example, the latest `full` build for Linux as of this writing is `arturo_0.9.83-2024-06-12-linux-full`.
Download the correct release for your platform and extract the `arturo` binary from the archive.
Move that binary to a directory on your system's PATH environment variable.
Common locatons might be `/usr/local/bin` or `~/.local/bin` on Linux or perhaps `C:\arturo` on Windows.
You can verify the binary is on your PATH by running `arturo --version` at the command-line.
That should print something like `arturo v/0.9.83 b/3112 (amd64/linux)`, and the specific version and platform identifiers may be different for you.

## Running Arturo code
At that point, you're ready to start writing Arturo code!
To access the Arturo REPL interactive console, run `arturo` at the command-line.
To execute an Arturo script, run `arturo <file>` at the command-line inside.
To import packages, run `import "<package-name>"!` inside the REPL.
If the package is not already installed, Arturo will download and install the package for you.
You can find packages using [Packager, the official Arturo package registry][packager].

[nightly]: https://github.com/arturo-lang/nightly/releases
[packager]: https://pkgr.art/
