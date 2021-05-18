# Kubernetes Cluster System Components

## Overview

JovianX manages Kubernetes clusters 

Container Logging \| Elastic + FluentD

Monitoring \|  Prometheus + Grafana 

Cluster Access Gateway \|  Ambassador + Cert-Manager

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

