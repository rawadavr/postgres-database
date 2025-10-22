# Basic Readme
This repo will represent containerizing the sql database portion of the work for the vrevent-manager

# Commands
# init container
docker run --name <name of container> -e POSTGRES_PASSWORD=<password here> -d -p 5432:5432 <Name of db>

# enter container
docker exec -it <name of container> bash

# connect to database
psql -U <Name of db>

# DEFAULT docker data is ephermeral, will go bye bye with no persistent volumes
# create volume
docker volume create <name of volume>

# run container with volume
docker run --name <name of container> -e POSTGRES_PASSWORD=<password here> -d -p 5432:5432 -v <name of volume>:/var/lib/postgresql/data <name of DB>

# create docker-compose to set up container with postgres
    version: '3.8' -> docker-compose version
    services: -> defines containers in app
      db: -> service named db for app
        image: postgres:<tag> -> docker image to use and tag version
        restart: always -> configure container with restart options
        environment: -> set env vars for container
          POSTGRES_DB: <database name>
          POSTGRES_USER: <database user>
          POSTGRES_PASSWORD: <user password>
        ports:
          - "5432:5432" -> <host port>:<container port> 
        volumes: -> mounts named volume to persist data
          - <volume name>:/var/lib/postgresql/data -> creates DB volume <volume name> and mounts it

    volumes:
      <volume name>: declares named volume
