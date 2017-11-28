# Heroku buildpack: Erlang

This is another Heroku buildpack for Erlang apps. It uses [Rebar](https://github.com/rebar/rebar) or [Rebar3](https://github.com/rebar/rebar3).

Which build tool to use is automatically detected.  Rebar is currently the default.  If either `rebar3` or `rebar.lock` are present, Rebar3 will be used. 

### Configure your Heroku App

    $ heroku config:add BUILDPACK_URL="https://github.com/madcat78/heroku-buildpack-erlang.git" -a YOUR_APP

or

    $ heroku create --buildpack "https://github.com/madcat78/heroku-buildpack-erlang.git"

### Select an Erlang version

The Erlang/OTP release version that will be used to build and run your application is now sourced from a dotfile called `.preferred_otp_version`. It needs to be the branch or tag name from the http://github.com/erlang/otp repository, and further, needs to be one of the versions that precompiled binaries are available for.

When you fail to specify the version, the version marked with a `*` will be used. this may vary per stack.

Currently supported OTP versions:

heroku-16:

* OTP-20.1 *

To select the version for your app:

    $ echo OTP-20.1 > .preferred_otp_version
    $ git commit -m "Select 20.1 as preferred OTP version" .preferred_otp_version

### Build your Heroku App

    $ git push heroku master

You may need to write a new commit and push if your code was already up to date.

NOTE: You need to have either an ebin/ directory or rebar.config checked into Git in order for Heroku to identify this project as an Erlang app it can build.

