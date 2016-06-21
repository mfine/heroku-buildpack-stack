# [Heroku Buildpack for Stack][1]

[Heroku buildpack][2] for [Stack][3]. Based on the excellent [heroku-buildpack-ghc][4]

### Useage

Create an app with this buildpack:

    $ heroku create --buildpack https://github.com/mfine/heroku-buildpack-stack.git

Set this buildpack on an exiting app:

    $ heroku buildpacks:set https://github.com/mfine/heroku-buildpack-stack

Interpolating Environment Variables in `stack.yaml`:

1. Create a `stack.vars` file at the project root
1. Enter the environment variables you would like to replace, one per line
1. In the `stack.yaml`, reference the variables by surrounding them with two curly braces like this: `{{<ENV_VAR>}}`


[1]: https://github.com/mfine/heroku-buildpack-stack
[2]: http://devcenter.heroku.com/articles/buildpacks
[3]: https://github.com/commercialhaskell/stack
[4]: https://github.com/begriffs/heroku-buildpack-ghc
