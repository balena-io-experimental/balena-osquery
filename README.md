# balena-osquery
Experiment on running osquery as a container in a balenaCloud device

## Getting started
1. Clone the repo.
1. Push it to a aarch64 balenaCloud app (eg Raspberry Pi 3 64bit or Raspberry Pi 4).
1. Wait for your device to download the release.
1. SSH to the device.
1. Run `osqueryi` to start the osquery shell.
1. Start running your osquery commands.

For example running `SELECT name, path, pid FROM processes` should print something like:
```
+----------+-------------------+-----+
| name     | path              | pid |
+----------+-------------------+-----+
| osqueryd | /usr/bin/osqueryd | 1   |
| osqueryd | /usr/bin/osqueryd | 17  |
| bash     | /bin/bash         | 28  |
| osqueryi | /usr/bin/osqueryd | 37  |
+----------+-------------------+-----+
```
