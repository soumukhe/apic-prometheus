# apic-prometheus
This docker-compose code was copied from https://github.com/vegasbrianc/prometheus
Slight Modifications were made for ease of use with APIC/cAPIC

# Requirements:  
VM with ubuntu and docker/docker-compose installed.  If you don't have that, please look at the bottom of this README file

# Steps to install:
1) ssh to ubuntu box and clone this repo:  git clone https://github.com/soumukhe/apic-prometheus.git
2) cd apic-prometheus
3) docker-compose up -d 
4) make sure to do a docker ps to verify that all 8 associated containers are up and running

```
You should have 5 cotainers running as shown below:

docker ps --format '{{ .Names }}' | sort |nl
     1  apic-prometheus_alertmanager_1
     2  apic-prometheus_cadvisor_1
     3  apic-prometheus_grafana_1
     4  apic-prometheus_node-exporter_1
     5  apic-prometheus_prometheus_1
        
```

# Configuring for APIC and Prometheus:
Please see unofficalaciguide.com

# In case you don't have a vm with docker/docker-compose, follow these steps first to install:
```
1) Download Ubuntu 20.04 --  https://ubuntu.com/download/desktop
2) Install Ubuntu VM minimum version
3) update/upgrade ubuntu and install basic utils: 
   sudo -i
   apt update && apt upgrade -y
   apt auto-remove
   apt install -y curl wget vim openssh-server
4) Install docker and docker-compose:
   ssh to your Ubuntu VM on backend APIM EPG
   sudo -i
   apt-get update && apt-get upgrade -y
   echo net.ipv4.ip_forward=1 >> /etc/sysctl.conf
   sysctl -p
   sudo sysctl --system
   exit 
   sudo apt install docker.io -y
   sudo systemctl start docker
   sudo systemctl enable docker
   sudo groupadd docker
   sudo usermod -aG docker $USER
   exit # and ssh back in for this to work
   docker --version
   sudo apt install docker-compose -y
