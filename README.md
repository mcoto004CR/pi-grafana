# pi-grafana
##Install Grafana to monitor raspberry vitals

Raspberry metrics
Expose raspberry PI metrics using Grafana and Prometheus:

Example


About
Visualise your Raspberry PI metrics. Very easy installation - requires single command. Supports multiple Raspberries.

This project contains Ansible playbook which installs four services on Raspberry:

Node exporter - exposes Raspberry metrics
rpi_exporter - exposes CPU temperature as Prometheus metric
Prometheus - collects and stores metrics
Grafana - metrics visualization
Scheme

Prerequisites
Raspberry PI with ARMv7 processor (Tested on Raspberry PI 2 Model B)
Debian installed on Raspberry (like Raspbian Buster)
open port 22 on raspberry (SSH)
open port 3000 on raspberry (Grafana)
How to install
Ansible is required for installation.

If you don't have Ansible installed, see Ansible installation.

1. Configure Raspberry IP address
Checkout project.

Edit file ansible/hosts and set Raspberry IP address in main-raspberry group.

If you have more than one Raspberry PI, configure additional Raspberry PI addresses in additional-raspberries group.

Here is the example:

IP_config

The "main" Raspberry will have all 4 services installed (Prometheus, Node exporter, rpi_exporter and Grafana), and the "additional Raspberries" will have Node exporter and rpi_exporter service installed.

The main Raspberry will collect metrics from all additional Raspberries (if configured), so they must be accessible from the main Raspberry.

2. Run ansible playbook
Run Ansible playbook with password authentication:

    cd ansible/
    ansible-playbook raspberry.yml -i hosts -u pi -D -k -K
Or run Ansible playbook with SSH keys authentication:

    cd ansible/
    ansible-playbook raspberry.yml -i hosts -u pi -D
3. Check metrics
Go to Grafana URL http://raspberry:3000/
login with admin/admin
Click on "Raspberry metrics" dashboard:
Dashboard

If you have more than one Raspberry configured, you can select another Raspberry using instance dropdown:
Instance
