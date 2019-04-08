# passport-oauth2

General-purpose OAuth 2.0 authentication strategy for [Passport](http://passportjs.org/).

[![npm](https://img.shields.io/npm/v/passport-oauth2.svg)](https://www.npmjs.com/package/passport-oauth2)
[![build](https://img.shields.io/travis/YuriKovalchuk/node-passport-oAuth.svg)](https://travis-ci.org/YuriKovalchuk/node-passport-oAuth)
[![coverage](https://img.shields.io/coveralls/YuriKovalchuk/node-passport-oAuth.svg)](https://coveralls.io/github/YuriKovalchuk/node-passport-oAuth)
[...](https://github.com/YuriKovalchuk/node-passport-oAuth/wiki/Status)

## Install

    $ npm install passport-oauth2

## Usage

#### Configure Strategy

The OAuth 2.0 authentication strategy authenticates users using a third-party
account and OAuth 2.0 tokens.  The provider's OAuth 2.0 endpoints, as well as
the client identifer and secret, are specified as options.  The strategy
requires a `verify` callback, which receives an access token and profile,
and calls `cb` providing a user.

```js
passport.use(new OAuth2Strategy({
    authorizationURL: 'https://www.example.com/oauth2/authorize',
    tokenURL: 'https://www.example.com/oauth2/token',
    clientID: EXAMPLE_CLIENT_ID,
    clientSecret: EXAMPLE_CLIENT_SECRET,
    callbackURL: "http://localhost:3000/auth/example/callback"
  },
  function(accessToken, refreshToken, profile, cb) {
    User.findOrCreate({ exampleId: profile.id }, function (err, user) {
      return cb(err, user);
    });
  }
));
```

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'oauth2'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

```js
app.get('/auth/example',
  passport.authenticate('oauth2'));

app.get('/auth/example/callback',
  passport.authenticate('oauth2', { failureRedirect: '/login' }),
  function(req, res) {
    // Successful authentication, redirect home.
    res.redirect('/');
  });
```

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2011-2016 Nikolay Kovalchuk 


