heroku-buildpack-imagemagick
=================================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for vendoring the ImageMagick binaries into your project.

## How it works
Rather than pulling down binary dependencies from a package manager and extracting them into place, this buildpack compiles Imagemagick from source the first time an app is built with it. The compiled binaries are cached for future builds, so this penalty is only incurred once.

This has the downside of a (potentially very long) deploy time for the first push, with the benefit of a less-fragile build product that's somewhat less likely to break due to platform and dependency shifts. Or at least, that's the hope!

## Stack compatibility
This buildpack is tested primarily against the `cedar-14` stack. Currently, a workaround is required to make it work on the newer `heroku-16` stack - see https://github.com/ello/heroku-buildpack-imagemagick/pull/17 for details.

## Note on Heroku config
Optionally, set the ImageMagick version in a Heroku config like this:

```
heroku config:set IMAGE_MAGICK_VERSION=7.0.5-0
```

Make sure the version you're referencing exists on as a `.tar.xz` file amon the [ImageMagic releases](http://www.imagemagick.org/download/releases/).

(Buildpack developer note: the config setting does not show up in the compile script as an environment variable, and has to be read from a file in `$3`, as explained in the [Heroku buildpack docs](https://devcenter.heroku.com/articles/buildpack-api#bin-compile-summary).)

The above was reconstructed from this PR https://github.com/ello/heroku-buildpack-imagemagick/pull/16 as the original fork was removed from GitHub.
