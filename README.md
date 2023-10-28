# Deployment startup

```bash
kubectl apply -f restrictednginx.yaml
```

# Check if everything starrted correctly

```bash
kubectl get deployments -n lab4
```

# Configuration checkup of created resources

```bash
kubectl describe namespace lab4 > dsc_namespace.yaml

kubectl describe resourcequotas lab4quota -n lab4  > dsc_resourcequota.yaml

describe deployments restrictednginx -n lab4  > dsc_deployment.yaml

kubectl describe pods -n lab4  > dsc_pods.yaml
```

# Configuration file description

Configuration file is composed of three parts:

- namespace declaration 
    ```yaml
    apiVersion: v1
    kind: Namespace
    metadata:
      creationTimestamp: null
      name: lab4
    spec: {}
    status: {}
    ```
- resourcequota declaration
    ```yaml
    apiVersion: v1
    kind: ResourceQuota
    metadata:
      creationTimestamp: null
      name: lab4quota
      namespace: lab4
    spec:
      hard:
        cpu: "1000"
        memory: 1Gi
        pods: "5"
    status: {}
    ```
- deployment declaration
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      creationTimestamp: null
      labels:
        app: restrictednginx
      name: restrictednginx
      namespace: lab4
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: restrictednginx
      strategy: {}
      template:
        metadata:
          creationTimestamp: null
          labels:
            app: restrictednginx
        spec:
          containers:
          - image: nginx
            name: nginx
            resources:
              limits:
                cpu: 250m
                memory: 256Mi
              requests:
                cpu: 125m
                memory: 64Mi
    status: {}
    ```