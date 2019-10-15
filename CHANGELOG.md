# Changelog

## pre 1.0

### 0.4.0

 * Added support for multiple users having different passwords and mounting different paths on a persistent volume
 * Added support for init script

### 0.3.0

* Added `NET_ADMIN` capabilities to the sftp-server container.
* Added nettools-debug containers (disabled by default)
* Changed sftp resource-definition from .resources to resources.sftp

### 0.2.0

* change update strategy to `Recreate` to prevent deadlock on PV allocation

### 0.1.1

* change image repository to `quay.io/openvnf/sftp`
