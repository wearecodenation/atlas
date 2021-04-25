.PHONY: env clean start stop build test requires lint docs superuser migrate migrations createsuperuser
.DEFAULT: env

env:
	@python -m venv .venv
	@poetry install

clean:
	@rm -rf .venv

start:
	@docker-compose up -d

stop:
	@docker container stop {{cookiecutter.project_repo_name}}_web_1
	@docker container rm {{cookiecutter.project_repo_name}}_web_1
	@docker container stop {{cookiecutter.project_repo_name}}_database_1
	@docker container rm {{cookiecutter.project_repo_name}}_database_1

build:
	@docker-compose build

test:
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 coverage run --branch -m unittest discover --pattern=tests/*.py
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 coverage html

requires:
	@poetry export --dev -f requirements.txt --output requirements.txt

lint:
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 isort --virtual-env .venv {{cookiecutter.project_repo_name}}/*.py
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 black . --exclude migrations

docs:
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 /bin/bash -c "sphinx-apidoc -f -o docs/source/ {{cookiecutter.project_repo_name}} ./tests/*.py && cd docs && make html"

superuser:
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 python manage.py createsuperuser

migrate: start
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 python manage.py migrate

migrations:
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 python manage.py makemigrations

createsuperuser:
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 python manage.py createsuperuser --noinput
