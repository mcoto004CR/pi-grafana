# Install Grafana to monitor raspberry vitals

Based on project: https://github.com/bhemar/raspberry-metrics

Raspberry metrics
Expose raspberry PI metrics using Grafana and Prometheus:

<img src="https://github.com/mcoto004CR/pi-grafana/blob/master/raspberry-metrics-master/preview/Screen_Shot.jpg">

This project contains Ansible playbook which installs four services on Raspberry:

    Node exporter - exposes Raspberry metrics
    rpi_exporter - exposes CPU temperature as Prometheus metric
    Prometheus - collects and stores metrics
    Grafana - metrics visualization
    Scheme

## Prerequisites
-Raspberry PI with ARMv7 processor (Tested on Raspberry PI 2 Model B)
-Debian installed on Raspberry (like Raspbian Buster)
-open port 22 on raspberry (SSH)
-open port 3000 on raspberry (Grafana)

Note: If you don't have Ansible installed, see Ansible installation.
https://geektechstuff.com/2019/06/25/installing-ansible-raspberry-pi/

## Configure Raspberry IP address
Edit file ansible/hosts and set Raspberry IP address in main-raspberry group.
If you have more than one Raspberry PI, configure additional Raspberry PI addresses in additional-raspberries group.

<img src="https://github.com/mcoto004CR/pi-grafana/blob/master/raspberry-metrics-master/preview/raspberry_IP_config.jpg">

The "main" Raspberry will have all 4 services installed (Prometheus, Node exporter, rpi_exporter and Grafana), and the "additional Raspberries" will have Node exporter and rpi_exporter service installed.

The main Raspberry will collect metrics from all additional Raspberries (if configured), so they must be accessible from the main Raspberry.

## Run ansible playbook
Run Ansible playbook with password authentication:

    cd ansible/
    ansible-playbook raspberry.yml -i hosts -u pi -D -k -K

Or run Ansible playbook with SSH keys authentication:

    cd ansible/
    ansible-playbook raspberry.yml -i hosts -u pi -D

## Check metrics

      Go to Grafana URL http://raspberry:3000/
      login with admin/admin
      Click on "Raspberry metrics" dashboard:
      Dashboard

If you have more than one Raspberry configured, you can select another Raspberry using instance dropdown:
Instance


