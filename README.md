# apic-prometheus
This docker-compose code was copied from https://github.com/vegasbrianc/prometheus
Slight Modifications were made for ease of use with APIC/cAPIC

# Requirements:  
VM with ubuntu and docker/docker-compose installed.  If you don't have that, please look at the bottom of this README file

# Steps to install:
```
1) You need to have a VM that's already running docker and docker-compose. In case you don't have this and need help, please see the bottom part or the readme file 
2) git clone https://github.com/soumukhe/prometheus.git
3) cd apic-prometheus/prometheus
4) vi prometheus.yml and modify line 65, 69, 74, 78 as appropriate
5) Add more APICs/cAPICs as appropriate as indicated in line 82
   65   - job_name: 'aws-capic'        # Please change this and put in an appropriate job name here like Fabric1-apic
   66     scheme: https
   67     metrics_path: '/nodeexporter/metrics'
   68     static_configs:
   69             - targets: ['x.x.x.x']    # Please change this and substitute your IP for APIC here
   70     tls_config:
   71       insecure_skip_verify: true
   72 
   73 
   74   - job_name: 'azure-capic'       # Please change this and put in an appropriate job name here like Fabric1-apic
   75     scheme: https
   76     metrics_path: '/nodeexporter/metrics'
   77     static_configs:
   78       - targets: ['y.y.y.y']    # Please change this and substitute your IP for APIC here
   79     tls_config:
   80       insecure_skip_verify: true
   81 
   82 # Please add more APICs here for different fabrics as needed.  Remember you need APIC version >= 5.3  or cAPIC >=25.x
```
```
6) docker-compose up -d
7) You should have 5 cotainers running as shown below:

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
   ssh to your Ubuntu VM 
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
