# Openshift
Cheat sheet 

$source<(oc completion bash)
oc whoami --show-console

Verifying the Health of a Cluster 

Displays a column with the status of each node. If a node is not Ready, then it cannot communicate with the OpenShift control plane, and is effectively dead to the cluster.:
```bash
oc get nodes 
```

Displays the current CPU and memory usage of each node:
oc adm top nodes 

Getting node informations:
oc describe node <nodename>

Login to cluster: 
oc login -u kubeadmin -p MMTUc-TnXjo-NFyh3-aeWmC \  https://api.ocp4.example.com:6443

Cluster Version:
oc get clusterversion 

Get more cluster version information:
oc describe clusterversion

Reviewing Cluster Operators:
oc get clusteroperators 


