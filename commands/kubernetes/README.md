# Kubernetes

## Cheat Sheet

[https://kubernetes.io/docs/reference/kubectl/cheatsheet/](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## Common Commands

```sh
# Set the default namespace
kubectl config set-context --current --namespace <NAMESPACE>

# List/Get the resource(s)
kubectl get <deployment|service|pod|...> [RESOURCE_NAME]

# Interactive shell access to a running pod
kubectl exec -it <POD_NAME> -- /bin/sh
```

## Multi-cluster Management

### Switch between Clusters

```sh
# List all contexts
kubectl config get-contexts

# Get current context
kubectl config current-context

# Switch to another context
kubectl config use-context <CONTEXT_NAME>
```
