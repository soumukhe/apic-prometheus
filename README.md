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
You should have 8 cotainers running as shown below:

aciadmin@DMZ-Ubuntu-Jump-User:~/ndi-kafka-elasticsearch-kibana$ docker ps --format '{{ .Names }}' | sort |nl
     1  broker
     2  elasticsearch
     3  kafkacat
     4  kafka-connect
     5  kibana
     6  ksqldb
     7  schema-registry
     8  zookeeper
     
after the containers come up, please repeat the command "docker ps --format '{{ .Names }}' | sort |nl"  after a few minutes.
What I noticed is that ksqldb might have crashed.  If this is the case,  just do "docker-compose up -d" again and then ksqldb will be stable

you can always check logs for ksqldb by:   docker logs -f ksqldb
    
```

# Configuring NDI to export data:
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
