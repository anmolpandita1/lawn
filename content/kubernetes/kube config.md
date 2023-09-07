---
tags:
  - k8
  - kubernetes
  - k8s
---

## Config
```bash
# get help 
kubectl config --help 

# view all config 
kubectl config view 

# use a context 
kubectl use-context context1 

# get current context 
kubectl get current-context 

# get contexts, clusters, users 
kubectl config get-contexts 
kubectl config get-clusters 
kubectl config get-users 

# set/create new contexts, clusters, credentials for users to be used when using the context 
# may also be used to update some property values 
kubectl config set-contexts 
kubectl config set-contexts --current --namespace dev 
kubectl config set-clusters --current --help 

# these do take more args like server name kubectl config set-credentials 
# takes username, creds etc 
# set and unset a particular property 
# kubectl config set current-context dev 
# kubectl config unser current-context 
# kubectl config set --help for more kubectl config set kubectl config unset 
# delete a cluster, context credential from config 
kubectl config delete-clusters 
kubectl config delete-contexts 
kubeclt config delte-credentials
```

