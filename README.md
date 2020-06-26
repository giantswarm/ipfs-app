# ipfs-app

`ipfs-app` helm charts makes [IPFS](https://ipfs.io/) available on your Kubernetes hosts (*read-only* mode).
This is done via running IPFS daemon with fuse mounting enabled.
After chart deployment, every Kubernetes node will get this directory structure propagated:

```
opt
└── ipfs
    ├── config
    └── fuse
        ├── ipfs
        └── ipns
```

This make it possible for other applications  to mount `hostPath` directories from the fuse mount.
E.g. object in IPFS can be accessed via `/opt/ipfs/fuse/ipfs/<cid>` path.

## How to install it?

```
git clone github.com/giantswarm/ipfs-app
cd ipfs-app

helm install helm/ipfs-app --name ipfs-app --values helm/ipfs-app/values.yaml
```

Verify pods are running:

```
kubectl get pods
NAME                             READY   STATUS    RESTARTS   AGE
ipfs-app-blcp2                   1/1     Running   0          19h
ipfs-app-clhzq                   1/1     Running   0          19h
ipfs-app-zf6zr                   1/1     Running   0          19h
```

Check logs to verify that IPFS daemon is running without errors:

```
kubectl logs ipfs-app-blcp2
Initializing daemon...
go-ipfs version: 0.6.0
Repo version: 10
System version: amd64/linux
Golang version: go1.14.4
Swarm listening on /ip4/10.7.59.67/tcp/4001
Swarm listening on /ip4/10.7.59.67/udp/4001/quic
Swarm listening on /ip4/127.0.0.1/tcp/4001
Swarm listening on /ip4/127.0.0.1/udp/4001/quic
Swarm listening on /p2p-circuit
Swarm announcing /ip4/10.7.59.67/tcp/4001
Swarm announcing /ip4/10.7.59.67/udp/4001/quic
Swarm announcing /ip4/127.0.0.1/tcp/4001
Swarm announcing /ip4/127.0.0.1/udp/4001/quic
Swarm announcing /ip6/::1/tcp/4001
Swarm announcing /ip6/::1/udp/4001/quic
API server listening on /ip4/127.0.0.1/tcp/5001
WebUI: http://127.0.0.1:5001/webui
IPFS mounted at: /ipfs/fuse/ipfs
IPNS mounted at: /ipfs/fuse/ipns
Gateway (readonly) server listening on /ip4/127.0.0.1/tcp/8080
Daemon is ready
```
