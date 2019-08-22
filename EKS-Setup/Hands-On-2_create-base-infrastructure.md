# Hands-On II : create base AWS infrastructure

### create VPC, subnets and security group for your K8s cluster
to create a VPC there is a prepared CloudFormation template to use. It creates a VPC including 3 Subnets
At the moment EKS is only available in the following 2 regions:  
  * US West (Oregon), _us-west-2_
  * US East (N.Virginia), _us-east-1_

* open ```https://console.aws.amazon.com/cloudformation/``` and select one of the above mentioned regions
* click _Create Stack_
* select _Upload a template to Amazon S3_ , click *_Upload file_* and select `eks-course-vpc.yaml`
* click _Next_
* provide data in the _Specify Details_ overview:
  * Stack name : set stack name _EKS-course-stack_
  * VPC Block : set CIDR range for your VPC, or leave the default from the CloudFormation template
  * Subnet01Block : set CIDR range for this subnet, or leave the default from the CloudFormation template
  * Subnet02Block : set CIDR range for this subnet, or leave the default from the CloudFormation template
  * Subnet03Block : set CIDR range for this subnet, or leave the default from the CloudFormation template
* click _Next_
* click _Create_
* observe the progress of the stack creation. After the stack is created, open tab _Outputs_ and record the *VPC-ID*, *SecurityGroup* and the *Subnet_IDs* for all 3 subnets. You'll need those at worker launch time.
