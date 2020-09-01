# Creating AWS ELK Cluster

### 1. Installing eksctl commandline tool

`elsctl` is a popular command-line tool to create and manage Elastic Kubernetes Service \(EKS\) on AWS. To install elsctl run following commands:

```bash
# Download  the latest version of eksctl commandline tool
$ curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

# Move eksctl to your default command path
$ sudo mv /tmp/eksctl /usr/local/bin
```

{% hint style="info" %}
You can add`eksctl` to the bash completion by running:

`$ cat '. <(eksctl completion bash)' >> ~/.bashrc`
{% endhint %}

### 2. Set AWS account credentials 

Configure your aws credentials files `~/.aws/credentials`. It should define the `aws_access_key_id` and  `aws_secret_access_key`:

```scheme
[default]
aws_access_key_id=A*****s
aws_secret_access_key=tm******f
```

You can also configure the default output and region in file `~/.aws/config`

```bash
[default]
region=us-east-2
output=yaml
```

More details on aws command-line tool configuration can be found [HERE](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html).

### 3. Create a new EKS Cluster 

```bash
# Create a new Kubernetes cluster using eksctl command 
$ eksctl create cluster --name jovianx-<COMPANY>-us-east-2 \
    --region us-east-2 \
    --version 1.15 \
    --managed \
    --nodegroup-name jovianx-system \
    --node-type t3.large \
    --nodes 2 \
    --nodes-min 2 \
    --nodes-max 20 \
    --asg-access \
    --external-dns-access \
    --full-ecr-access \
    --alb-ingress-access \
    --auto-kubeconfig
```



