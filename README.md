
# Vagrantfile and Scripts to Automate Kubernetes Setup using Kubeadm 

## Prerequisites

1. Working Vagrant setup
2. 8 Gig + RAM workstation as the Vms use 3 vCPUS and 4+ GB RAM
 
## Usage/Examples

To provision the cluster, execute the following commands.

```shell
git clone https://github.com/somu4git/vagrant-kubeadm-k8.git
cd vagrant-kubeadm-k8
vagrant up
```

## Set Kubeconfig file varaible.

```shell
cd vagrant-kubeadm-k8
cd configs
export KUBECONFIG=$(pwd)/config
```

or you can copy the config file to .kube directory.

```shell
cp config ~/.kube/
```

## Kubernetes Dashboard URL

To access the dashboard on your local workstation you need to create a secure channel to your k8 cluster.

Run : kubectl proxy

```shell
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/overview?namespace=kubernetes-dashboard
```

## Kubernetes login token

Vagrant up will create the admin user token and saves in the configs directory.

```shell
cd vagrant-kubeadm-k8
cd configs
cat token
```

## To shutdown the cluster, 

```shell
vagrant halt
```

## To restart the cluster,

```shell
vagrant up
```

## To destroy the cluster, 

```shell
vagrant destroy -f
```

