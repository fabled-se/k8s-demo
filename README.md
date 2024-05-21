# This repo is a simple demo application to understand the Kubernetes basics.
Refer to Kubernetes Documentation for more details: https://kubernetes.io/docs

## Tools:
    k3d
    Kubectl
    docker/podman
    
# Use
Update k3d.yaml with your desired configuration and create a cluster:
k3d cluster create --config k3d.yaml

Modify and apply resources:
Kubectl apply -f <resource.yaml>


# Resources

## Namespace:
In Kubernetes, namespaces provide a mechanism for isolating groups of resources within a single cluster. Names of resources need to be unique within a namespace, but not across namespaces. Namespace-based scoping is applicable only for namespaced objects (e.g. Deployments, Services, etc.) and not for cluster-wide objects (e.g. StorageClass, Nodes, PersistentVolumes, etc.)
## Deployment:
A Deployment provides declarative updates for Pods and ReplicaSets. You describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate. You can define Deployments to create new ReplicaSets, or to remove existing Deployments and adopt all their resources with new Deployments.
## Service:
In Kubernetes, a Service is a method for exposing a network application that is running as one or more Pods in your cluster.
## Secrets
A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in a container image. Using a Secret means that you don't need to include confidential data in your application code.
## Configmaps
A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.
## Horizontal Pod Autoscaler
It is implemented as a Kubernetes API resource and a controller and periodically adjusts the number of replicas in a workload to match observed resource utilization such as CPU or memory usage
    
# Tips and Tricks

## Kubectl commands:
    
    Apply: kubectl apply -f <resource.yaml>
    Edit: kubectl edit <resource>
    Rollout restart: kubectl rollout restart deploy <deployment name>
    Describe: kubect describe <resource(e.g pod)>
    Delete: kubectl delete <resource>
    Logs: kubectl log <pod-name>
    Exec: kubectl exec -it <pod-name> -- /bin/sh (command)
    list all resources in k8s (use with responsability): kubectl api-resources --verbs=list --namespaced -o name \
| xargs -n 1 kubectl get --show-kind --ignore-not-found -l <label>=<value> -n <namespace>

## Troubleshoot
Check your service status by describing the pod and checking logs
    
Check your service, ingress certificates if you suspect of networking issues
    
Get a shell running in your pod if it's in a runnign state and check for processes; if it's not running you can use a sandbox sidecar container to check for your files and possibly logs

Describe your nodes and check for inconsistencies
 - kubectl get nodes / -o yaml
     
Check control plane logs
 - /var/log/kube-apiserver.log - API Server, responsible for serving the API
 - /var/log/kube-scheduler.log - Scheduler, responsible for making scheduling decisions
 - /var/log/kube-controller-manager.log - a component that runs most Kubernetes built-in controllers, with the notable exception of scheduling (the kube-scheduler handles scheduling).
     
     
