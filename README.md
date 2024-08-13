# Dockerizing Number Counting Application

![Diagram](https://github.com/Helion55/Dockerizing-Number-Counter-Application/blob/main/Dockerizing-Number-Counter-Application.jpg?raw=true)

A number counting application made with GO, running on port 8080, using Redis a database and Nginx as reverse proxy. This Project is about creating an image of the Application and Running that with Docker Compose on Vagrant Machine configured with Ansible. I have configured Nginx as reverse proxy and passing the config file on docker compose, pulling the Redis Image and connecting all together to run the whole Application Stack. Vagrant is used to create the Virtual Machine where our application is deployed using Ansible playbook.

## Tech Stack
1. Go
2. Redis
3. Nginx
4. Docker
5. Ansible
6. Vagrant

## Steps and Commands
### Creating the Dockerfile
1. Pulling the Golang image and exposing the port.
2. In the Dockerfile passing two Environment variables input 
```DEMO_APP_ADDR = <APPLICATION-IP>:<APPLICATION-PORT>``` 
and 
```DEMO_REDIS_ADDR = <REDIS-CONTAINER-NAME>:<REDIS-PORT>``` 
3. Specifying the working directory where application code will be copied and executed.
4. Copying the Application code.
5. Building the Application.
6. Running the Application.

### Creating Docker Compose file
1. Creating the services as ```demoapp```, ```database``` and ```server```.
2. Giving the build context or the dockerfile location
3. Giving ```image-name```, ```container-name``` and specifying the ```ports``` of database and server services.
4. Creating a Volume to store Redis data
5. Adding that volume to redis container
6. Passing the Nginx Configfile

### Configuring Nginx as Reverse proxy
1. Get the Config file on nginx containers ``` /etc/nginx/conf.d ``` directory. 
2. Copy that file and configure it on the proxy pass section.
3. Give the port and ip of your application.

### Vagrant Machine starting 
1. After Installing Vagrant writing the command 
```
vagrant init <YOUR-MACHINE-NAME>
```
and 
```
vagrant up
```
to start the machine.

2. The IP of that machine is needed so execute
```
vagrant ssh
```
to ssh into system and get the ip
### Ansible Playbook Execution
1. Creating a ssh pair and connect with the Vagrant machine.
2. Creating ```ansible.cfg``` file to configure ansible for this project.
3. Creating a ``` inventory``` file and stored the Vagrant machine IP
4. Writting the Ansible playbook and,
 - Adding user demo
 - Setingup firewall to open only ports- 22,80,6379,8080
 - Configuring sysctl to increase open file limits
 - Setting systems time zone to asia/kolkata
 - Installing docker
 - Deploying docker-compose 
 - Running the services
5. Finnaly executing the playbook by running...
```
ansible-playbook playbook.yaml
```
