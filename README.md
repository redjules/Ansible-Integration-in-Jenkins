# Ansible-Integration-in-Jenkins

-create and configure a dedicated server for Jenkins

I have created a droplet in Digital Ocean to be a dedicated server for Jenkins:

<img width="686" alt="Screenshot 2024-11-03 at 15 17 49" src="https://github.com/user-attachments/assets/a4def363-50a5-4f30-a411-f95322d994f4">


- create and configure a dedicated server for Ansible Control Node

I have created 2 droplets in Digital Ocean as 2 remote servers that we will connect to Ansible

<img width="576" alt="Screenshot 2024-11-03 at 16 12 24" src="https://github.com/user-attachments/assets/336b0c64-bdeb-405b-9948-983b45fa9829">

we check python3 is installed:

![Screenshot 2024-11-03 at 16 13 58](https://github.com/user-attachments/assets/0eb0605c-eaac-489c-91ce-8c39c7192767)

Now we are going to connect Ansible to these 2 remote servers

We create the hostfile (Ansible inventory file) with command:

```
vim hosts
```

and write there the IP addresses of all the servers we want to connect to with Ansible and this hostfile we can specidy which private key Ansible should use for each host using an attribute called Ansible ssh private key file that takes the location of the private key and we specify the ansible user root:

![Screenshot 2024-11-03 at 16 21 39](https://github.com/user-attachments/assets/6dbafde6-624e-4b91-9e6a-22d827273e14)

-write Ansible Playbook, which configures 2 EC2 Instances


- Add ssh key file credentials in Jenkins for Ansible Control Node server and Ansible Managed Node servers
- configure Jenkins to execute the Ansible Playbook on remote Ansible Control Node server as part of the CI/CD pipeline
- so the Jenkins configuration will do the following:
a. Connect to the remote Ansible Control Node server
b. Copy Ansible playbook and configuration files to the remote ANSIBLE Control Node server
c. Copy the ssh keys for the Ansible Managed Node servers to the Ansible Control Node server
d. Install Ansible, Python3, Boto3 on the Ansible Control Noe server
e. With everything installed and copied to the remote Ansible Control Node server, execute the playbook remotely on that Control Node that will configure the 2EC2 Managed Nodes

