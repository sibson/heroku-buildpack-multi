# Heroku buildpack: multi

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) that
allows one to multiple other buildpacks in a single deploy process. This helps support:

1. Running multiple language buildpacks such as JS for assets and Ruby for your application
2. Running a daemon process such as [pgbouncer](https://github.com/heroku/heroku-buildpack-pgbouncer) with your application
3. Pulling in system dependencies.

## Usage

To use this buildpack you'll first need to set it as your custom buildpack:

    $ heroku config:add BUILDPACK_URL=https://github.com/heroku/heroku-buildpack-multi.git

From here you will need to create a `.buildpacks` file which contains (in order) the buildpacks you wish to run when you deploy:

    $ cat .buildpacks
    https://github.com/heroku/heroku-buildpack-nodejs.git#0198c71daa8
    https://github.com/heroku/heroku-buildpack-ruby.git#v86

### Hooks

This buildpack provides a couple of hooks, pre_build and post_build, that allow you to customize the build process.
To take advantage of this feature place one or both scripts in bin/pre_build, bin/post_build, pre_build will run as the first step before any other buildpack and post_build is run after all other buildpacks have completed.
They will be passed the BUILD_DIR and CACHE_DIR as arguments.

## License

MIT

## FAQ

