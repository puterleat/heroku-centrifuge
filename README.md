heroku-centrifuge
=================

This is a simple recipe for deploying Python [Centrifuge](https://github.com/FZambia/centrifuge)
on [Heroku](https://heroku.com/) PaaS.

Centrifuge is an Open Source real-time messaging backend similar to
[Pusher](http://pusher.com/), [Pubnub](http://www.pubnub.com/) or [Faye](http://faye.jcoglan.com/).

The end result will look like
[centrifuge.herokuapp.com](https://centrifuge.herokuapp.com/) (admin password: ``password``).


## Create Heroku app

Clone this repository or copy files to a new git repo and provision a new Heroku app.

```
heroku apps:create app-name
```

## Provision Heroku services

Start with provisioning dev service plans.

Add PostgreSQL addon:

```
heroku addons:add heroku-postgresql:hobby-dev
```

Promote created Postgres Database to default db:

```
heroku pg:promote HEROKU_POSTGRESQL_*_URL
```

If you want to use Redis engine add Redis:

```
heroku addons:add redistogo
```

## Configure centrifuge

Update `Procfile` if you want non-single instance deployment.

You can look up RedisCloud host, port and password (skip username)
using ``heroku config`` command.

Do the same for ``centrifuge.json`` and amend the file:

```json
{
    "password": "password",
    "cookie_secret": "secret",
    "api_secret": "secret"
}
```

## Deploy to Heroku

```
git push heroku master
heroku logs --tail
```

## Navigate to admin panel

Go to *app-name.herokuapp.com* and configure project settings as
described in
[centrifuge.readthedocs.org](https://centrifuge.readthedocs.org/en/latest/content/web_interface.html)


## Contribute

Contribute to Centrifuge at [github.com/FZambia/centrifuge](https://github.com/FZambia/centrifuge).

Open pull requests to send updates for the heroku-centrifuge recipe.
