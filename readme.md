# Grafana Dashboard for Telegraf with flux queries (influxdb_v2)

Basic health and usage monitoring of any host running Telegraf. All queries are written in flux, requireing influxdb 2.x.

## Included in the package

- **ansible_gist.yaml** - install and configure telegraf, including mod to sudoers file to allow telegraf to run /usr/sbin/smartctl and /usr/sbin/nvme.
- **telegraf.conf** - to send all required metrics to influxdb_v2 to drive the dashboard
- **grafana_dashboard.json** - the dashboard definition

## Screenshots

![Screenshot](screenshots/Screenshot%20from%202023-02-11%2017-37-46.png)
![Screenshot](screenhot/../screenshots/Screenshot%20from%202023-02-11%2017-38-05.png)
![Screenshot](screenhot/../screenshots/Screenshot%20from%202023-02-11%2017-38-17.png)
![Screenshot](screenhot/../screenshots/Screenshot%20from%202023-02-11%2017-38-47.png)
![Screenshot](screenshot/../screenshots/Screenshot%20from%202023-02-11%2017-39-24.png)
![Screenshot](screenshot/../screenshots/Screenshot%20from%202023-02-11%2017-40-15.png)
![Screenshot](screenshot/../screenshots/Screenshot%20from%202023-02-11%2017-40-29.png)
![Screenshot](screenshot/../screenshots/Screenshot%20from%202023-02-11%2017-42-05.png)
![Screenshot](screenshot/../screenshots/Screenshot%20from%202023-02-11%2017-42-40.png)

## License

MIT