# PGBouncerTestinator
Setup a docker environment to allow for quick testing of pgbouncer pool_modes

## Setup
* Start Postgres & PgBouncer containers with `docker-compose up`
* Initialize the pgbench tables, etc. with `docker exec -ti postgres pgbench -U postgres -i postgres`
* Run pgbench in one terminal session, specify the connecting user as
  * `sess_usr` for testing session pooling
  * `tx_usr` for testing transaction pooling
  * `st_usr` for testing statement pooling
* Run pgbench in another terminal with the same settings, e.g.

```
# terminal 1
docker exec -ti postgres pgbench -U sess_usr -c 100 -T 30 -h pgbouncer -p 6432 -n postgres
```
```
# terminal 2
docker exec -ti postgres pgbench -U sess_usr -c 100 -T 30 -h pgbouncer -p 6432 -n postgres
```