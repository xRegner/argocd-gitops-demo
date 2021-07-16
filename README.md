# Argo cd

## It is awesome tool

Ofiicial docs here: [https://argoproj.github.io/]

## 1. Argo Installation quick and dirty

```bash

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

#Check your password: only one time use
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

```

## 2. Resources to work with CLI

```bash
#to install in mac
brew install argocd
```

## 3. patch your svc to go to the local host or Port forward

### For Docker-Desktop cluster

```bash
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
#To change the pass -> not manatory 
argocd login localhost
argocd account update-password
#ie argocd login localhost 
argocd cluster add docker-desktop

```

## 4. Testing this repo

```bash

#apply
kubectl create ns dev-argo-test

kubectl apply -f 01-guestbook-sample.yaml 
#sync
argocd app create guestbook --repo https://github.com/argoproj/argocd-example-apps.git --path guestbook --dest-server https://kubernetes.default.svc --dest-namespace dev-argo-test
#delete
argocd app delete guestbook

```
