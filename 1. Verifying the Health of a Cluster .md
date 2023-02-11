# Openshift Verifying the Health of a Cluster 
 ```
$source<(oc completion bash)
oc whoami --show-console
```
Displays a column with the status of each node. If a node is not Ready, then it cannot communicate with the OpenShift control plane, and is effectively dead to the cluster:
```bash
oc get nodes 
```

Displays the current CPU and memory usage of each node:
```
oc adm top nodes 
```
Getting node informations:
```
oc describe node <nodename>
```
Login to cluster: 
```
oc login -u kubeadmin -p MMTUc-TnXjo-NFyh3-aeWmC \  https://api.ocp4.example.com:6443
```
Cluster Version:
```
oc get clusterversion 
``` 
Get more cluster version information:
```
oc describe clusterversion
```
List all events from the current project and look for error messages related to the pod:
```
oc get events
```
Reviewing Cluster Operators:
```
oc get clusteroperators 
```
Displaying the Logs of OpenShift Nodes:
```
oc adm node-logs -u crio my-node-name
oc adm node-logs -u kubelet my-node-name
You can also display all journal logs of a node: oc adm node-logs my-node-name
```
Opening a Shell Prompt on an OpenShift Node: Direct access to a node to inspect their status
```
oc debug node/my-node-name
```
Opening a Shell Prompt on an OpenShift Node: To run local commands directly from the node, while in a oc debug node session
```
oc debug node/my-node-name

Example:  oc debug node/master01
Still using the same shell session, verify that the Kubelet and the CRI-O container engine are running. 
$ systemctl status kubelet

Rerun the same command against the crio service
$ systemctl status crio

Type q to exit the command.

Still using the same shell session, verify that the etcd pod is running
$ crictl ps --name etcd

Terminate the chroot session and shell session to the node
$ exit
```
Creating Troubleshooting Pods: creating a pod from a deployment, but running as the root user and thus proving that the deployment references a container image that was not designed to run under the default security policies of OpenShift:
```
oc debug deployment/my-deployment-name --as-root
```
Changing a Running Container:
```
Opens a shell inside a pod to run shell commands interactively and non-interactively.
oc rsh my-pod-name

Copies local files to a location inside a pod. You can also reverse arguments and copy files from inside a pod to your local file system. See also the oc rsync command for copying multiple files at once.
oc cp /local/path my-pod-name:/container/path

Creates a TCP tunnel from local-port on your workstation to local-port on the pod. The tunnel is alive as long as you keep the oc port-forward running. This allows you to get network access to the pod without exposing it through a route. Because the tunnel starts at your localhost, it cannot be accessed by other machines.
oc port-forward my-pod-name local-port:remote-port
```
Troubleshooting OpenShift CLI Commands: 
```
 oc get pods --loglevel 6
 oc get pods --loglevel 10
```
With this token, an automation tool can make OpenShift API requests as if it was logged in as your user. To get your token, use the -t option of the oc whoami command:
```
oc whoami -t
```
Log in to the Red Hat Container Catalog with your Red Hat account:
```
$ podman login registry.redhat.io
```
Skopeo to find information about the container image from the events:
```
skopeo inspect \ docker://registry.redhat.io/rhel8/postgresq-13:1
```
```
```
