# Passport-Coggle-OAuth2
[Passport](http://passportjs.org/) strategies for authenticating with [Coggle](http://coggle.it/)
using OAuth 2.0.

This module lets you authenticate using Coggle in your Node.js applications.
By plugging into Passport, Coggle authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Install
    $ npm install passport-coggle-oauth2

## Usage
#### Configure Strategy
The Coggle OAuth 2.0 authentication strategy authenticates users by their
Coggle login, and OAuth 2.0 tokens. The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

    var CoggleStrategy = require('passport-coggle-oauth2').OAuth2Strategy;

    passport.use(new CoggleStrategy({
        clientID: COGGLE_CLIENT_ID,
        clientSecret: COGGLE_CLIENT_SECRET,
        callbackURL: "http://localhost:5000/auth/coggle/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({coggle_id: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests
Use `passport.authenticate()`, specifying the `'coggle'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/coggle/callback', 
      passport.authenticate('coggle', { failureRedirect: '/request-coggle-auth' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Credits
  - [Jared Hanson](http://github.com/jaredhanson) for the original passport module, and the Google OAuth module from which this is derived.

## License
[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2012-2013 Jared Hanson <[http://jaredhanson.net/](http://jaredhanson.net/)>
Copyright (c) 2014 Coggle <[http://coggle.it](http://coggle.it)>

