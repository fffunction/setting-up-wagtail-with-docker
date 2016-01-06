# Starting a Wagtail build

## Prerequisites

- [Docker Toolbox](https://www.docker.com/docker-toolbox)

## Getting Running

1. Go to folder you want to start a new project in. It doesn't have to be empty.
2. Copy the `.dockerfile`, `docker-compose.yml`, and `requirements.txt` files included here into your directory.
3. In a command line, `cd` to your project folder.
4. `docker-compose build`
5. `docker-compose run web wagtail start [projectname]`
6. Move the contents of the new [projectname] folder out into the root
7. Change the database settings in [projectname]/settings/base.py to use `dj_database_url` [Link to example config](#dj_database_url-config)
8. `docker-compose run web ./manage.py migrate`
9. `docker-compose run web ./manage.py createsuperuser`
10. `docker-compose up` and your Wagtail admin will be running at `http://192.168.99.100/admin` (if you use the default docker ip)

## Custom Branding

1. Create a new app called `dashboard` to hold your custom wagtail branding templates. This is done with `docker-compose run web django startapp dashboard`
2. Copy the `dashboard/templates` folder from this repo into your own dashboard folder.
3. Point the image sources in these tempates to a logo and change `[project name]` to a suitable name.
4. Add `'dashboard'` to the `INSTALLED_APPS` in `base.py` making sure `'overextends','dashboard',` comes before `'wagtail.wagtailadmin','wagtail.wagtailcore',`.

## Config changes

> ... Compressor problems with whitenoise on admin css?

## Set up for Dokku deployment

Required files:

 - Procfile (requires pointing to the correct wsgi file)
 - runtime.txt (requires setting to correct env)
 - bin/post_compile

1. Add the dokku server to your remotes. `git remote add dokku dokku@server.com:[appname]`
2. Push to dokku. `git push dokku [currentbranch]:master`
3. On dokku configure the necessary plugins, e.g. `dokku postrgresql:create [appname]; dokku elasticsearch:create [appname]`
4. Either import a database with pgAdmin or run the `migrate` and `createsuperuser` commands details above

___

## Misc

### dj_database_url config

```python
import dj_database_url

DATABASES = {
    'default': dj_database_url.config()
}
```
