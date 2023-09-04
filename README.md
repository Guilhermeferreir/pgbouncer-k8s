# pgbouncer
Deployment pbouncer in Kubernetes


### Generate authentication credentials for all users:

generate-userlist >> userlist.txt


### Generate the secrets:

./create-secrets

### Install services

kubectl apply -f service.yaml -n pgbouncer
kubectl  apply -f deployment -n pgbouncer


### In GCP (Google Cloud Platform) to be able to view the auth_id in the user, it is necessary to add some flags to the database

![image](https://github.com/Guilhermeferreir/pgbouncer-k8s/assets/83267524/79b5cd8b-077e-4b62-9fb4-7d7595dfab58)
