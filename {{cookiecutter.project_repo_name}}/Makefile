.PHONY: build clean createsuperuser docs env lint logs migrate migrations reboot_and_log requires requires-dev start stop test
.DEFAULT: env

build:
	@docker-compose build

clean: stop
	@rm -rf .venv

createsuperuser:
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 python manage.py createsuperuser --noinput

docs:
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 /bin/bash -c "sphinx-apidoc -f -o docs/source/ {{cookiecutter.project_repo_name}} ./tests/*.py && cd docs && make html"

env:
	@poetry install

lint:
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 isort --virtual-env .venv {{cookiecutter.project_repo_name}}/*.py
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 black . --exclude migrations

logs:
	@docker logs --follow {{cookiecutter.project_repo_name}}_web_1

migrate: start
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 python manage.py migrate

migrations:
	@docker exec -it {{cookiecutter.project_repo_name}}_web_1 python manage.py makemigrations

reboot_and_log:
	@echo "Rebooting and logging, now!"
	@echo "Taking containers down"
	@make stop
	@echo "Bringing containers up"
	@make start
	@make logs

requires:
	@poetry export -f requirements.txt --output requirements.txt --without-hashes

requires-dev:
	@poetry export --dev -f requirements.txt --output requirements-dev.txt --without-hashes

start:
ifeq ($(findstring {{cookiecutter.project_repo_name}},$(shell docker container ls)),{{cookiecutter.project_repo_name}})
	@echo "{{cookiecutter.project_repo_name}} containers already running"
else
	@docker-compose up -d
endif

stop:
ifeq ($(findstring {{cookiecutter.project_repo_name}},$(shell docker container ls)),{{cookiecutter.project_repo_name}})
	@docker container stop {{cookiecutter.project_repo_name}}_web_1
	@docker container rm {{cookiecutter.project_repo_name}}_web_1
	@docker container stop {{cookiecutter.project_repo_name}}_database_1
	@docker container rm {{cookiecutter.project_repo_name}}_database_1
else
	@echo "No {{cookiecutter.project_repo_name}} containers running"
endif

test:
	@docker exec --tty {{cookiecutter.project_repo_name}} coverage run --branch -m unittest discover --pattern=tests/*.py
	@docker exec --tty {{cookiecutter.project_repo_name}} coverage html
