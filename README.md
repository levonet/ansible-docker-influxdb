InfluxDB Role
=============

Configure and start InfluxDB in a docker container using the official image `influxdb:latest`.  
[More information](https://hub.docker.com/r/library/influxdb/) about using docker image.

Role Variables
--------------

- `docker_influxdb_name` (default: influxdb): This name used in name of home folder path and in name of container.
- `docker_influxdb_image` (default: influxdb:latest)
- `docker_influxdb_directory_volumes` (optional): Mount folders into docker
- `docker_influxdb_file_volumes` (optional): Mount files into docker
- `docker_influxdb_ports` (default: [8086])
- `docker_influxdb_env` (optional)
- `docker_influxdb_network_mode` (default: host): Connect the container to a network.
- `docker_influxdb_networks` (default: []): List of networks the container belongs to.
- `docker_influxdb_log_driver` (default: json-file): Specify the logging driver.
- `docker_influxdb_log_options` (optional): Dictionary of options specific to the chosen log_driver. See [Configure logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for details.

Dependencies
------------

- `docker`

Example Playbook
----------------

```yaml
- hosts: {{ hosts }}
  become: yes
  become_method: sudo
  roles:
    - role: docker-influxdb
      docker_influxdb_env:
        INFLUXDB_HTTP_LOG_ENABLED: "false"
        INFLUXDB_GRAPHITE_ENABLED: "true"
      docker_influxdb_ports:
        - 8086:8086
        - 2003:2003
      docker_influxdb_log_driver: syslog
      docker_influxdb_log_options:
        syslog-facility: local0
        tag: "{{ docker_influxdb_name }}"
```

License
-------

[MIT](https://opensource.org/licenses/MIT)

Author Information
------------------

This role was created by [Pavlo Bashynskyi](https://github.com/levonet)
