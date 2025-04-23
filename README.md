# Kubernetes Scaling and Scheduling: Resource Quotas

Resource quotas are an essential feature in Kubernetes for controlling and limiting resource usage within namespaces. They help administrators ensure fair resource distribution and prevent any single application from consuming excessive cluster resources.

## What are Resource Quotas?

Resource quotas in Kubernetes are objects that define constraints on resource consumption per namespace. They allow you to:

- Limit the total amount of compute resources (CPU, memory) that can be requested by all pods in a namespace
- Restrict the number of Kubernetes objects (pods, services, configmaps, etc.) that can be created in a namespace
- Control storage resource usage

## Creating a ResourceQuota

Here's a basic example of a ResourceQuota:

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-quota
  namespace: nginx-ns
spec:
  hard:
    pods: "10"
    requests.cpu: "1"
    requests.memory: 1Gi
    limits.cpu: "2"
    limits.memory: 2Gi
```

This quota would limit the `nginx-ns` namespace to:
- Maximum 10 pods
- Total CPU requests of 1 core
- Total memory requests of 1GB
- Total CPU limits of 2 cores
- Total memory limits of 2GB

## Key Considerations

1. **Resource Requirements**: When a quota is active in a namespace, pods must specify resource requests and/or limits for the resources being constrained.

2. **Quota Enforcement**: Kubernetes will reject any pod creation that would cause the namespace to exceed its quota limits.

3. **Monitoring**: You can check quota usage with:
   ```
   kubectl describe quota -n <namespace>
   ```

4. **Types of Quotas**:
   - **Compute quotas**: Limit CPU and memory resources
   - **Storage quotas**: Limit storage resource consumption
   - **Object count quotas**: Limit number of objects by type

## Best Practices

- Define resource quotas for all production namespaces
- Combine with LimitRanges to enforce default limits and requests
- Regularly review quota utilization to adjust as needed
- Create different quota tiers for different types of workloads
