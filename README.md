# Configure webserver inside Docker by using Ansible automation

![Screenshot 2024-03-05 174420](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/8d1dccb8-16de-4aa8-aba6-6a13e5c78993)


For this Configuration I take two instance one for Ansible-Master node & Ansible-Target node, I use AWS cloud and EC2 instance is "Amazon Linux".

![Screenshot 2024-03-05 173517](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/7497cd99-984b-4f13-a0d6-f79eb1787b74)


### prerequisites:

Ansible ssh configuration (set-up) master and target node must be done and ansible installed.
   
[Ansible-master-target-SSH-Setup-onAWS](https://github.com/Pratikshinde55/Ansible-setup-onAWS.git) 
(Use given link for ssh configuration)
  
- NOTE:

For this configuration Ansible master node need Docker collection, and also install python3-pip .

Use this command to install **Docker community collection**:

      ansible-galaxy collection install community.docker

![Screenshot 2024-03-05 171855](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/4ef212b5-59dd-4dd7-bf5a-b9ee542aa78d)

On ansible master node i create workspace for this configuration named as "mycode" & create code(webpage) "Index.html" which deploy on apache webserver.

![Screenshot 2024-03-05 173437](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/1e002af3-07d2-4a67-bcf5-c2ac69edbbc7)



open or write ansible-playbook :

My ansible-playbook name is "myweb.yml" ,

NOTE: Ansible-playbook name must be extension " **.yml** " 

      vim myweb.yml


### Here some information about playbook tasks:

 1. **download Docker package**:

       
            tasks:

               - name: Install Docker
                 yum:
                   name: docker
                   state: present

           
2. **Start and enable Docker service**:


            - name: Start Docker service
              systemd:
                name: docker
                state: started
                enabled: yes

3. **Create a file which will add to my apache container create file in path /root/code** :

   File module in ansible-playbook which help to create directory.


                - name: create file for adding container volume
                  file:
                      state: directory
                       path: /root/code1
            
4. **Local code or local Webpage copy**:
   
    Copy module in ansible-playbook helps to copy my local master node code to target node dest: /root/code1 this destination is point 3 i have created 


                    - name: copy local code or deploy webpage
                      copy:
                        src: index.html
                        dest: /root/code1

 5. **Pull httpd image for Docker Container**: 


                  - name: Pull httpd image from Docker Hub
                    docker_image:
                      name: httpd
                      source: pull

 6. **Launch Docker container using httpd image & exposed this httpd container for clients. Here i have atached volume to container this volume contain my webpage
    "index.html" from master node to Target node to docker httpd container:**


                  - name: Run httpd container
                    docker_container:
                      name: my_httpd_container
                      image: httpd
                      state: started
                      exposed_ports: 80
                      ports:
                       - "8080:80"
                      volumes:
                       - /root/code1/index.html/:/usr/local/apache2/htdocs/index.html
                      restart_policy: always


    
### Run ansible playbook :

    ansible-playbook myweb.yml

![Screenshot 2024-03-05 172636](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/e6d5cf8c-a116-4d96-943f-d6c3f94c4cc3)




**After ansible-playbook run successfully, on Target node Automation take place & configure our tasks**

![Screenshot 2024-03-05 173327](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/c10ceda7-3104-45ef-ab5e-b804128d97f1)



### Now From Browser i can access my Webserver :

  On google - "< public ip of target node > : port no /index.html"

![Screenshot 2024-03-05 173455](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/8287070f-5632-4ed9-89e8-c93775ebcdef)


Also from my laptop command prompt: using "curl" command

![Screenshot 2024-03-05 173048](https://github.com/Pratikshinde55/Ansible-Playbook-LaunchDocker-container/assets/145910708/8718ac9e-3259-4e68-a775-1f44b09ed0dc)





