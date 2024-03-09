# Deploying Django App in Kubernetes

## 1. Set up Virtual Environment
```shell
python3 -m venv myenv
source myenv/bin/activate
pip install django
pip freeze > requirements.txt
docker build -t archtaqi/django-kubernetes:1.0 .
docker push archtaqi/django-kubernetes:1.0 

brew install kubectl
kubectl cluster-info
kubectl create ns django-app
# Deploy the application
cd k8s/
kubectl apply -f db/
kubectl apply -f app/
kubectl apply -f nginx/

# Check status of pods
kubectl get pods -n django-app -w
# Create Superuser in django
kubectl get pods -n django-app
kubectl exec -it <pod-name> -n django-app -- sh
python3 manage.py createsuperuser

# debugging
kubectl get deployment/<pod-name> -o yaml

# 127.0.0.1:30005
```
