# Grafana Dashboard for Telegraf with flux queries (influxdb_v2)

Visualise health and usage data gathered by Telegraf:
- Host System Metrics
- Docker Engine and Docker Container Metrics

The data is stored in an influxdb 2.x and queried using Flux.

## Included in the package

- **ansible_gist.yaml** - install and configure telegraf, including mod to sudoers file to allow telegraf to run /usr/sbin/smartctl and /usr/sbin/nvme.
- **telegraf.conf** - to send all required metrics to influxdb_v2 to drive the dashboard
- **grafana_dashboard.json** - the dashboard definition

## Installation and usage

- Modify the **telegraf.conf** to include your influxdb_v2 installation in the '[[outputs.influxdb_v2]]' section. 
  - You may want to disable 'insecure_skip_verify = true' in case you don't use self-signed certificates.
- Install telegraf on the to-be-monitored host and use the above **telegraf.conf** configuration file to configure telegraf. This will provide all the required, and only those, parameters to the influxdb_v2.
- On a Graphana instance with the influxdb_v2 configured as data source, create a new dashboard and select 'import'
  - select 'upload dashboard JSON file' and select the **grafana_dashboard.json** from this repository
  - select the influsdb_v2 data source where telegraf is sending it's metrics to
  - Open the dashboard and at the top select the bucket to which telegraf is sending it's metrics to

At this point the dashboard and it's variables should explore the schema and data in the bucket and find all hosts and devices for which metrics are available.
The telegraf installation can be rolled out to a fleet of servers or PCs and all of them monitored in one dashboard. The **ansible_gist.yaml** in this repository allows automated rollout of the telegraf installation to more hosts by using ansible.

## Screenshots

![Screenshot](screenshots/Screenshot%20from%202023-02-11%2017-37-46.png)
![Screenshot](screenhot/../screenshots/Screenshot%20from%202023-02-11%2017-38-05.png)
![Screenshot](screenshot/../screenshots/Screenshot%20from%202023-02-13%2022-52-55.png)
![Screenshot](screenshot/../screenshots/Screenshot%20from%202023-02-13%2022-53-18.png)
![Screenshot](screenshot/../screenshots/Screenshot%20from%202023-02-13%2022-54-01.png)
![Screenshot](screenhot/../screenshots/Screenshot%20from%202023-02-11%2017-38-17.png)
![Screenshot](screenhot/../screenshots/Screenshot%20from%202023-02-11%2017-38-47.png)
![Screenshot](screenhot/../screenshots/Netstat.png)
![Screenshot](screenshot/../screenshots/Screenshot%20from%202023-02-11%2017-39-24.png)
![Screenshot](screenshot/../screenshots/Screenshot%20from%202023-02-11%2017-40-15.png)
![Screenshot](screenshot/../screenshots/Screenshot%20from%202023-02-11%2017-40-29.png)
![Screenshot](screenshot/../screenshots/Screenshot%20from%202023-02-11%2017-42-05.png)
![Screenshot](screenshot/../screenshots/Screenshot%20from%202023-02-11%2017-42-40.png)

## License

MIT

## Author

Created in 2023 by Damian Hurschler