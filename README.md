# Dockerize Ruby on Rails Application

Boilerplate files for deploying simple Rails application in production using Docker.

## Requirements

- Separate running container with **jwilder/nginx-proxy** (using external rev-proxy network).
- Separate running container with **postgresql** (using external net-pg network).
- config/database.yml should depend on environmental variables.
- Postgresql should have role with createdb, login and password. 

## Installation

Copy/clone repository into the main application's directory:

```
...
- app
- bin
- config
- config.ru
- db
- docker-rails-production
  - docker-compose.yml.example
  - Dockerfile.example
  - entry-point.sh.example
  - .env-app.example
  - .env.example
  - .env-webserver.example
  - nginx.conf.example
  ...
- Gemfile
- Gemfile.lock
- .git
- .gitignore
- lib
- log
- public
- Rakefile
...
```

Rename `docker-rails-production` directory to `docker-production`.

Edit all `*.example` files and rename them by deleting `.example` extentions.

## Deploying app

In the main app's directory

```
docker build -t mynick/my-app-name:1.0.0 -f docker-production/Dockerfile .
```

Then enter the docker-production directory

```
cd docker-production
```

Update the app image name in the docker-compose.

Then start the services

```
docker-compose up -d
```

## Flaws

This early version can't serve static files by nginx and it leaves it for rails server.