## Launch the worker nodes
After ramping up the K8s controlplane now it is time to launch the worker nodes of your EKS cluster.
* open CloudFormation in AWS Management console ( ```https://console.aws.amazon.com/cloudformation/``` )
* in the navigation bar choose **same regions as for creating the controlplane before**, US East (N.Virginia)=> _us-east-1_
* choose _create Stack_
* under _Upload a template to Amazon S3_ , click *_Upload file_* and select `eks-course-nodegroup.yaml` (from the downloaded resources folder of this course)
* on page _Specify Details_ provide the following information
  * Stack name: name of your CloudFormation stack, _eks-course-worker-nodes_
  * Cluster name: enter **same** name as at step `Create Cluster` => _EKS-course-cluster_
  * ClusterControlPlaneSecurityGroup: select the Security Group which has been created from the CloudFormation run at creating the cluster => it starts with _eks-vpc-ControlPlaneSecurityGroup..._
  * NodeGroupName: name for the autoscaling node group, _eks-course-nodegroup_
  * NodeAutoScalingGroupMinSize / NodeAutoScalingGroupMaxSize : specify min+max number of worker nodes, start with `2 / 4`
  * NodeInstanceType: choose EC2 instance type => `t2.medium`
  * NodeImageID: specify the AMI to use for the EC2 instances, for region US East(N.Virginia) us-east-1 it is: `ami-048486555686d18a0`
  * Key name: specify the key name to use for ssh into the worker nodes afterwards
  * VPC ID: choose the VPC ID you created before, and recorded from the `output tab` after the VPC has been created via CloudFormation
  * Subnets: pick the Subnet IDs from dropdown box, which have been create via CloudFormation at step `Create VPC` (check tab `output` of the corresponding CloudFormation stack)
* click `Next`
* review your information and click `Create`
* after the stack has been created, switch to tab `Outputs`
  * record the `NodeInstanceRole` of the node group. You need this info for configuring the EKS worker nodes.

Let the worker nodes join the cluster:

* create yaml file containing the configMap for AWS IAM authority. The value for `rolearn` is the NodeInstanceRole you recorded in the previous step (Outputs tab after launching worker nodes via CloudFormation).
From the downloaded code for this course, open aws-auth.yaml and set the role arn:
```
vi aws-auth.yaml
```
...and replace `<<role-arn-from-previous-step>>` by the one you recorded in the previous step.

```
kubectl apply -f aws-auth.yaml
```

Check current state of cluster services and nodes:  
```
kubectl get svc,nodes -o wide
```
