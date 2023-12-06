# K8s

## Applications

### [Syncthing](https://syncthing.net/)

Syncs files between devices.

- pvc
<!-- - samba:ro -->

### [Changedetection.io](https://changedetection.io/)

Monitors websites for changes.

- pvc
- no samba

### [Transmission](https://transmissionbt.com/) + [VPN](https://github.com/haugene/docker-transmission-openvpn)

Torrent client with VPN. [There is an image that combines both](https://github.com/haugene/docker-transmission-openvpn).

- pvc
- samba:rw

### [Jellyfin](https://jellyfin.org/)

A Media server with DLNA.

- pvc
- samba:rw

### [Immich](https://github.com/immich-app/immich)

A web app for managing a collection of movies and series.

- pvc
- samba:ro

### Samba

We need a way to connect to the storage from PCs, because that is ez.

We can use the samba operator: https://github.com/samba-in-kubernetes/samba-operator

### ArgoCD

Manages the cluster, deploys applications, etc.

### [Velero](https://velero.io/)

Backup and restore for Kubernetes using blackblaze b2 as external storage.

### Traefik + Let's Encrypt

Manages routing into services using the domain name. Also manages SSL certificates using [Let's Encrypt](https://letsencrypt.org/).

[How to Install](https://traefik.io/blog/secure-web-applications-with-traefik-proxy-cert-manager-and-lets-encrypt/)

Requirements:

- [Traefik](https://traefik.io/traefik/)
- [Cert-manager](https://cert-manager.io/docs/installation/kubernetes/)

Routes:

| Service               | Domain                            | notes  |
| --------------------- | --------------------------------- | ------ |
| Traefik - Dashboard   | traefik.localhost                 | local  |
| ArgoCD - Dashboard    | argocd.localhost                  | local  |
| Changedetection.io    | (changedetection \| cd).localhost | public |
| Jellyfin              | jellyfin.localhost                | public |
| Syncthing - service   | syncthing.localhost               | public |
| Syncthing - dashboard | syncthing.localhost               | local  |
| Immich                | immich.localhost                  | public |
| Samba                 | ---                               | local  |

### Cloudflare tunnel

Allows us to connect to the cluster from anywhere. Preferably we connect tunnel pod to the ingress.

Cloudflare should only have access public facing ingress routes.

## Security

Stuff enters via CloudFlared Tunnel. This tunnel should only have access to Ingress/Traefik, and nothing else.
Traefik should not have access to anything, only to the ingress routes.

All pods should default to not having access to anything, and only have access to what they need by using network policies.

## Phase 1:

Applications:

- Traefik
- Tunnel
- ArgoCD

Configuration:
- Traefik ingress route to ArgoCD
- Block all traffic by default
- Allow traffic from tunnel to ingress (traefik)
- Allow traffic from traefik to ingress routes
- 
