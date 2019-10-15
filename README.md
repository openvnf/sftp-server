# SFTP Server

A helm chart for a SFTP server.

This chart is a fork of [openvnf/sftp-server](https://github.com/openvnf/sftp-server)
The extra features added in this fork:
- Included pull request fixing a missing indent in sftp-container resource definition (https://github.com/openvnf/sftp-server/pull/6)
- Support for multiple users having different passwords and mounting different paths on a persistent volume. This allows to configure 2 users, one for external, more limited access, and one for internal, less limited access
- Support for init script
- Changing the default image to atmoz/sftp


## Introduction

The SFTP server is based on [atmoz/sftp](https://github.com/atmoz/sftp).

The chart supports:
- persistent SSH server host keys
- provision of authorized SSH keys
- persistentVolumeClaim for data
- [kube-vxlan-controller](https://github.com/openvnf/kube-vxlan-controller)


## Prerequisites

- Kubernetes 1.6+ with Beta APIs enabled


## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release repo/sftp-server
```

The command deploys an SFTP server exposing the service as `ClusterIP`. The [configuration](#configuration) section lists the parameters that can be configured during installation.


## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the SFTP server chart and their default values.

|          Parameter                 |                Description                 |                   Default                   |
| -----------------------------------| ------------------------------------------ | ------------------------------------------- |
| `image.repository`                 | Docker repo to use                         | `atmoz/sftp`                                |
| `image.tag`                        | Docker tag to be used                      | `alpine-3.7`                                |
| `image.pullPolicy`                 | Image pull policy                          | `IfNotPresent`                              |
| `service.enabled`                  | If true, expose as Service                 | `true`                                      |
| `service.type`                     | Type of exposed Service                    | `ClusterIP`                                 |
| `service.port`                     | Port to expose Service                     | `22`                                        |
| `sftpConfig.users.username`        | SFTP username                              | `sftp`                                      |
| `sftpConfig.users.password`        | SFTP password for user                     | `""`                                        |
| `sftpConfig.users.encrypted`       | If true, password is given as hash         | `false`                                     |
| `sftpConfig.users.uid`             | UID of SFTP user                           | `1000`                                      |
| `sftpConfig.users.gid`             | GID of SFTP user                           | `100`                                       |
| `sftpConfig.users.authorizedKeys`  | list of authorized SSH keys                | `{}`                                        |
| `sftpConfig.users.mountPath`       | Path to mount an existing volume           | `"/home/sftp/ftp"`                          |
| `sftpConfig.users.subPath`         | Use subPath of existing volume             | `""`                                        |
| `sftpConfig.hostKeys.secret`       | name of secret for SSH host keys           | `""`                                        |
| `sftpConfig.hostKeys.keys`         | list of items to be used from secret       | `{}`                                        |
| `persistentVolume.enabled`         | If true, use persistent volume             | `true`                                      |
| `persistentVolume.annotations`     | annotations put on the volume              | `{}`                                        |
| `persistentVolume.accessModes`     | access modes for volume                    | `[ReadWriteOnce]`                           |
| `persistentVolume.existingClaim`   | If set, use existing PVC                   | `""`                                        |
| `persistentVolume.size`            | Size of volume                             | `20Gi`                                      |
| `persistentVolume.storageClass`    | StorageClass to be used in PVC             | not set                                     |
| `init.enabled`                     | If true, use an init script                | `false`                                     |
| `init.script`                      | The content of init script                 | `""`                                        |
| `vxlanController.enabled`          | If enabled, start kube-vxlan-controller    | `false`                                     |
| `vxlanController.annotationKey`    | Annotation name to set for vxlan           | `vxlan.openvnf.org/networks`                |
| `vxlanController.metadataKey`      | Metadata key to set for vxlan              | `vxlan.openvnf.org`                         |
| `vxlanController.image.repository` | Docker repo to use                         | `openvnf/kube-vxlan-controller-agent`       |
| `vxlanController.image.tag`        | Docker tag to be used                      | `2.1.0`                                     |
| `vxlanController.image.pullPolicy` | Image pull policy                          | `IfNotPresent`                              |
| `vxlanController.network`          | VXLAN network to attach to                 | `vxeth0`                                    |
| `vxlanController.ip`               | IP address to assign to vxlan interface    | `{}`                                        |
| `vxlanController.route`            | additional route to configure              | `{}`                                        |
