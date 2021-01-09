# Ansible Installation

Ansible is an open-source automation platform. It is very, very simple to set up and yet powerful. Ansible can help you with configuration management, application deployment, task automation.

### Pre-requisites

1. An AWS EC2 instance (on Control node)

### Installation steps:
#### on Amazon EC2 instance

1. Install python and python-pip
   ```sh
   sudo su
   yum install python
   yum install python-pip
   ```
1. Install ansible using pip check for version
    ```sh
    pip install ansible
   ansible --version
   ```
   
1. Create a user called ansadmin (on Control node and Managed host)  
   ```sh
   useradd ansadmin
   passwd ansadmin
   ```
1. Below command grant sudo access to ansadmin user. But we strongly recommended using "visudo" command if you are aware vi or nano editor.  (on Control node and Managed host)
   ```sh
   echo "ansadmin ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
   ```
   
1. Log in as a ansadmin user on master and generate ssh key (on Control node)
   ```sh 
   sudo su - ansadmin
   ssh-keygen
   ```
1. Copy keys onto all ansible managed hosts (on Control node)
   ```sh 
   ssh-copy-id ansadmin@<target-server>
   ```

1. Ansible server used to create images and store on docker registry. Hence install docker, start docker services and add ansadmin to the docker group. 
   ```sh
   yum install docker
   
   # start docker services 
   service docker status
   service docker start 
   
   # add user to docker group 
   usermod -aG docker ansadmin
   
   ##Edit PasswordAuthentication to "yes" for docker.
   vi /etc/ssh/sshd_config
   service sshd reload

   ```
   
1. Create a directory /etc/ansible and create an inventory file called "hosts" add control node and managed hosts IP addresses to it. 


### Validation test

   
1. Run ansible command as ansadmin user it should be successful (Master)
   ```sh 
   ansible all -m ping
   ```
### switch to Docker server and add ansadmin

   ```sh
   useradd ansadmin
   passwd ansadmin
   ```
### switch to Ansible server
make sure your in ansadmin home directory and copy over ssh key ID for ansadmin to Docker server 
   ```sh
   hostname ansible-control-node
   sudo su -
   su - ansadmin
   ssh-copy-id ansadmin@"IP-ADDR_DOCKER-SERVER"
   ##ssh into docker server to confirm passwordless authentication
   ssh ansadmin@"Docker-Server-IP"
   ```

### test connectivity by creating hostfile
make sure your in ansible server and create hostfile
   ```sh
   cd /etc/ansible
   ls
   sudo vi hosts
   add ip address of your docker server and then next line type in localhost
   save file
   ```
Add ansible-id to localhost by running the following command

      ```sh
      sh-copy-id localhost
      ```

Test connectivity to all servers by running ping module
   ```sh
   ansible all -m ping
   ```

   
   






