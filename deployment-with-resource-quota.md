# Working on Resourse Quota to the certain pod (eg: nginx)

Example
```
➜  scaling-and-scheduling kubectl apply -f deployment-with-resource-quota.yml 
deployment.apps/nginx created
➜  scaling-and-scheduling kubectl get pods -n nginx-ns
NAME                     READY   STATUS    RESTARTS   AGE
nginx-6548dcc9d7-dhtfh   1/1     Running   0          7s
nginx-6548dcc9d7-mzckz   1/1     Running   0          7s
➜  scaling-and-scheduling kubectl get pods -n nginx-ns -o wide
NAME                     READY   STATUS    RESTARTS   AGE   IP           NODE                         NOMINATED NODE   READINESS GATES
nginx-6548dcc9d7-dhtfh   1/1     Running   0          31s   10.244.2.8   ignius-k8s-cluster-worker2   <none>           <none>
nginx-6548dcc9d7-mzckz   1/1     Running   0          31s   10.244.3.9   ignius-k8s-cluster-worker3   <none>           <none>
➜  scaling-and-scheduling kubectl describe pod nginx-6548dcc9d7-dhtfh -n nginx-ns 
Name:             nginx-6548dcc9d7-dhtfh
Namespace:        nginx-ns
Priority:         0
Service Account:  default
Node:             ignius-k8s-cluster-worker2/172.18.0.2
Start Time:       Wed, 23 Apr 2025 23:15:03 +0545
Labels:           app=nginx
                  pod-template-hash=6548dcc9d7
Annotations:      <none>
Status:           Running
IP:               10.244.2.8
IPs:
  IP:           10.244.2.8
Controlled By:  ReplicaSet/nginx-6548dcc9d7
Containers:
  nginx:
    Container ID:   containerd://70962df683bc5ca9ecbb6ba4ca7c33cea2dca9d38767df16fbbc4c8410d69efb
    Image:          nginx:latest
    Image ID:       docker.io/library/nginx@sha256:5ed8fcc66f4ed123c1b2560ed708dc148755b6e4cbd8b943fab094f2c6bfa91e
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Wed, 23 Apr 2025 23:15:05 +0545
    Ready:          True
    Restart Count:  0
    Limits:
      cpu:     200m
      memory:  256Mi
    Requests:
      cpu:        100m
      memory:     128Mi
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-bblbb (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       True 
  ContainersReady             True 
  PodScheduled                True 
Volumes:
  kube-api-access-bblbb:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   Burstable
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  67s   default-scheduler  Successfully assigned nginx-ns/nginx-6548dcc9d7-dhtfh to ignius-k8s-cluster-worker2
  Normal  Pulling    67s   kubelet            Pulling image "nginx:latest"
  Normal  Pulled     65s   kubelet            Successfully pulled image "nginx:latest" in 2.085s (2.085s including waiting). Image size: 68844367 bytes.
  Normal  Created    65s   kubelet            Created container: nginx
  Normal  Started    65s   kubelet            Started container nginx
➜  scaling-and-scheduling 


```
