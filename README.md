# flask-template
## Boilerplate for a dockerised, production ready, database driven flask application that can be easily deployed on a cluster 

### Getting started
1. Stop any services on host machine that use ports 80 or 5432 (such as apache2, postgresql) e.g. `service apache2 stop`. Alternatively change the ports exposed by the nginx and postgres containers to something else (not recommended).
2. Run `docker-compose up -d --build`
3. Create the database schema using the provided script `docker-compose exec web python create_db.py`. NOTE: This will teardown any existing tables so only use for dev or initial setup.
4. Inspect the Postgresql server on the DB container to verify that tables have been created successfully `docker-compose exec db psql -U postgres --dbname=site_db`
5. Verify that the volume has been created to persist DB data `docker volume inspect flask-template_db_data`
6. For use in production, set environment variables in `env.prod` and then set that file as the `env_file` for the web and db containers in `docker-compose.yml`

Finally, it is recommended to set the Nginx image to a specific verison in the nginx docker file to avoid upsteam changes breaking the build.
