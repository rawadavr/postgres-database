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
