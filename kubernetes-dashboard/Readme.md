## Kubernetes Dashboard
### Deploy the K8s dashboard
```
kubectl apply -f deploy-dashboard.yaml
kubectl apply -f deploy-heapster.yaml
kubectl apply -f deploy-influxdb.yaml
kubectl apply -f deploy-heapster-rbac.yaml
```
### create an admin user account
```
kubectl apply -f admin-service-account.yaml
kubectl apply -f dashboard-account-rbac.yaml
```
### access the dashboard
* get a security token
```kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep eks-course-admin | awk '{print $1}')
```
record the output of ```token:```

* start kube proxy via ```kubectl proxy```

* open browser at `http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/`

and choose _token_ as login method, where you have to provide the token you recorded two steps before
