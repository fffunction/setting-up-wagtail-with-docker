# Starting a Wagtail build

## Prerequisites

- [Docker Toolbox](https://www.docker.com/docker-toolbox)

## Steps

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

## Config changes

> ... Compressor problems with whitenoise on admin css?

## Set up for Dokku deployment

> Procfile, dokku plugins, .env, 

___

## Misc

### dj_database_url config

```python
DATABASES = {
    'default': dj_database_url.config()
}
```
