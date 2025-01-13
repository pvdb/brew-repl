# brew-repl

The generic [`repl` command-line tool](pvdb/repl) can be installed as a `brew` external command, after which it can be used as a regular `brew` subcommand.

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

## installation

The `brew-repl` command is just a symlink to the generic `repl` command-line tool and therefore requires that `repl` is installed on your system first.

### #1/2 - install `repl`

Install the latest version of the [`repl` script](repl.rb) in a directory that is on your `PATH` and ensure that it is executable:

    REPL_INSTALL_DIR=/usr/local/bin
    curl -s https://raw.githubusercontent.com/pvdb/repl/master/repl.rb -o "${REPL_INSTALL_DIR}/repl"
    chmod 755 "${REPL_INSTALL_DIR}/repl"

### 2/2 - install `brew-repl`

In the same directory on your `PATH` where `repl` is installed, create a symlink named `brew-repl` to the `repl` script:

    REPL_INSTALL_DIR=/usr/local/bin
    ln -s "${REPL_INSTALL_DIR}/repl" "${REPL_INSTALL_DIR}/brew-repl"

This way you can run `brew repl` without any changes to your system's `$PATH`, but you can adjust `REPL_INSTALL_DIR` to match your shell environment.

## usage

Once installed, a `brew` REPL can be launched using `brew repl` (or less commonly as `brew-repl`).

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
