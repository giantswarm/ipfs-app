# ipfs-demo-app

This demo chart demonstrates how to IPFS mounted with the fuse on Kubernetes hosts.
It shares a static web page, hosted in IPFS, via caddy web-server.

## How to install it?

1. Install `ipfs-app` chart.
2. Put your ingress host into values file and run 

3. Install `demo-app` chart 
```
helm install helm/ipfs-demo-app --name ipfs-demo-app --values helm/ipfs-demo-app/values.yaml
```

Verify pods are running:

```
kubectl get pods
NAME                             READY   STATUS    RESTARTS   AGE
ipfs-app-blcp2                   1/1     Running   0          19h
ipfs-app-clhzq                   1/1     Running   0          19h
ipfs-app-zf6zr                   1/1     Running   0          19h
ipfs-demo-app-865d98cf85-k6bzl   1/1     Running   0          17h
ipfs-demo-app-865d98cf85-khsgs   1/1     Running   0          17h
ipfs-demo-app-865d98cf85-q896q   1/1     Running   0          17h
```

Now demo page is available via your ingress host.