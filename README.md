# Elk-Project

The files in this repository were used to create an Elk server deployment in Microsoft Azure.

Network Topology
This network leverages an instance of DVWA that is fully load balanced and automated. This is to ensure redundancy and availability of the network. The Elk server acts as the monitor to identify and changes or vulnerable VMs.

Access Policies
Since all the machines on the internal network are not accessible by the public Internet, only the Jump Box can connect to the public Internet. To access the machines on the network, you must access them through the Ansible container on the Jump Box where a public key is generated in the Ansible Docker container. To view Kibana, my personal computer was given access to port 5601 on the Elk machine. Below is an outline of the policies in place.
Jump Box - Publicly accessible - Local IPv4 allowed
Web-1 - Not publicly accessible - 10.0.0.4 allowed
Web-2 - Not publicly accessible - 10.0.0.4 allowed
Web-3 - Not publicly accessible - 10.0.0.4 allowed
Elk - Not publicly accessible - 10.0.0.4 allowed

Elk Configuration Overview
The playbook created does the following
 - install docker
 - install python3
 - install Docker pip
 - download Docker image
 - Enable Docker 
Run sudo docker ps to check the status.

Beat Files Overview
This setup allows the Elk server to control and monitor 10.0.0.7/8/9
Filebeat is responsible for collecting log files for the servers. Metricbeat collects metric such as uptime, CPU usage, memory, and more metrics pertaining to the Docker containers.

Playbook Overview
Use curl command to download filebeat-config.yml
Use curl command to download metricbeat-config.yml
nano into the .yml files to include Elk server private IP, alsi include the webservers we want to install on.

[elk]
10.1.0.4 ansible_python_interpreter=/usr/bin/python3

[webservers]
10.0.0.7 ansible_python_interpreter=/usr/bin/python3
10.0.0.8 ansible_python_interpreter=/usr/bin/python3
10.0.0.9 ansible_python_interpreter=/usr/bin/python3

Run ansible-playbook [playbook name] comamnd. Enter the Elk machine public IP:5601 and it brings up Kibana. Click Check Data to verify successful installation (refer to screenshots)

Finally, run the stress.yml file to collect data on CPU usage. If successful, all machines should read 100%.
