# Ansible-Playbook-LaunchDocker-container

🌟Configure webserver inside Docker by using Ansible automation🌟

![Screenshot 2024-03-05 174420](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/8d1dccb8-16de-4aa8-aba6-6a13e5c78993)


For this Configuration I take two instance one for Ansible-Master node & Ansible-Target node, I use AWS cloud ans EC2 instance is "Amazon Linux".

⚡prerequisites:

   Ansible ssh configuration (set-up) master and target node must be done and ansible installed.
   
❄NOTE:

For this configuration Ansible master node need Docker collection,

Use this command to install Docker community collection:

#ansible-galaxy collection install community.docker


write an ansible playbook that does the following operations in managed nodes:
1. download docker package ,
2. start and enable docker service , 
3. pull httpd image from docker hub ,
4.  Run docker container using httpd image and expose it to public ,
5. copy local html code to /var/www/html on container .

