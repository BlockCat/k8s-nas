# Talos

Talos is a modern OS for Kubernetes. It is designed to be secure, immutable, and minimal.

```bash
talosctl gen config blockcat-nas https://192.168.?.?
talosctl --talosconfig talosconfig config endpoint 192.168.?.?
talosctl --talosconfig talosconfig config node 192.168.?.?
```

```bash
talosctl --nodes 192.168.0.2 --endpoints 192.168.0.2 health \
   --talosconfig=./talosconfig
talosctl --nodes 192.168.0.2 --endpoints 192.168.0.2 dashboard \
   --talosconfig=./talosconfig
```