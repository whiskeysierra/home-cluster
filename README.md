# Home Custer
My kubernetes at home setup

## 🚧 GPG

- Master key + sub keys
- YubiKey as a smartcard
- SSH support

## 🚧 Secrets

- SOPS

## 🚧 Networking

- Fritz!Box 7490
    - Dynamic DNS support
    - Port forwarding to first IP in range
- [metallb](https://metallb.universe.tf/)

## 🚧 DNS

- [Pi-hole](https://pi-hole.net/)
- Dynamic DNS, No-IP
- local vs. public
    - `xyz.local`
    - `xyz.whiskeysierra.ddns.net`
    
## 🚧 Storage

- ConfigMap vs. local disk
- NAS?

## 🚧 Ingress

- ingress-nginx
- cert-manager
- oauth2-proxy
    - Github OAuth application
    - Restricted access
    - Single-Sign-On

### 🚧 Routes

| Domain       | Name                 | Private | Public |
|--------------|----------------------|---------|--------|
| `grafana`    | Grafana              | ✅       | ✅      |
| `kubernetes` | Kubernetes Dashboard | ✅       | ✅      |
| `pi-hole`    | Pi-hole              | ✅       | ✅      |
| `prometheus` | Prometheus           | ✅       | ❌      |
| `router`     | Fritz!Box UI         | ✅       | ✅      |

## 🚧 Services

- [Grafana](https://grafana.com/)
- [Prometheus](https://prometheus.io/)
- [Kubernetes Dashboard](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)
  
## 🚧 Applications

- [Nextcloud](https://nextcloud.com/)
- [Kodi](https://kodi.tv/)
- [Home-Assistant](https://www.home-assistant.io/)
