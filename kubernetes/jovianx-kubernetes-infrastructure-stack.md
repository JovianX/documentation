# JovianX System Components

## Overview

JovianX manages Kubernetes clusters 

Installing Helm

Installing Container Logging \| Elastic + FluentD

Installing Monitoring \|  Prometheus + Grafana 

Installing Cluster Access Gateway \|  Ambassador + Cert-Manager

## Installing Helm 

### Helm Initialization

```bash
# Create A service-account for Tiller with cluster-role 
$ kubectl  apply -f https://raw.githubusercontent.com/JovianX/kubernetes-cluster-infrastructure/master/tiller-serviceaccount.yaml
$ helm init --service-account tiller --history-max 200
```

## Installing Ambassador Gateway

```bash
# Create the jovianX-system namespace
$ kubectl create namespace jovianx-system

# Add Ambassador Helm Repo
$ helm repo add datawire https://www.getambassador.io

# Install Ambassador in the JovianX-System namespace
$ helm install --name ambassador --namespace jovianx-system datawire/ambassador --set nodeSelector\\.eks\\.amazonaws\\.com/nodegroup=gigaspaces-nodepool-system

```

{% hint style="info" %}
Note: Configure nodeSelector to run Ambassador on the jovianx-system node pool.  Note that node selector has

To view current labels on the nodes run `$ kubectl get nodes --show-labels` . then 
{% endhint %}

Note that nodeSelector has to escape dot\(`.` \)char. 

