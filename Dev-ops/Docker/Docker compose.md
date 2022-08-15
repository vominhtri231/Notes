# Docker compose

Usually, containers would have multiple dependencies and setups. E.g. A web server would need database setup, port exposed, bind volumes, etc. 

=> Docker compose would reduce the amount of work when trying to run the services, mostly used in development.

## `docker-compose.yml`

The blueprint for setting up the services. By default, the config file would be named `docke-rcompose.yml` but can be overrided via `-f` options.

```yaml
services:
  proxy:
    # `docker-compose up` would build the image if it is not found
    # To build the image if there is any chagnes, use `docker-compose build` or `docker-compose up --build`
    build:
      context: . # where to build the image
      dockerfile: nginx.Dockerfile # docker file name - by default is `Dockerfile`
    ports: # export the port
      - '80:80'
    volumes: 
      - ./nginx.conf:/etc/nginx/conf.d/default.conf # mount container directory to host directory
  web:
    image: httpd:2  # specify image name
  web-postgres:
    image: postgres:14.3
    environment: # specify environment variable for the container
      - POSTGRES_DB=drupal
      - POSTGRES_USER=tri
      - POSTGRES_PASSWORD=Tri123
    volumes:
      - postgres-data:/var/lib/postgresql/data # mount container directory to volume

volumes: # create volumes
  postgres-data:

networks: # create networks
# All services create via a docker-compose file would be in the same default network by default.
```

## docker-compose cli

The docker-compose cli would connect to docker cli for creating services, volumes or networks, etc.

It would have most of the docker cli command, and 2 additional commands:

- `docker-compose up` for creating services, volumes, networks, etc
- `docker-compose down` for deleting serives, volumes, networks, etc