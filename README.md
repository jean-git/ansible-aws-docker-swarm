# Install Docker Swarm cluster with Ansible

# Introduction
This is a ansible project to deploy and configure a Docker Swarm Cluster. This will install and configure the following resources:
- 1 docker swarm master
- 2 docker swarm workers

# What we need
- 3 servers with communitication each other
- The network ports required for a Docker Swarm to function correctly are:
    - TCP port 2376 for secure Docker client communication. This port is required for Docker Machine to work. Docker Machine is used to orchestrate Docker hosts.
    - TCP port 2377. This port is used for communication between the nodes of a Docker Swarm or cluster. It only needs to be opened on manager nodes.
    - TCP and UDP port 7946 for communication among nodes (container network discovery).
    - UDP port 4789 for overlay network traffic (container ingress networking).

- Your ansible configured and have communication with 3 servers

# How To Run
- Clone this repository
- Make sure you have terraform installed
- Make sure, AWS credentials are set in ~/.aws/credentials or exported variables in your enviremont:
    - Linux or macOS:
        - export AWS_ACCESS_KEY_ID=YOUR_AWS_ACCESS_KEY_ID
        - export AWS_SECRET_ACCESS_KEY=YOUR_AWS_SECRET_ACCESS_KEY

    - Windows Command Prompt:
        - setx AWS_ACCESS_KEY_ID YOUR_AWS_ACCESS_KEY_ID
        - setx AWS_SECRET_ACCESS_KEY YOUR_AWS_SECRET_ACCESS_KEY
    
    - PowerShell
        - $Env:AWS_ACCESS_KEY_ID="YOUR_AWS_ACCESS_KEY_ID"
        - $Env:AWS_SECRET_ACCESS_KEY="YOUR_AWS_SECRET_ACCESS_KEY"

- in variables.tf file, change variable value(aws-key-us-west-2) to you EC2 Key Name
- Edit hosts files with yours servers IPs
    ```
    [swarm_master]
    IP_YOUR_MASTER

    [swarm_workers]
    IP_YOUR_WORKER_1
    IP_YOUR_WORKER_2
    ```
- Run ansible Playbook
    ```
    ansible-playbook -i hosts main.yml
    ```
    

