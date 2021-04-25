# Atlas

Atlas is an opinionated [cookiecutter](https://cookiecutter.readthedocs.io/en/latest/) template for bootstrapping Python/Django based projects.

It uses [Poetry](http://poetry.eustace.io/) as its package manager however, it also uses Docker, so while poetry resolves dependencies on your local machine, they need to be exported to requirements.txt so that the Docker containers can be built and run.

Atlas projects use `make` to run various commands to help you run your project, there are several rules configured by default (although you are free to continue adding your own), please see the Makefile for the available rules.

Atlas also runs `git init` on your newly generated project ready for you to start committing,
with that in mind it also installs a git-precommit hook that ensures upon each commit that your
requirements.txt file is kept up to date with poetry and that both `make lint` & `make test`
are ran.

## Usage

There is an example env file than can be renamed to .env after your changes are added to the file.

### Setup

    cookiecutter atlas
    cd <project_name>
    <edit .env file>
    make env
    make start
    make migrate
    make createsuperuser
    
    
### Working

    make env
    make start
