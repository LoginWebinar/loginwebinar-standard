# Postgres Local Server Configuration Changes

If the server has Postgres install as a VPS/Barebones service

The following are the instructions for the Postgres 18 version

PORT 5432 must be opened for the Docker Network to communicate


## CHANGES TO POSTGRESQL.CONF

Must allow all addresses to listen

** Change this:
#listen_addresses = 'localhost' 

** To this:
listen_addresses = '*'

```
sudo nano /etc/postgresql/18/main/postgresql.conf
```

## CHANGES TO THE PG_HBA.CONF

** must add this to the bottom of the configuration
host all all 172.17.0.0/16 md5


```
sudo nano /etc/postgresql/18/main/pg_hba.conf
```

```
sudo systemctl restart postgresql
```