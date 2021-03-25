## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.



These files have been tested and used to generate a live ELK deployment on AWS. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible_config.yml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting incoming traffic to the network.
Load balancers will help protect against the aspects of SQL injection and cross site scripting. This Jump Box will provide a high level of security to the databases and webservers by making them inaccessible to the public internet. It will accomplish by using a complicated/generated key or .pem file and using the SSH protocols. The Jump Box will also house and run the needed containers and images to allow the webservers and databases to comminute.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- When Filebeat is deployed it will monitor the network simplify the data logs to be reviewed at a later time/date
- When metricbeat is added it will record the statistical data from the OS, such as CPU usage and RAM usage, and record services running on the server. Although metricbeats is not deployed in my network this is a highly recommended practice.   

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Operating System 	|       Name      	|    Subnet    	| Access Policy 	| Security Group 	|   Function  	|
|:----------------:	|:---------------:	|:------------:	|:--------------:	|:--------------:	|:-----------:	|
|      Ubuntu      	|    ELK Server   	| 10.10.2.x/24 	|     Private    	|  ELK-SG  	|    Server   	|
|      Ubuntu      	|  DVWA 1 Server  	| 10.10.2.x/24 	|     Private    	|  WebServer-SG  	|    Server   	|
|      Ubuntu      	|  DVWA 2 Server  	| 10.10.2.x/24 	|     Private    	|  WebServer-SG  	|    Server   	|
|      Windows     	| Windows Machine 	| 10.10.0.x/24 	|     Public     	|   Windows-SG   	| Viewing our services 	|
|   Amazon Linux EC2  	| Ansible/Docker/Jumpbox 	| 10.10.0.x/24 	|     Public     	|   Jumpbox-SG   	|   Gateway   	|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box and RDP machines can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: The two webservers would be considered whitelisted
ip 10.10.2.x
ip 10.10.2.x

Machines within the network can only be accessed by SSH protocol for Linux and RDP secure for windows.
- The Jump Box is the only machine accesable by my own home network 


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration needs to be performed manually, which is advantageous because of automating configuration with Ansible, is this practice saves time, it is easier on the installation process and there will be no trouble shooting during deployment because the scripts and commands work.

The playbook implements the following tasks:
- _Here is a simple rundown or the ELK installation process 
- SSH into jumpbox and install and download/run the Docker service. Be sure to pull the correct ansible container for your jumpbox.
- Run Docker and ssh into your private machines from the ansible container to establish a connection to them and then set your ansible files to allow these private machines to have ansible deploy to them with your playbook.
- Use the proper commands to copy the playbooks and your public key over to the docker container
- Using your newly copied playbooks and key, deploy the playbooks
- Use windows to ensure that your playbooks have deployed


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- DWVA 10.10.2.x
- DVWA2 10.10.2.x
- Filebeats 10.10.2.x


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the file to ansible:/root.
- Update the filebeat.yml file to include the ELK ip 
- Run the playbook, and navigate to Kibana in your windows RDP to check that the installation worked as expected.

The files that were used and include are - filebeat-playbook.yml this file was acquired from a secure credible website written by a trusted source 
- You have to edit and reconfigure the configuration file. 
The way I specified which machine to install the ELK server 
on versus the way in which to install Filebeat on . by navigating to the ansible director while the Is the elk server was more automated by  was done in hosts file and the file beat was configured prior to by changing lines 1106 and making it my 10.10.0.27 and the doing the same to 1806 in the filebeat.yml file prior to importingin to docker.
- _The url you want to navigate is http://10.10.2.31:5601/ to make sure that elk is working 

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

Step 1: Use CloudFormation to form a Network Stack: VPC, Subnets, Route Tables, IGW, NAT

- Go to https://aws.amazon.com/cloudformation/ and upload your basic network template file. Click next and then launch the network stack according to your template.

The CloudFormation built here demonstrates creating a basic network and automatic deployment on AWS that utilizes an ELK server and load-balanced DVWAs for testing, practicing, and learning purposes. 

