# [Heroku Buildpack for Stack][1]

[Heroku buildpack][2] for [Stack][3]. Based on the excellent [heroku-buildpack-ghc][4]

### Usage

Create an app with this buildpack:

    $ heroku create --buildpack https://github.com/mfine/heroku-buildpack-stack.git

Set this buildpack on an exiting app:

    $ heroku buildpacks:set https://github.com/mfine/heroku-buildpack-stack

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

[1]: https://github.com/mfine/heroku-buildpack-stack
[2]: http://devcenter.heroku.com/articles/buildpacks
[3]: https://github.com/commercialhaskell/stack
[4]: https://github.com/begriffs/heroku-buildpack-ghc
