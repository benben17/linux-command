# linux-command

Helm Chart for `linux-command`. This chart bootstraps a `linux-command` deployment on a Kubernetes cluster using the Helm package manager.

## Installing the Chart

```bash
$ helm install linux-command ./linux-command --namespace linux-command --create-namespace
```

## Uninstalling the Chart

```bash
$ helm -n linux-command uninstall linux-command
```

This will remove all Kubernetes components associated with the chart and delete the release.

## Configuration Parameters

The following table lists the configurable parameters of the `linux-command` chart and their default values.

| Key                                                          | Type   | Default                   | Description |
| ------------------------------------------------------------ | ------ | ------------------------- | ----------- |
| linuxCommand.linuxCommandContainer.image.repository          | string | `"wcjiang/linux-command"` |             |
| linuxCommand.linuxCommandContainer.image.tag                 | string | `"latest"`                |             |
| linuxCommand.linuxCommandContainer.imagePullPolicy           | string | `"IfNotPresent"`          |             |
| linuxCommand.linuxCommandContainer.resources.limits.cpu      | string | `"100m"`                  |             |
| linuxCommand.linuxCommandContainer.resources.limits.memory   | string | `"50Mi"`                  |             |
| linuxCommand.linuxCommandContainer.resources.requests.cpu    | string | `"100m"`                  |             |
| linuxCommand.linuxCommandContainer.resources.requests.memory | string | `"50Mi"`                  |             |
| linuxCommand.replicas                                        | int    | `1`                       |             |
| service.ports[0].port                                        | int    | `9665`                    |             |
| service.ports[0].protocol                                    | string | `"TCP"`                   |             |
| service.ports[0].targetPort                                  | int    | `3000`                    |             |
| service.type                                                 | string | `"NodePort"`              |             |

Each parameter can be specified for `helm install` using the `--set key=value[,key=value]` argument.

Alternatively, you can provide a YAML file specifying the values when installing the chart. For example:

```bash
helm install <release-name> -f values.yaml ./linux-command
```
