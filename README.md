# ostara-k8s
Guide and manifests for installing Ostara on Kubernetes


Prerequisites:

installed and working kubernetes
kubectl access and working
traefik set up

then run
git clone https://github.com/OstaraTime/ostara-k8s
cd ostara-k8s
kubectl create namespace ostara
kubectl config set-context --current --namespace ostara

First, let's set up the kiosk service
kubectl apply -f ostara-web-kiosk-deployment.yaml 
kubectl apply -f ostara-web-kiosk-service.yaml
kubectl apply -f ostara-web-kiosk-ingress.yaml 


To use a database inside the cluster:

edit mariadb-secret.yaml and set
  MYSQL_USER: uporabnik
  MYSQL_PASSWORD: geslo
to something safer

kubectl apply -f mariadb-secret.yaml 

kubectl apply -f mariadb-pvc.yaml 
kubectl apply -f mariadb-deployment.yaml
kubectl apply -f mariadb-service.yaml 

now install the database schemas (work in progress, please do it manually from https://raw.githubusercontent.com/OstaraTime/OstaraServer/refs/heads/main/database/ostara_db.sql for now):
kubectl apply -f ostara-db-init.yaml 

To use phpMyAdmin (recommended):

kubectl apply -f phpmyadmin-deployment.yaml
kubectl apply -f phpmyadmin-service.yaml

now try logging in to it on http://<node-ip-address>:30881/ with the username and password you set in mariadb_secret
You should see some test data. Feel free to customize, especially dept and event_type.


Install minimal version of keycloak. This should not be used in prod and it is expected that you switch to a more permanent install once this is validated.


