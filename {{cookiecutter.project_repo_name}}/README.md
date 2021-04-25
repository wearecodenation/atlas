# {{cookiecutter.project_repo_name}}

{{cookiecutter.project_short_description}}

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. This uses Docker and will setup a database container and a web container, please see the Makefile for more information.

## Config

You will need to write a .env file which contains the following:

* DJANGO_SETTINGS_MODULE
* SECRET_KEY
* DEBUG
* ALLOWED_HOSTS
* POSTGRES_DB
* POSTGRES_HOST
* POSTGRES_USER
* POSTGRES_PASSWORD
* DJANGO_SUPERUSER_PASSWORD
* DJANGO_SUPERUSER_USERNAME
* DJANGO_SUPERUSER_EMAIL

### Installing

Setting up an Atlas project should be as simple as:

```
make env
```

## Running the tests

```
make test
```

## Generating the documentation

```
make docs
```

## Author

* {{cookiecutter.author_name}}

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc

