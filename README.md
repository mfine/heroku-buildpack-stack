# [Heroku Buildpack for Stack][1]

[Heroku buildpack][2] for [Stack][3]. Based on the excellent [heroku-buildpack-ghc][4]

### Useage

Create an app with this buildpack:

    $ heroku create --buildpack https://github.com/mfine/heroku-buildpack-stack.git

Set this buildpack on an exiting app:

    $ heroku buildpacks:set https://github.com/mfine/heroku-buildpack-stack

[1]: https://github.com/mfine/heroku-buildpack-stack
[2]: http://devcenter.heroku.com/articles/buildpacks
[3]: https://github.com/commercialhaskell/stack
[4]: https://github.com/begriffs/heroku-buildpack-ghc
