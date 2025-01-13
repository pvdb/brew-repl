# brew-repl

The [generic, command-agnostic `repl` utility][pvdb/repl] can be installed as a `brew` external command, after which it can be used as a regular `brew` subcommand.

```sh
$ brew repl
"brew %s" >> update
...
"brew %s" >> outdated
...
"brew %s" >> info gh
...
"brew %s" >> upgrade
...
"brew %s" >> cleanup
...
"brew %s" >> ^D
$ _
```

As illustrated above, it provides a generic REPL environment that can be used to interact with `brew` in a more interactive way than the regular `brew` command-line tool allows.

## installation

`brew-repl` is installed as a symlink to the generic `repl` command-line utility and therefore requires that `repl` is installed on your system first.

`repl` itself comes in two flavors: a Ruby version and a Go version, so you have the choice between the two, depending on which language runtime you prefer to have installed on your system; both versions are functionally equivalent.

First, install the latest version of the [generic `repl` utility][pvdb/repl] in a directory that is on your `PATH`; you can adjust `REPL_INSTALL_DIR` in the below instructions to match your shell environment.

Next, in the same directory on your `PATH` where `repl` is installed, create a symlink named `brew-repl` to the `repl` utility; that way you can run `brew repl` without any changes to your system's `$PATH`.

### (option 1) if `repl` is already installed

Create `brew-repl` as a symlink to `repl`:

    REPL_INSTALL_DIR=/usr/local/bin
    ln -s "${REPL_INSTALL_DIR}/repl" "${REPL_INSTALL_DIR}/brew-repl"

You can now run `brew repl` in the same way you invoke any other `brew` subcommand.

### (option 2) install the Ruby version of the `repl` utility

[`repl.rb`][repl.rb] is the Ruby version of the `repl` utility, which requires Ruby to be installed on your system, but has no other external dependencies _(that is: it only uses classes and modules from [Ruby's standard library](https://docs.ruby-lang.org/en/master/standard_library_md.html))_.

    REPL_INSTALL_DIR=/usr/local/bin
    curl -s -O https://raw.githubusercontent.com/pvdb/repl/main/repl.rb
    mv ./repl.rb "${REPL_INSTALL_DIR}/repl"
    chmod 755 "${REPL_INSTALL_DIR}/repl"
    ln -s "${REPL_INSTALL_DIR}/repl" "${REPL_INSTALL_DIR}/brew-repl"

Finally, ensure and check that `brew-repl` is executable

    brew-repl --version

With `rlwrap` installed, and for the Ruby version of `repl` this will be something like:

> `repl 1.0.0 (rlwrap 0.46.1, ruby 3.3.6)`

### (option 3) install the Go version of the `repl` script

[`repl.go`][repl.go] is the Go version of the `repl` utility, which requires Go to be installed on your system, but has no other external dependencies _(that is: it only uses packages from [Go's standard library](https://pkg.go.dev/std))_.

    REPL_INSTALL_DIR=/usr/local/bin
    curl -s -O https://raw.githubusercontent.com/pvdb/repl/main/repl.go
    go build -o "${REPL_INSTALL_DIR}/repl" repl.go
    rm repl.go
    chmod 755 "${REPL_INSTALL_DIR}/repl"
    ln -s "${REPL_INSTALL_DIR}/repl" "${REPL_INSTALL_DIR}/brew-repl"

Finally, ensure and check that `brew-repl` is executable

    brew-repl --version

With `rlwrap` installed, and for the Go version of `repl` this will be something like:

> `repl 1.0.0 (rlwrap 0.46.1, go1.23.5)`

## usage

Once installed, a `brew` REPL can be launched using `brew repl` (or less commonly as `brew-repl`).

Running `brew repl [args]` is equivalent to running `repl brew [args]`, which means that `brew` is the default command that is invoked in the REPL environment.

It also means that it supports all the same command-line options as the `repl` utility itself, which can be used to customize the REPL environment to your liking

Use `brew-repl --help` or else go to the full documentation of [the `repl` utility][pvdb/repl] for more information.

## (optional) add `readline` support to `repl`

The `repl` utility wraps itself in [`rlwrap`][rlwrap] if it is installed on your system.

`rlwrap` is a GNU `readline` wrapper that provides command history and line editing capabilities for any command-line tool that lacks these features.

## example

Coming soon

## generate a `brew`-specific completion file for `repl`

```sh
brew commands | egrep '^[^ ]+$' > ${HOME}/.repl/brew
```

The default `repl` completion directory is `${HOME}/.repl/` but can be overridden by setting the `REPL_COMPLETION_DIR` environment variable _(in your shell environment or else in `$(HOME)/.replrc`)_.

[pvdb/repl]: https://github.com/pvdb/repl
[rlwrap]: https://github.com/hanslub42/rlwrap

[repl.rb]: https://raw.githubusercontent.com/pvdb/repl/refs/heads/main/repl.rb
[repl.go]: https://raw.githubusercontent.com/pvdb/repl/refs/heads/main/repl.go
