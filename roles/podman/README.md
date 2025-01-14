# podman

This role installs podman.

## DNS resolution

The default podman network `podman` does not support DNS resolution of container names. This role creates a new network, which has this feature enabled. By default this network is named `podman-dns`, you can change the name by setting `podman__dns_enabled_network: customName`. Add your containers to this network if you need DNS resolution.

If you don't need this feature, set `podman__dns_enabled_network: False`

## nftables

By default this role will create a nftables config, which is necessary for communication between containers. If you don't need this feature, set `podman__nftables_config: False`

## Auto update

see <https://silentlad.com/systemd-timers-oncalendar-(cron)-format-explained>
see  <https://docs.podman.io/en/latest/markdown/podman-auto-update.1.html>

```yaml
podman__auto_update_time: # defaults to Monday 02:00 Datetime string in Systemd Timer OnCalendar Format
podman__auto_update: true # (default)
```

## other registries

Other registries can be added with following configuration:

```YAML
podman__proxy_registry_my_registry:
  prefix: "my_registry.io"
  location: "my_registry.io"
```

will result in following registry config:

```INI
[[registry]]
prefix = "my_registry.io"
location = "my_registry.io"
```

## Proxy cache

The ZIH-Harbor instance can be used as a proxy cache for the registries `ghcr.io` and `docker.io` by adding the variables:

```YAML
podman__proxy_registry_docker:
  prefix: "docker.io"
  location: "harbor.zih.tu-dresden.de/proxy_cache"
podman__proxy_registry_ghcr:
  prefix: "ghcr.io"
  location: "harbor.zih.tu-dresden.de/proxy_cache_ghcr_io"
```

alternatively the server can be added to the group `linux`
