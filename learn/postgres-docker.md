Offical docs: https://github.com/docker-library/docs/blob/master/postgres/README.md

Article: [local development of postgres using docker](https://towardsdatascience.com/local-development-set-up-of-postgresql-with-docker-c022632f13ea)

Official network tutorial: https://docs.docker.com/network/network-tutorial-standalone/





#### Steps taken:

1. `docker pull postgres` 

   1. `docker images` to list all images

2. ```
   docker run -d \
   	--name dev-postgres \
   	-e POSTGRES_PASSWORD=Pass2020! \
   	-v ${HOME}/postgres-data/:/var/lib/postgresql/data \
           -p 5432:5432
           postgres
           
        
   ```

3. Postgres username: `postgres`       password: `Pass2022!`

4. PgAdmin4 password: `SuperSecret`

5.  To run a psql from terminal

   ```
   docker exec -it dev-postgres bash
   
   $ psql -h localhost -U postgres
   ```

   

6. Starting pgAdmin instance

   ```
   $ docker pull dpage/pgadmin4
   $ docker run -p 127.0.0.1:5433:80 -e 'PGADMIN_DEFAULT_EMAIL=pranay.velisoju@gmail.co' -e 'PGADMIN_DEFAULT_PASSWORD=SuperSecret' --name dev-pgadmin -d dpage/pgadmin4
   ```

   

   7. Get the ip address of the postgres container 

      ```
      $ docker inspect dev-postgres -f "{{json .NetworkSettings.Networks }}"
      ```

   8. Created a `pgnetwork`  bridge using the steadylearner's tutorial.

Network related: 

- https://www.freecodecamp.org/news/how-to-get-a-docker-container-ip-address-explained-with-examples/
- https://dev.to/steadylearner/how-to-set-up-postgresql-and-pgadmin-with-docker-51h
- https://www.freecodecamp.org/news/how-to-get-a-docker-container-ip-address-explained-with-examples/