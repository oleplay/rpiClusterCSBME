# Docker Swarm monitoring 

The goal of this project is to deploy [Prometheus](https://prometheus.io/) and [Grafana](http://grafana.org/) monitoring on a Raspberry Pi Swarm cluster.

It's fully deployable via a single docker-compose file.

This project was created during the IT project week by Lisa, Tom and Ole.

It's greatly inspired by the fantasic [swarmprom](https://github.com/stefanprodan/swarmprom) project of [Stefan Prodan](https://github.com/stefanprodan)

## Hardware

Our Hardware was a asortment of different Raspberry Pis

* 1 Pi 4 2GB (Manager node)
* 4 Pi 3 B+
* 2 Pi 3 B

## Prerequisites:

* Docker CE ([instructions](https://docs.docker.com/engine/install/debian/#install-using-the-convenience-script))
* Docker Compose ([instructions](https://docs.docker.com/compose/install/))
* Docker Swarm cluster with one manager and at least one worker ([instructions](https://docs.docker.com/engine/swarm/swarm-tutorial/create-swarm/))
* Docker Daemon metrics exposed on `0.0.0.0:9323` for all nodes ([instructions](https://docs.docker.com/config/daemon/prometheus/))

## Deployed services
`<swarm-ip>` = IP of any Swarm node
* [prometheus](https://prometheus.io/) (metric collector and database) `http://<swarm-ip>:9090`
* [grafana](https://grafana.com/) (visualizer) `http://<swarm-ip>:3000`
* [node-exporter](https://github.com/prometheus/node_exporter) modified [version](https://github.com/oleplay/swarmprom-node-exporter) (host metrics)
* [cadvisor](https://github.com/google/cadvisor) ARM [version](https://github.com/ZCube/cadvisor-docker) (container metrics)
* [docker-exporter](https://github.com/stefanprodan/dockerd-exporter) updated [version](https://hub.docker.com/r/oleplayt/swarmprom-node-exporter) (Docker daemon metrics )
* [caddy](https://caddyserver.com/) (reverse proxy)

## Install

Clone this repo on the manager node and deploy the stack

```bash
git clone https://github.com/oleplay/rpiClusterCSBME
cd rpiClusterCSBME

docker stack deploy -c docker-compose.yml mon
```

## Grafana

### Dashboards:
* 