# [Heroku Buildpack for Stack][1]

[Heroku buildpack][2] for [Stack][3]. Based on the excellent [heroku-buildpack-ghc][4]

### Usage

Create an app with this buildpack:

    $ heroku create --buildpack https://github.com/mfine/heroku-buildpack-stack.git

Set this buildpack on an existing app:

    $ heroku buildpacks:set https://github.com/mfine/heroku-buildpack-stack

Binary executables are placed in `/app/.local/bin/` after compilation, a directory which Heroku includes in your `$PATH`, so assuming that your application is [binding to `$PORT`](https://devcenter.heroku.com/articles/dynos#web-dynos), you can serve your app by [creating a `Procfile`](https://devcenter.heroku.com/articles/procfile) at your project root that defines a `web` process type for the `executable` defined in your `.cabal` file:

    $ cat *.cabal | grep executable
    executable YOURAPPNAME-exe

    $ echo "web: YOURAPPNAME-exe" >> Procfile


### Templating stack.yaml

To avoid committing secrets into `stack.yaml` for access to private
repos, an app's config vars values can be substituted for tags
enclosed in double brackets. For example, given a `stack.yaml` containing:

    packages:
    -location:
        git: https://mfine:{{GITPASS}}@github.com/mfine/heroku-buildpack-stack.git

and an application with config vars:

    $ heroku config -app calm-storm-51595
    === murmuring-beyond-51595 Config Vars
    GITPASS: abc123
    $

before compilation, the `stack.yaml` will be substituted as follows:

    packages:
    -location:
        git: https://mfine:abc123@github.com/mfine/heroku-buildpack-stack.git


### Makefile Support

This buildpack now supports an optional Makefile, in case you need to coordinate
other build steps with Stack. It assumes that the Makefile includes a `make
install` target that uses the Stack build command with the flag `--copy-bins`.
For example, a possible `install` target configuration in the Makefile could be:

    install:
        stack build --copy-bins

[1]: https://github.com/mfine/heroku-buildpack-stack
[2]: http://devcenter.heroku.com/articles/buildpacks
[3]: https://github.com/commercialhaskell/stack
[4]: https://github.com/begriffs/heroku-buildpack-ghc
