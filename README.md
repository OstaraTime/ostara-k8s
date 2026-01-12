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


