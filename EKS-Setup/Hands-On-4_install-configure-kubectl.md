
# kubectl - the commandline K8s tool

### install _kubectl_ & _aws-iam_authenticator_
* kubectl
  * on RH based Linux: ```sudo dnf install kubernetes-client```
    * check: ```kubectl version --short --client```
  * on Windows, open a terminal emulator, preferrably MobaXterm:
  ```
  curl -k -# -o kubectl.exe https://amazon-eks.s3-us-west-2.amazonaws.com/1.10.3/2018-07-26/bin/windows/amd64/kubectl.exe
  chmod +x kubectl.exe
  mkdir $HOME/bin
  mv kubectl.exe $HOME/bin
  echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
  source .bashrc
  ```
    * check: ```kubectl.exe version --short --client```

* aws-iam-authenticator
  * on Linux:
  ```
  curl -o aws-iam-authenticator https://amazon-eks.s3-us-west-2.amazonaws.com/1.10.3/2018-07-26/bin/linux/amd64/aws-iam-authenticator   
  chmod +x ./aws-iam-authenticator  
  cp ./aws-iam-authenticator /usr/local/bin/
  ```
    * Test: ```aws-iam-authenticator help```

  * on Windows, open a terminal emulator, preferrably MobaXterm:  
  ```
  curl -k -# -o aws-iam-authenticator.exe  https://amazon-eks.s3-us-west-2.amazonaws.com/1.10.3/2018-07-26/bin/windows/amd64/aws-iam-authenticator.exe
  chmod +x aws-iam-authenticator.exe
  mv aws-iam-authenticator.exe $HOME/bin
  ```
    * Test: ```aws-iam-authenticator.exe help```

* aws credentials (ACCESS KEY+SECRET)
now we have to provide the Access key+secret from the first lesson _Part I : covering prerequisites_ and put them into the credentials template.

    * populate aws credentials file
      copy the provided file named _credentials_ to
      * WINDOWS cygwin: ```mkdir $HOMEPATH/.aws && vi $HOMEPATH/.aws/credentials```
      * Linux: ```~/.aws/credentials```
      and set the properties _aws_access_key_id_ and _aws_secret_access_key_


### configure _kubectl_
in this step we are creating a configuration file for the binary ```kubectl```, which is the main tool to interact with Kubernetes later on.
* use template file _kube-config-eks_ and copy it to:
  * Linux: ```~/.kube/kube-config-eks```
  * Windows (cygwin): ```mkdir $HOMEPATH/.kube && vi $HOMEPATH/.kube/kube-config-eks```
* edit file ```kube-config-eks``` and replace _endpoint-url_, _base64-encoded-ca-cert_ by the values you recorded in the Hands-On lesson 3 _Part III: create the K8s control plane_.

* Linux : ```export KUBECONFIG=~/.kube/kube-config-eks```
  Windows : ```export KUBECONFIG=$HOMEPATH/.kube/kube-config-eks```

* Test connectivity and access:  
  ```
  #>kubectl get svc
  NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
  kubernetes   ClusterIP   xxxxxxxxx    <none>        443/TCP   4m
  ```
  command to check the config for kubectl: `kubectl config view`

Now you successfully talked to the K8s control plane on AWS !!
