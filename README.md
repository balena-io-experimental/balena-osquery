# balena-osquery
Experiment on running osquery as a container in a balenaCloud device

## Getting started
1. Clone the repo.
1. Push it to a aarch64 balenaCloud app (eg Raspberry Pi 3 64bit or Raspberry Pi 4).
1. Wait for your device to download the release.
1. SSH to the `osquery` service.
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

Note: the data returned by osquery is related to the container, if you want to query
information about the host, you should make sure to enable the correct feature by using 
the appropriate [Balena label](https://www.balena.io/docs/reference/supervisor/docker-compose/#labels), 
e.g. `io.balena.features.procfs` to mount the proc subsystem.

## Querying docker status using osquery

1. In order to query docker status, the docker socket must be mounted in the container
by using the `io.balena.features.balena-socket` label.
2. Run the osquery shell by passing the location of the socket as stated by 
the [osquery documentation](https://osquery.readthedocs.io/en/latest/installation/cli-flags/#docker-flags): 
`osqueryi --docker_socket=/var/run/balena-engine.sock` 
3. Query any of the docker tables in the [osquery schema](https://osquery.io/schema/4.5.1/#docker_containers), for example:
```
osquery> select name, status from docker_containers;
+-------------------+----------------------+
| name              | status               |
+-------------------+----------------------+
| /osquery_1_1      | Up 24 minutes        |
| /resin_supervisor | Up 2 hours (healthy) |
+-------------------+----------------------+
```
