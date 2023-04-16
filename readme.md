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
  - Review all the metrics and collapse or delete the sections not relevant to you, or where your setup does not provide dat.

At this point the dashboard and it's variables should explore the schema and data in the bucket and find all hosts and devices for which metrics are available.
The telegraf installation can be rolled out to a fleet of servers or PCs and all of them monitored in one dashboard. The **ansible_gist.yaml** in this repository allows automated rollout of the telegraf installation to more hosts by using ansible.

## Upgrading

### Dashboard

If a new release tag comes out, simply create a new dashboard and import the updated dashboard.json file. This provides a new dashboard with all the features.

### Telegraf configuration

In case there were changes to the gathered data (which may well be the case on any major release tag), replace the telegraf.conf file with the new version and restart the telegraf service (or execute the command in the ansible_gist.yaml to automate the process).

## Screenshots

![Screenshot](screenshots/Screenshot%20from%202023-02-11%2017-37-46.png)
![Screenshot](/screenshots/Screenshot%20from%202023-02-11%2017-38-05.png)
![Screenshot](/screenshots/Screenshot%20from%202023-02-13%2022-52-55.png)
![Screenshot](/screenshots/Screenshot%20from%202023-02-13%2022-53-18.png)
![Screenshot](/screenshots/Screenshot%20from%202023-02-13%2022-54-01.png)
![Screenshot](/screenshots/Screenshot%20from%202023-02-11%2017-38-17.png)
![Screenshot](/screenshots/Screenshot%20from%202023-02-11%2017-38-47.png)
![Screenshot](/screenshots/netstat.png)
![Screenshot](/screenshots/Screenshot%20from%202023-02-11%2017-39-24.png)
![Screenshot](/screenshots/drives_summary.png)
![Screenshot](/screenshots/smart_device_all_overview.png)
![Screenshot](/screenshots/smart_device_numeric_detail.png)
![Screenshot](/screenshots/smart_attribute_reallocated_sector.png)
![Screenshot](/screenshots/smart_attribute_temperature.png)
![Screenshot](/screenshots/smart_attribute_total_lba_written.png)
![Screenshot](/screenshots/Screenshot%20from%202023-02-11%2017-42-05.png)
![Screenshot](/screenshots/Screenshot%20from%202023-02-11%2017-42-40.png)

## Tags

#### v3.1 Expanded panels for smart attributes
  - Added installation, usage and upgrade instructions, plus dashboard export instructions to readme
  - Added variable to read all smart attribute names to make them selectable and allow automatic replication of panels for each selected attribute. Updated screenshots in readme.
  - Now enables 'multi-value' for all variables where it makes sense, like smart attributes, drives, containers, etc.
  - Renaming of several section and panel headers to make it more clear which variable changes will affect which graphs.
  - Added these 'tag notes'
  
#### v3.0 Added netstat metrics
  - Enabled netstat in docker config file to gather the data
  - Added dashboard panel for netstat
  - Included minor dashboard.json changes caused by Grafana update (Grafana included it in the exported json file)
  Bugfix:
  - Also enabled the docker metrics in telegraf.conf, which were missing.

#### v2.1 Bug fix
  - To read docker metrics the 'telegraf' user must have access to the docker engine. Added telegraf to the 'docker' group.
  
#### v2.0 Added Docker metrics
  - Telegraf gets access to docker engine to pull all metrics
  - Variable added in grafana to detect and select all containers
  - Added docker engine overview and container specific metrics
  
#### v1.0 Initial release

## Contributing

- Please report bugs as issues on GitHub. If you have an idea how to improve it, please include that too!
- When providing a pull request, please make sure to use a clean copy and extract the post-change dashboard.json as instructed below.

## Dashboard export

It is possible to review and modify the 'json model' of the dashboard in the dashboard settings. However, this json representation of the dashboard is not portable to other installations. In order to create a 'generalised' export, wich can be imported on other systems, these steps must be taken:

- In Grafana click the 'Share dashboard or panel' button in the top left cordner (three connected circles)
- Select 'export'
- Enable 'Export for sharing externally'
- Select 'Save to file'

## License

MIT

## Author

Created in 2023 by Damian Hurschler