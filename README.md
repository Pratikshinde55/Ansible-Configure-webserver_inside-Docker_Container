# Ansible-Playbook-LaunchDocker-container

🌟Configure webserver inside Docker by using Ansible automation🌟

![Screenshot 2024-03-05 174420](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/8d1dccb8-16de-4aa8-aba6-6a13e5c78993)


For this Configuration I take two instance one for Ansible-Master node & Ansible-Target node, I use AWS cloud and EC2 instance is "Amazon Linux".

![Screenshot 2024-03-05 173517](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/7497cd99-984b-4f13-a0d6-f79eb1787b74)


⚡prerequisites:

   Ansible ssh configuration (set-up) master and target node must be done and ansible installed.
   
NOTE:

For this configuration Ansible master node need Docker collection, and also install python3-pip .

Use this command to install Docker community collection:


       #ansible-galaxy collection install community.docker

![Screenshot 2024-03-05 171855](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/4ef212b5-59dd-4dd7-bf5a-b9ee542aa78d)

On ansible master node i create workspace for this configuration named as "mycode" & create code(webpage) "Index.html" which deploy on apache webserver.

![Screenshot 2024-03-05 173437](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/1e002af3-07d2-4a67-bcf5-c2ac69edbbc7)



open or write ansible-playbook :

My ansible-playbook name is "myweb.yml" ,

NOTE: Ansible-playbook name must be in " .yml " 


        #vim myweb.yml


💫Here some information about playbook task💫
 1. download docker package:

       
            tasks:

               - name: Install Docker
                 yum:
                   name: docker
                   state: present

           
2. start and enable docker service:


            - name: Start Docker service
              systemd:
                name: docker
                state: started
                enabled: yes

3. Create a file which will add to my apache conatiner create file in path /root/code :

   File is module which help to create directory in ansible-playbook 


                - name: create file for adding container volume
                  file:
                      state: directory
                       path: /root/code1
            





Run ansible playbook :

    
      #ansible-playbook myweb.yml

![Screenshot 2024-03-05 172636](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/e6d5cf8c-a116-4d96-943f-d6c3f94c4cc3)




❄️After ansible-playbook run successfully, on Target node Automation take place & configure our tasks .

![Screenshot 2024-03-05 173327](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/c10ceda7-3104-45ef-ab5e-b804128d97f1)



⭐Now From Browser i can access my webserver :

  On google - "< public ip of target node > : port no /index.html"

![Screenshot 2024-03-05 173455](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/8287070f-5632-4ed9-89e8-c93775ebcdef)


Also from my laptop command prompt: using "curl" command

![Screenshot 2024-03-05 173048](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/8718ac9e-3259-4e68-a775-1f44b09ed0dc)



write an ansible playbook that does the following operations in managed nodes:
1. download docker package ,
2. start and enable docker service , 
3. pull httpd image from docker hub ,
4.  Run docker container using httpd image and expose it to public ,
5. copy local html code to /var/www/html on container .

