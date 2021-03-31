# Home Custer
My kubernetes at home setup

https://blog.quickbird.uk/domesticating-kubernetes-d49c178ebc41

## Prerequisites

- [Homebrew](https://brew.sh/)
- [Docker for Mac](https://docs.docker.com/docker-for-mac/)
- [Kind](https://kind.sigs.k8s.io/)
- [kubectx](https://github.com/ahmetb/kubectx)

```shell
brew install homebrew/cask/docker kind kubectx
```

## 🚧 GPG

- Master key (offline)
- Sub keys
    - **S**ignature
    - **E**ncryption
    - **A**uthentication
- YubiKey as a smart card
- SSH support

## 🚧 Secrets

- SOPS
    - https://github.com/goabout/kustomize-sopssecretgenerator

## Infrastructure

### 🚧 Hardware

I'm currently running `kind` on macOS.
See [kind/config.yaml](kind/config.yaml).
The most limiting factor is the lack of the docker containers joining my home network.
See https://www.thehumblelab.com/kind-and-metallb-on-mac/.

I'm planning to use one or more Raspberry Pi 4 w/ 8G memory.

### 🚧 Networking

- Fritz!Box 7490
    - Dynamic DNS support
    - Port forwarding to first IP in range
- Network plugin
    - https://kubernetes.io/docs/concepts/cluster-administration/networking/
- [metallb](https://metallb.universe.tf/)
- ingress-nginx

#### IP Address Management

Everything operates within a `192.168.100.0/24` (254 hosts) subnet.
It's important that this subnet's range is not used by the network's DHCP server.
My router operates within `192.168.188.0/24` and DHCP is limited to `192.168.188.20-192.168.188.200`.

```shell
ipcalc 192.168.100.0/24 -s 62 62 62
```

- `192.168.100.0/26` reserved for fixed external IPs
    - `192.168.100.1-192.168.100.63` (63 hosts)
    - Managed by [`metallb`](metallb/metallb-config.yaml)
    - `192.168.100.1` reserved for DNS server
    - `192.168.100.2` reserved for Ingress controller
       - Target of port-forwarding on TCP/80 and TCP/443
- `192.168.100.64/26` reserved for dynamic external IPs
    - `192.168.100.64-192.168.100.127` (64 hosts)
    - Managed by [`metallb`](metallb/metallb-config.yaml)
- `192.168.100.128/26` reserved for future use
    - `192.168.100.128-192.168.100.191` (64 hosts)
- `192.168.100.192/26` reserved for running locally with `kind`
    - `192.168.100.192-192.168.100.255` (63 hosts)
    - Managed by [`docker`](bin/cluster)
    - `192.168.100.192` gateway
    - `192.168.100.193-192.168.100.255` nodes
    - See [`kind` network setup](bin/cluster)

### 🚧 DNS

- [Pi-hole](https://pi-hole.net/)
- [DynDNS Service](https://ddnss.de/)
- local vs. public
    - `xyz.local`
    - `xyz.whiskeysierra.myhome-server.de`
    
### 🚧 Storage

- ConfigMap vs. local disk
- NAS?

## 🚧 System

- Which kubernetes distro?

## 🚧 Services

- cert-manager
- oauth2-proxy
    - Github OAuth application
    - Restricted access
    - Single-Sign-On
- [Grafana](https://grafana.com/)
- [Prometheus](https://prometheus.io/)
- [Kubernetes Dashboard](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)
  
## 🚧 Applications

- [Nextcloud](https://nextcloud.com/)
- [Kodi](https://kodi.tv/)
- [Home-Assistant](https://www.home-assistant.io/)

### 🚧 Routes

| Domain       | Name                 | Private | Public |
|--------------|----------------------|---------|--------|
| `grafana`    | Grafana              | ✅       | ✅      |
| `kubernetes` | Kubernetes Dashboard | ✅       | ✅      |
| `pi-hole`    | Pi-hole              | ✅       | ✅      |
| `prometheus` | Prometheus           | ✅       | ❌      |
| `router`     | Fritz!Box UI         | ✅       | ✅      |