![Alt text](https://raw.githubusercontent.com/BORoS49/UCI-Cloud-Networking/main/Ansible/Images/Cloudformation%20stack.png?raw=true "Cloud Formation Stack")

![Alt text](https://raw.githubusercontent.com/BORoS49/UCI-Cloud-Networking/main/Ansible/Images/Create%20Stack.png?raw=true "Create Stack")

![Alt text](https://raw.githubusercontent.com/BORoS49/UCI-Cloud-Networking/main/Ansible/Images/Basuc-Network.png?raw=true "Cloud Formation Stack")


Step 2: Set IPV4 to auto for both public subnets

- Go to your subnets page, highlight your public subnets, go to actions, click on "Modify auto-assign IP Settings" and then check the box titled "Enable auto-assign public IPv4 address"

![Alt text](https://github.com/BORoS49/UCI-Cloud-Networking/blob/main/Ansible/Images/Set%20IPV4.png?raw=true)

![Alt text](https://github.com/BORoS49/UCI-Cloud-Networking/blob/main/Ansible/Images/Set%20IPV4%202.png?raw=true)

Step 3: Launch Public Amazon Linux EC2 Instance

- Amazon Linux 2 AMI

- Set to VPC1 created with cloudformation template

- Public1 Subnet

- t2 Micro (Free Tier)

- Configure Security Group (Port 22, SSH)

- Select or create a Key Pair (mine is called "OregonKey.pem")

![Alt text](https://github.com/BORoS49/UCI-Cloud-Networking/blob/main/Ansible/Images/Launch%20EC2%20Instance.png?raw=true)

![Alt text](https://user-images.githubusercontent.com/75498072/112550142-2750cd00-8d7c-11eb-8aaa-77132cab1d75.png)

![Alt text](https://github.com/BORoS49/UCI-Cloud-Networking/blob/main/Ansible/Images/Configuring%20EC2%20Instance.png?raw=true)

![Alt text](https://github.com/BORoS49/UCI-Cloud-Networking/blob/main/Ansible/Images/EC2%20Security%20Group.png?raw=true)

![Alt text](https://github.com/BORoS49/UCI-Cloud-Networking/blob/main/Ansible/Images/Key%20Pair.png?raw=true)


Step 4: Setup 2 Ubuntu Private Subnet Instances for the ansible container

- Ubuntu Server 20.04 LTS (HVM)

- t2 Micro (Free Tier)

- Private1 Subnet

- Configure Security Group (Port 22 and 80, SSH & HTTP)

- Select Key Pair used for EC2 Instance (OregonKey.pem)

- Launch Instance

Step 5: Verify Instances are running


Step 6: Connect to your Public Instance via CMD on your work machine VIA your public key for the instance

- Need to be in the folder where your key pair is stored

- ```ssh -i "OregonKey.pem" ec2-user@ec2-54-68-215-46.us-west-2.compute.amazonaws.com```



Step 7: Use another CMD console to import your public key and the ansible container to your public instance

- ```scp -i "Key" "file to be transferred" "location":/home/"user"```

- ```scp -i "OregonKey.pem" OregonKey.pem ansible_config.yml ec2-user@ec2-54-68-215-46.us-west-2.compute.amazonaws.com:/home/ec2-user```



Step 8: chmod 400 the key on your EC2 instance

- ```sudo chmod 400 "key"```

- ```sudo chmod 400 OregonKey.pem```

Step 9: Get Docker on your EC2 instance

- ```sudo yum install docker```



Step 10: Start docker and verify its running

- ```sudo service docker start```

- ```sudo service docker status```


Step 11: Pull the cybersecurity ansible container image onto your public instance and verify its there.

- ```sudo docker pull cyberxsecurity/ansible```

- ```sudo docker images```



Step 12: Set up the daimon.json file for docker

- ```cd /etc/docker```

- ```sudo nano daemon.json ```

- Paste the following into the .json and save it

```
{
"default-address-pools":
[
{"base":"10.10.0.0/24","size":16}
]
}
```
Step 13: Restart docker

- ```sudo service docker restart```


Step 14: Connect to the docker image pulled previously 

- ```sudo docker run -ti cyberxsecurity/ansible bash```

- ```Should change to root@"container ID" ```

Step 15: add the public key and ansible config/playbook to the docker container running from another ec2 terminal in cmd 

- Launch new cmd and ssh into your ec2 instance

- ```ssh -i "OregonKey.pem" ec2-user@ec2-54-68-215-46.us-west-2.compute.amazonaws.com```

- ```sudo docker ps``` (This pulls up the active docker containers)

- ```sudo docker cp OregonKey.pem c98c5b496c89:/root```

- ```sudo docker cp ansible_config.yml c98c5b496c89:/root```



Step 16: SSH from the ansible container into both private instances and update/upgrade them

- ```ssh -i "OregonKey.pem" ubuntu@10.10.2.32```

- ```sudo apt-get update```

- ```sudo apt-get upgrade```

- ```exit```

- ```ssh -i "OregonKey.pem" ubuntu@10.10.2.52```

- ```sudo apt-get update```

- ```sudo apt-get upgrade```

- ```exit```

Step 17: Get into the /etc/ansible folder and edit the hosts and ansible.cfg files to allow the private machines to hosts the webservers

- ```cd /etc/ansible```

- ```nano hosts`````` (Uncomment "Webservers" and add IP addresses of both private instances underneath)

- ```nano ansible.cfg``` (Change remote user to ubuntu, "remote_user = ubuntu")

Step 18: Run the ansible playbook from the ~ folder in the container

- ```ansible-playbook ansible_config.yml --key-file OregonKey.pem```

Step 19: Set up a windows instance to connect to DVWA

Step 20: Connect to windows and verify DVWA is running via the private DNS of one of the containers the ansible playbook deployed on

Step 21: Create Elk Stack Instance

- Ubunutu

- T3 medium

- ELK Stack Security Group (ports open are: 22, 80, 5044, 5601, 9200, 9300, 9600)

Step 22: Run Elk

- Download the install-elk.yml file
- Edit contents of install-elk.yml so that "remote_user = ubuntu"
- Move install-elk.yml to ansible docker 
- ```sudo docker cp <file> <docker process>:/root```
- In docker process (aka ansible), make sure to add (if not there) the following beneath "[webservers]" and the ip addresses in /etc/ansible/hosts:
[Elk]
- Private IPv4 Address of your ELK server>


- Ensure that elkserver ubuntu instance has been updated and upgraded 

- ```sudo apt-get update``` or upgrade

- Ensure before running install-elk.yml that you have sshed into the ELK server
- Ensure that inbound rules on your ELK server allow for ports 5044, 5061, and 9200 to be open.
- Run the following command within our ansible container ```ansible-playbook install-elk.yml --key-file="your key"```

- Connect by copying the private ip address of your ELK server and paste it into your Windows machine and connect via port 5601.

Step 23: CELEBRATE GOOD TIMES CMON