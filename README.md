# Kubernetes 101

## Tools: 
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/-install-azure-cli?view=azure-cli-latest)
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [Kubectx/Kubens](https://github.com/ahmetb/kubectx#installation)
- [Helm](https://helm.sh/docs/intro/install/)
- [Octant](https://github.com/vmware-tanzu/octant#installation)
- [Kail](https://github.com/boz/kail#installing) 

## Kubernetes intro
- What is Kubernetes? *Container Orchestrator*
    - Namespace: virtual sub-cluster
    - Service: describes networking to pods
    - Deployment: Describes how to run a pod (replicas, resources, readiness probes, ...)
    - Pod: Smalles application unit in k8s - should run 1 container (or sometimes a sidecar container)
    - Container: Docker container

## Kubernetes tools: kubectl, kubectx, kubens, octant
- Using kubectx to swap clusters
- Using kubens to set active namespace
- Using kubectl
- Using octant to have a GUI

## Managing Kubernetes: Imperative vs Declarative vs Helm (also Declarative)

### Imperative
*You tell k8s what to do*
```
kubectl create deployment --image=nginx nginx
kubectl expose deployment/nginx --type="NodePort" --port 80
kubectl delete svc nginx
kubectl delete deployment nginx
```

### Declarative
*You describe k8s your desired state*
```
kubectl apply -f declarative/deployment.yaml
kubectl apply -f declarative/service.yaml
```

### Helm
*You describe k8s your desired state + variables*

#### Deploy
```
helm upgrade \
--namespace devcon \
--install \
--values ./helm/nginx/charts/nginx/values.yaml \
--wait \
nginx \
./helm/nginx/charts/nginx/
```

#### Update
*All values in values.yaml can be overruled*
```
helm upgrade \
--namespace devcon \
--install \
--values ./helm/nginx/charts/nginx/values.yaml \
--set image.container.version=1.17.9 \
--wait \
nginx \
./helm/nginx/charts/nginx/
```

### Kubernetes debugging

#### Describe
```
kubectl describe deployments
```

#### Logging

```
kct logs deployments/nginx --all-containers -f
kail
```

#### Port Forwarding
```
kct port-forward deployments/nginx 9999:80
```

### Azure Devops
