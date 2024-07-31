# Talos

Talos is a modern OS for Kubernetes. It is designed to be secure, immutable, and minimal.

## Installing

Install according to the official documentation.

- [Talosctl](https://www.talos.dev/v1.7/talos-guides/install/talosctl/)
- [Talos using ISO](https://www.talos.dev/v1.7/talos-guides/install/bare-metal-platforms/iso/)

```bash
# set configuration
talosctl config endpoint 192.168.?.?
talosctl config node 192.168.?.?
```

## Check stuff

```bash
 talosctl dashboard
talosctl health
talosctl apply-config -f controlplane.yaml # apply the controlplane.yaml
talosctl apply-config -f controlplane.yaml -p '@patch.yaml' # apply the controlplane.yaml with patch.yaml
```

## Update

```bash
talosctl --talosconfig=./talosconfig upgrade --image ghcr.io/siderolabs/installer:v1.7.5 --preserve
talosctl --talosconfig=./talosconfig version
```

```bash
helm install cilium cilium/cilium --version 1.16.0 --namespace kube-system --set ipam.mode=kubernetes --set kubeProxyReplacement=true --set securityContext.capabilities.ciliumAgent="{CHOWN,KILL,NET_ADMIN,NET_RAW,IPC_LOCK,SYS_ADMIN,SYS_RESOURCE,DAC_OVERRIDE,FOWNER,SETGID,SETUID}" --set securityContext.capabilities.cleanCiliumState="{NET_ADMIN,SYS_ADMIN,SYS_RESOURCE}" --set cgroup.autoMount.enabled=false --set cgroup.hostRoot=/sys/fs/cgroup --set k8sServiceHost=localhost --set k8sServicePort=7445


helm upgrade cilium cilium/cilium --version 1.16.0 --namespace kube-system --reuse-values --set externalIPs.enabled=true --set l2announcements.enabled=true --set l2announcements.leaseDuration="3s" --set l2announcements.leaseRenewDeadline="1s" --set l2announcements.leaseRetryPeriod="500ms" --set k8sServiceHost=localhost --set k8sServicePort=7445 --set devices="{eno1}"
```