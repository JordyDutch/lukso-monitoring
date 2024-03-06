# LUKSO monitoring

Docker setup for ONLY the monitoring of LUKSO node as created by @lykhonis in [his guide](https://github.com/lykhonis/lukso-node/tree/main). 

## Setup

#### Prerequisites

1. Docker. Install it by following [few steps](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository).

#### Setup Environment

```shell
cp .env.example .env
```

#### Monitoring

Enable monitoring by setting up your password to grafana and secure access. Set password in `.env` file for `GRAFANA_PASSWORD=`:

```shell
nano .env
```

Open port for grafana
```
sudo ufw allow 46321/tcp
```

Setup secure access:

```shell
cd grafana/etc
sudo openssl genrsa -out grafana.key 2048
sudo openssl req -new -key grafana.key -out grafana.csr
sudo openssl x509 -req -days 365 -in grafana.csr -signkey grafana.key -out grafana.crt
sudo chmod 400 grafana.key grafana.crt
```

## Start

```shell
sudo docker compose up -d
```

to stop run:

```shell
sudo docker compose down
```

## Monitor

Replace IP address with your node's IP and navigate to `https://IP:46321`. Select advance settings and proceed to an unsafe connection if prompted by a web browser. It may take some time to fully sync the chain, but some metrics should be populated within few minutes.
