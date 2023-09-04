# pgbouncer
PgBouncer is an open-source, lightweight, single-binary connection pooler for PostgreSQL. It can pool connections to one or more databases (on possibly different servers) and serve clients over TCP and Unix domain sockets.
And here I will show you how to deploy this service on a kubernetes cluster

## How it works

clients (users and systems) point their connection strings to the PgBouncer IP/Port, using a user specifically created for this connection (which may or may not be the same as the database), they are introduced into a queue and this queue is performed by the database through a connection between the pool and the database.


### Generate authentication credentials for all users:

generate-userlist >> userlist.txt


### Generate the secrets:

./create-secrets

### Install services

kubectl apply -f service.yaml -n pgbouncer
kubectl  apply -f deployment -n pgbouncer


#### In GCP (Google Cloud Platform) to be able to view the auth_id in the user, it is necessary to add some flags to the database

![image](https://github.com/Guilhermeferreir/pgbouncer-k8s/assets/83267524/79b5cd8b-077e-4b62-9fb4-7d7595dfab58)


## Connecting Localhost

You can connect via: 

localhost
- kubectl port-forward -n pgbouncer  svc/pgbouncer-example 5432:80
- psql --host localhost --port 5432 -U pgbouncer -d <dbname> -W


DB IP
- psql --host <IP> --port 5432 -U pgbouncer -d <dbname> -W



### Connecting to an Application via Localhost


Open the proxy:
kubectl port-forward service/pgbouncer-example 5432:5432 -n pgbouncer

In your application:
SQL_DATABASE_URI=postgres://pgbouncer:<user><password_user>@localhost:5432/<dbname>
