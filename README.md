# Passport-Chalkable-OAuth2

[Passport](http://passportjs.org/) strategies for authenticating with [Chalkable](http://www.chalkable.com/)
using OAuth 1.0a and OAuth 2.0.

This module lets you authenticate using Chalkable in your Node.js applications.
By plugging into Passport, Chalkable authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Install

    $ npm install passport-chalkable-oauth2

## Usage

#### Configure Strategy

The Chalkable OAuth 2.0 authentication strategy authenticates users using a Chalkable
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

    var ChalkableStrategy = require('passport-chalkable-oauth2').OAuth2Strategy;

    passport.use(new ChalkableStrategy({
        clientID: CHALKABLE_CLIENT_ID,
        clientSecret: CHALKABLE_CLIENT_SECRET,
        callbackURL: "http://127.0.0.1:3000/auth/chalkable/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ chalkableId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'chalkable'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/chalkable/callback', 
      passport.authenticate('chalkable', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Credits

  - [Jared Hanson](http://github.com/jaredhanson) for the orignial passport module, and the Google OAuth module from which this is derived.

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2012-2013 Jared Hanson <[http://jaredhanson.net/](http://jaredhanson.net/)>
