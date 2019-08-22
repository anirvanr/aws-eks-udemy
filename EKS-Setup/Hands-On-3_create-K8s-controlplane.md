# Hands-On III : create the K8s control plane
Kubernetes API server is a AWS service, hence it doesn't need dedicated EC2 instances to run.

* Open the EKS overview page in AWS Management console, ```https://console.aws.amazon.com/eks/home#/clusters``` and click _Create Cluster_.  
* Populate the following fields:
  * Cluster name : enter a unique name, _EKS-course-cluster_
  * Kubernetes version : by default the latest available version is preselected
  * Role ARN : select the IAM Role you created in the first Hands-On lesson _Part I: cover prerequisites_
  * VPC : select the VPC-ID from the dropdown box which was created in the first Hands-On lesson _Part II: create base AWS infrastructure_
  * Subnets : provide the comma separated Subnet-IDs you recorded in the previous step
  * SecurityGroup : select the security group (it has name _ControlPlaneSecurityGroup_ ) which has been created in Hands-On _Part II: create base AWS infrastructure_

* click _Create_
* on the _Clusters_ overview page,  observe field *_Status_* until cluster creation is finished.
  Click on your clustername, and record the *API server endpoint* and *Certificate authority* values to configure ```kubectl``` in the next Hands-On _Part IV: install & configure kubectl_.
