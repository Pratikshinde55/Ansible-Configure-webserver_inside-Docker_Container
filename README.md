# Ansible-Playbook-LaunchDocker-container

🌟Configure webserver inside Docker by using Ansible automation🌟

![Screenshot 2024-03-05 174420](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/8d1dccb8-16de-4aa8-aba6-6a13e5c78993)


For this Configuration I take two instance one for Ansible-Master node & Ansible-Target node, I use AWS cloud ans EC2 instance is "Amazon Linux".

![Screenshot 2024-03-05 173517](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/7497cd99-984b-4f13-a0d6-f79eb1787b74)


⚡prerequisites:

   Ansible ssh configuration (set-up) master and target node must be done and ansible installed.
   
❄NOTE:

For this configuration Ansible master node need Docker collection, and also install python3-pip.

Use this command to install Docker community collection:


       #ansible-galaxy collection install community.docker

![Screenshot 2024-03-05 171855](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/4ef212b5-59dd-4dd7-bf5a-b9ee542aa78d)

On ansible master node i create workspace for this configuration named as "mycode" & create code(webpage) which deploy on apache webserver.

![Screenshot 2024-03-05 173437](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/1e002af3-07d2-4a67-bcf5-c2ac69edbbc7)



Play ansible playbook 

![Screenshot 2024-03-05 172636](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/e6d5cf8c-a116-4d96-943f-d6c3f94c4cc3)


write an ansible playbook that does the following operations in managed nodes:
1. download docker package ,
2. start and enable docker service , 
3. pull httpd image from docker hub ,
4.  Run docker container using httpd image and expose it to public ,
5. copy local html code to /var/www/html on container .

