+++
Categories = []
Description = "Monitoring"
Tags = ["monitoring", "golang"]
Title = "monitoring"
date = "2016-04-13T23:25:21+02:00"

+++

- [InfluxDB](https://influxdata.com/) The platform for Storing/Managing/Collecting time-series data
- [InfluxDB Client](https://github.com/influxdata/influxdb/tree/master/client) A Go client library written and maintained by the InfluxDB team
- [Grafana](http://grafana.org/) Grafana provides a powerful and elegant way to create, explore, and share dashboards and data with your team and the world

## InfluxDB

InfluxDB is a time series database built from the ground up to handle high write and query loads. InfluxDB is meant to be used as a backing store for any use case involving large amounts of timestamped data, including DevOps monitoring, application metrics, IoT sensor data, and real-time analytics.

#### Key Features

Here are some of the features that InfluxDB currently supports that make it a great choice for working with time series data.

- Custom high performance datastore written specifically for time series data. The TSM engine allows for high ingest speed and data compression.
- Written entirely in Go. It compiles into a single binary with no external dependencies.
- Clustering is built in. Nothing else is needed to make data highly available (unlike Redis, ZooKeeper, Cassandra, and others).
- Simple, high performing write and query HTTP(S) APIs.
- Plugins support for other data ingestion protocols such as Graphite, collectd, and OpenTSDB.
- Expressive SQL-like query language tailored to easily query aggregated data.
- Tags allow series to be indexed for fast and efficient queries.
- Retention policies efficiently auto-expire stale data.
- Continuous queries automatically compute aggregate data to make frequent queries more efficient.
- Built in web admin interface.



### Installation
Installation instructions for OS: **Ubuntu & Debian (64-bit)** and InfluxDB version: **Stable v0.12.1**


1. Download `.deb` file

        wget https://s3.amazonaws.com/influxdb/influxdb_0.12.1-1_amd64.deb

2. Check `.deb` file

        echo '465e6cd66eb6dd23592386ce7d19136f  influxdb_0.12.1-1_amd64.deb' |  md5sum -c

3. Install `.deb` file

        sudo dpkg -i influxdb_0.12.1-1_amd64.deb

### Getting Started

1. Start the `influxd` server by

    * starting the service: `service influxdb start`
    * or running `influxd` directly in a shell

2. Execute `influx` to start the CLI and automatically connect to the local InfluxDB instance

3. Create and show a database

        create database mydb
        show databases


## Grafana

### Install 3.0 Beta
http://docs.grafana.org/installation/debian/

      $ wget https://grafanarel.s3.amazonaws.com/builds/grafana_3.0.0-beta41460581169_amd64.deb
      $ sudo apt-get install -y adduser libfontconfig
      $ sudo dpkg -i grafana_3.0.0-beta41460581169_amd64.deb


### Start the server (init.d service)

Start Grafana by running:

      $ sudo service grafana-server start

This will start the grafana-server process as the grafana user, which was created during the package installation. The default HTTP port is 3000 and default user and group is admin.

To configure the Grafana server to start at boot time:

      $ sudo update-rc.d grafana-server defaults 95 10
