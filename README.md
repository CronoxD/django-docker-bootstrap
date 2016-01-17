# django-docker-bootstrap

## Concept
The main idea behind this project to create an easily configurable and easy to use django
development/production environment for any project.

## Installation
* Install the docker,docker-compose - https://docs.docker.com/engine/installation/
* Build the images: ```bash buildall.sh```
* Start the project: ```docker-compose up ```
* If you want to run the project in dev mode you need to set the following environment variable:         
    * ```COMPOSE_FILE="dev-docker-compose.yml"```
    * https://docs.docker.com/compose/reference/overview/#compose-file

## Tips & Tricks
* Every image has a container_shared directory linked as a volume, so if you want to put something inside the container, or
you want to get something from inside the containers like a backup file you just need to copy everything to this directory.
* Create a bash alias for for the docker-compose by edit the ```.bash_aliases``` file ```alias dc='docker-compose'```
* If you want to use sudo inside the container you need to anter as a root: ```dc run --rm django shell root```

## Images


1. base
 * Contains every data(db, files, logs) and connected to every other container as a volume (/data/).
 * If you delete the base container you will lose everything (be cautious)
 * Commands:
   * shell - start a bash shell ```dc run --rm data shell```
2. postgres
 * postgresql-9.4
 * Commands:
    * shell - start a bash shell ```dc run --rm postgres shell```
    * backup - create a backup (```/data/backup/<backup_name>```) ```dc run --rm postgres backup```
    * restore - restore from a backup (```/data/backup/<backup_name>```) ```dc run --rm postgres restore```
3. django-python3
 * The projects can be found under the /src/ directory
 * Installed Apps:
    * Django: 1.9.1
    * uWSGI: 2.0.12
    * psycopg2: 2.6.1
    * django-debug-toolbar: 1.4
 * Commands:
   * shell -start a bash shell ```dc run --rm django shell```
4. nginx
 * Commands:
   * shell -start a bash shell ```dc run --rm nginx shell```

### Environmental variables (env.txt):
First you need to create a ```env.txt``` in the root and set the followings:
```
DJANGO_SECRET_KEY=
DB_PASSWORD=
DEBUG=
ALLOWED_HOSTS=
```
