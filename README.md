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

we connect the 2 servers to Ansibles with command:

```
ansible all -i hosts -m ping
```

![Screenshot 2024-11-03 at 18 52 48](https://github.com/user-attachments/assets/16408c6f-4085-4e29-8821-ec0b11e857b8)

we rearrange to make it cleaner the hostfile:

![Screenshot 2024-11-03 at 19 00 07](https://github.com/user-attachments/assets/0bdb1d41-c2bd-4dfe-954d-3c49645e729a)

-write Ansible Playbook, which configures 2 EC2 Instances

we go to AWS EC2 and create 2 instances and a key pair called ansible:

![Screenshot 2024-11-03 at 20 00 59](https://github.com/user-attachments/assets/b1f889cc-de41-4608-b3f8-d75f1e9c779a)

![Screenshot 2024-11-03 at 21 10 49](https://github.com/user-attachments/assets/07453e2b-582f-46f0-a7ce-a86f899c1869)

and we update the hostfile and copy the public DNS:

![Screenshot 2024-11-03 at 21 11 01](https://github.com/user-attachments/assets/51b2edf8-a7d8-4561-9e6c-023f80032bb9)

![Screenshot 2024-11-03 at 21 12 15](https://github.com/user-attachments/assets/54bb178d-b31a-4c97-af13-f39403744923)

we check the python version in the instance:

![Screenshot 2024-11-03 at 21 15 46](https://github.com/user-attachments/assets/65ff67a4-1ad5-4b3f-8357-eba12f6e082b)

we execute te ansible command:

![Screenshot 2024-11-03 at 21 16 45](https://github.com/user-attachments/assets/26792f0b-1ceb-4bdc-9639-bb458730865e)

we see we have a warning about the python interpreter. We can solve it editing the hostfile and adding the location of the Python interepreter explicitly for the host:

![Screenshot 2024-11-03 at 21 21 04](https://github.com/user-attachments/assets/4265ef83-b07a-4367-828a-27c61f84275f)

and the warning has disappeared from the first server:

![Screenshot 2024-11-03 at 21 21 26](https://github.com/user-attachments/assets/caef448c-d422-49a9-95ac-4aa66991fa92)

- Add ssh key file credentials in Jenkins for Ansible Control Node server and Ansible Managed Node servers
- configure Jenkins to execute the Ansible Playbook on remote Ansible Control Node server as part of the CI/CD pipeline
- so the Jenkins configuration will do the following:
a. Connect to the remote Ansible Control Node server
b. Copy Ansible playbook and configuration files to the remote ANSIBLE Control Node server
c. Copy the ssh keys for the Ansible Managed Node servers to the Ansible Control Node server
d. Install Ansible, Python3, Boto3 on the Ansible Control Noe server
e. With everything installed and copied to the remote Ansible Control Node server, execute the playbook remotely on that Control Node that will configure the 2EC2 Managed Nodes

