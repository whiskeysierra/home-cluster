# Home Custer
My kubernetes at home setup

https://blog.quickbird.uk/domesticating-kubernetes-d49c178ebc41

## 🚧 GPG

- Master key + sub keys
- YubiKey as a smartcard
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

- `192.168.100.0/26` reserved for running locally with `kind`
    - `192.168.100.1-192.168.100.62` (62 hosts)
    - `192.168.100.1` gateway
    - `192.168.100.2-192.168.100.62` nodes
    - See [`kind` network setup](bin/start)
- `192.168.100.64/26` reserved for fixed external IPs
    - `192.168.100.65-192.168.100.126` (62 hosts)
    - [Managed by `metallb`](metallb/metallb-config.yaml)
    - `192.168.100.65` reserved for DNS server
    - `192.168.100.34` reserved for Ingress controller
        - Target of port-forwarding on TCP/80 and TCP/443
- `192.168.100.128/26` reserved for dynamic external IPs
    - `192.168.100.129-192.168.100.190` (62 hosts)
    - [Managed by `metallb`](metallb/metallb-config.yaml)    
- `192.168.100.192/26` reserved for future use

### 🚧 DNS

- [Pi-hole](https://pi-hole.net/)
- Dynamic DNS, No-IP
- local vs. public
    - `xyz.local`
    - `xyz.whiskeysierra.ddns.net`
    
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