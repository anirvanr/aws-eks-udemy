# Prerequisites

* Python3 or Python2.7.9+
* Python Pip

# Install awscli
## linux based system
```
pip install --user awscli
export PATH=$PATH:/home/<username>/.local/bin
```
_--user_ is used to install the awscli under your home directory, not to interfere with any existing libraries/installations

create file _~/.aws/credentials_ , just if you didn't go through first Hands-On _EKS-setup_:
```
[default]
aws_access_key_id=###
aws_secret_access_key=###
region=us-east-1
output=json
```

## Windows, using Anaconda
after Anaconda python distribution, goto "Start" => "Anaconda" => "open anaconda shell"
```
# potentially upgrade pip first
python -m pip install --upgrade pip
pip install --user awscli

set path=%path%;c:\users\<<username>>\appdata\roaming\python\python37\scripts
```

## TEST

```
aws eks describe-cluster --name EKS-course-cluster 
```
