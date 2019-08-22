# Setup of eksctl
for non-Linux OS you can find a binary download here:

https://github.com/weaveworks/eksctl/releases

on Linux, you can just execute:
```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/download/latest_release/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp  

sudo mv /tmp/eksctl /usr/local/bin
```

This utility will use the same _credentials_ file as we explored for the AWS cli, located under '~/.aws/credentials'
