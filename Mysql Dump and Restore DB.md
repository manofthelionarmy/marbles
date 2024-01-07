[Links?](#)
[Embbed Videos?](#)
[Mysql dump and restore dbs](https://linuxize.com/post/how-to-back-up-and-restore-mysql-databases-with-mysqldump/)
# Summary

----
# Related Stuff

----
# Notes:
- To do this in a docker container, make sure to add new services in the docker-compose file:
```yaml
  backup:
    container_name: backup_nyla_treatment
    image: nyla_treatment_db:latest
    networks:
      - mysql
    volumes:
      - ./db/backup/:/backup/
  restore:
    container_name: restore_nyla_treatment
    image: nyla_treatment_db:latest
    networks:
      - mysql
    volumes:
      - ./db/backup/nyla_treatment.sql:/backup/nyla_treatment.sql
```
- What this does is ensures we have some things setup without having to manually type all the needed flags in the terminal.
- Now, I can simply run:
```shell
docker compose run -it backup bash
docker compose run -it restore bash
```
- And, inside of the containers I run:
```shell
mysqldump -h mysql -u root -p db_name > dump.sql

mysql -h mysql -u root -p db_name < dump.sql
```
- Super simple
- However, if I do drop the database, I have to recreate it.
```sql
drop database db_name;
create database db_name;

-- or (in MySql, it appears these are used synonymously)
drop schema db_name;
create schema db_name;
```
## Questions:

## Follow Up:
