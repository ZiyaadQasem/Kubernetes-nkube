# Recipe to Install n-nodes Kubernetes cluster on your windows local machine (production-like environment)
The scripts used here have been adapted from [this blog](https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/) with some necessary modifications to fix some bugs and facilitate the process of cluster creation.

## Prerequisites
Before you begin, you should check if virtualization is supported on your windows. See [this link](https://www.shaileshjha.com/how-to-find-out-if-intel-vt-x-or-amd-v-virtualization-technology-is-supported-in-windows-10-windows-8-windows-vista-or-windows-7-machine/) to do that.

### 1. Oracle VirtualBox
Use [this link](https://www.virtualbox.org/wiki/Download_Old_Builds_6_0) to download Oracle VirtualBox if it is not already installed on your machine.

> Note: To ensure compatibility with the rest of the prerequisites, make sure that the version is 6.0.x or older.

### 2. Vagrant
Use [this link](https://www.vagrantup.com/downloads.html) to download Vagrant if it is not already installed.
> Note: You should  restart the computer after downloading Vagrant.


## Creating  Kubernetes cluster
Performe the following steps with powershell :
1. Clone this repository `git clone https://github.com/ZiyaadQasem/Kubernetes-nkube.git`
2. Navigate to install-nkube directory `cd install-nkube`
3. Run this command `vagrant up --provider virtualbox`
> Note: this command will create 3-nodes cluster (1 maser and 2 workers). If you want more or less worker nodes you can just change the value of the variable WORKERS_NUMBER inside the file Vagrantfile.

4. Bring the kubeconfig to your local machine  `$Env:KUBECONFIG=($Env:KUBECONFIG + ";"+$PWD.Path+"/kubernetes-setup/kubectl-config")`
5. Set current context `kubectl config use-context nkube-cluster`

After you have done all the above steps, you should now be able to work with kubernetes cluster from your local terminal. To confirm this, the output from `kubectl get nodes` should be similar to:

```console
NAME             STATUS   ROLES    AGE   VERSION
master     Ready    master   45m   v1.17.2
worker-1   Ready    <none>   42m   v1.17.2
worker-2   Ready    <none>   40m   v1.17.2
```

> Notes: 
    - After you create the cluster, you can only perform steps 2 and 3 whenever you want to run it. 
    - To login any node you can run this command: `vagrant ssh [NODE_NAME]`.

