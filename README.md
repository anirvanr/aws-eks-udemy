#install eksctl
#macOS users can use Homebrew:
```
brew install weaveworks/tap/eksctl
```

#verify
```
eksctl version
```
#Create cluster
```
eksctl create cluster --nodes 1 --region us-west-2
```
--> helloworld.yaml
```
---
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: helloworld-deployment
  labels:
    app: helloworld
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: helloworld
    spec:
      containers:
      - name: helloworld
        image: dockercloud/hello-world
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: "service-helloworld"
spec:
  selector:
    app: helloworld
  type: LoadBalancer
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
```

#update kubeconfig if deleted
```
aws eks --region us-west-2 update-kubeconfig --name wonderful-mongoose-1566283660
```

#get nodegroup name
```
eksctl utils describe-stacks --region=us-west-2 --name=wonderful-mongoose-1566283660
```
#get details of nodegroup
```
eksctl get nodegroup --name=ng-6d3bf314 --region=us-west-2 --cluster=wonderful-mongoose-1566283660
```

#Change instance type(replace each of the nodegroups by creating a new one and deleting the old one)
#add a new nodegroup
--> nodegroup_update.yaml
```
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: wonderful-mongoose-1566283660
  region: us-west-2

nodeGroups:
  - name: ng-mycluster
    instanceType: t2.medium
    desiredCapacity: 1
```
```
eksctl create nodegroup --config-file=nodegroup_update.yaml
```
#delete old nodegroup
```
eksctl delete nodegroup --name=ng-6d3bf314 --region=us-west-2 --cluster=wonderful-mongoose-1566283660
```
