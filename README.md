# Home Custer
My kubernetes at home setup

https://blog.quickbird.uk/domesticating-kubernetes-d49c178ebc41

## 🚧 GPG

- Master key + sub keys
- YubiKey as a smartcard
- SSH support

## 🚧 Secrets

- SOPS

## Infrastructure

### 🚧 Hardware

- Currently `kind` running on macOS
- Planning to use Raspberry Pi 4 w/ 8G memory

### 🚧 Networking

- Fritz!Box 7490
    - Dynamic DNS support
    - Port forwarding to first IP in range
- Network plugin
    - https://kubernetes.io/docs/concepts/cluster-administration/networking/
- [metallb](https://metallb.universe.tf/)
- ingress-nginx

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