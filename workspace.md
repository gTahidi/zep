
# Logging into Azure and Setting the Sub and Resource-group

az login
az account set --subscription 2c9e694a-be3b-4604-b4d9-dc4bdd41a3e1
az aks get-credentials --resource-group gtahidi_group --name zepmemory

## Creating a secret for the Zep Deployment Service

kubectl create secret generic my-secret --from-env-file=.env

### Creating and applying Deployment YAMLS, and Configmaps

kubectl apply -f zep-k8-deployment.yaml
kubectl create configmap zep-config --from-file=zep-config.yaml

### Logging, description of pods, and restating deployments.

kubectl describe pod zep-7949f9799b-z47jt -n zep
kubectl logs zep-7949f9799b-z47jt -n zep
kubectl apply --dry-run=client -f zep-k8-deployment.yaml

kubectl rollout restart deployment zep -n zep

kubectl scale rs zep-79768fb877-p5s6n --replicas=0 -n zep
zep-79768fb877-zssz6

az aks disable-addons --addons monitoring --name zepmemory --resource-group gtahidi_group
 kubectl port-forward svc/zep-postgres-76dff5f44f-bs7wd 5432:5432

 kclear
 kubectl apply -f zep-config.yaml
kubectl get configmaps
kubectl apply -f zep-config.yaml

# Connecting to the postgres store via bash

kubectl exec -it -n zep $(kubectl get pods -n zep -l app=zep-postgres -o jsonpath="{.items[0].metadata.name}") -- bash

# Accessing the postgres environment

psql -U postgres -d postgres

kubectl logs -n zep $(kubectl get pods -n zep -l app=zep-postgres -o jsonpath="{.items[0].metadata.name}")

# Postgress Cheat Sheet

1. Viewing Data
\l or \list: List all databases in your PostgreSQL server.
\c [database_name]: Connect to the postgres DB
\dt: List all tables in the current database.
SELECT * FROM table_name;: View all data in a specific table.
\d table_name: Describe the structure of a specific table, showing information about its columns, types, and constraints