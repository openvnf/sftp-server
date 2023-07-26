# Changelog

## pre 1.0

### 0.4.0
* Add initScript container capability
* Bump nettools container image v1.10.0 -> v1.12.0
* Add additionalAnnotations
* Add additionalLabels
* Add imagePullSecrets

### 0.3.2

* add .helmignore for a clean chart

### 0.3.1

* Move debug container to first position to make it the default target for container attachments.
* Fix inclusion of resource definitions.

### 0.3.0

* Added `NET_ADMIN` capabilities to the sftp-server container.
* Added nettools-debug containers (disabled by default)
* Changed sftp resource-definition from .resources to resources.sftp

### 0.2.0

* change update strategy to `Recreate` to prevent deadlock on PV allocation

### 0.1.1

* change image repository to `quay.io/openvnf/sftp`
