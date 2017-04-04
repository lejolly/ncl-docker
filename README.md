# Docker for NCL
Quickly setup Docker on NCL. 

## Instructions
1. Create an experiment on NCL using the [template.ns](template.ns) file or a ns file of your own. 
2. If you do not yet have a Docker image on NCL, start with the Ubuntu Server 14.04 image and use the [install-docker.sh](install-docker.sh) script to install Docker. 
3. This is all you need to do to get Docker running, but it's not doing much now is it?

## Instructions for getting Docker Swarm and Portainer Running
1. Choose one node to be the manager node in the swarm. Following the [template.ns](template.ns), let's pick `node0` as an example. Just take note of its IP address (in this case it's `172.30.1.2`). 
2. Just run the command on the chosen node to initialize the swarm: `$ sudo docker swarm init --advertise-addr=172.30.1.2` (change the IP address accordingly). 
3. If the above command completes successfully, it should output another command which we will then use on the other nodes so that they can join the swarm. 
	- Sample output: `$ docker swarm join --token SWMTKN-1-49nj1cmql0jkz5s954yi3oex3nedyz0fb0xx14ie39trti4wxv-8vxv8rssmk743ojnwacrr2e7c 172.30.1.2:2377`
4. Enter the above command on the other nodes for them to join the swarm. 
5. If everything completes successfully, we can now install Portainer for easier management of the swarm. 
6. On the manager node, run this command: `$ sudo docker run -d -p 9000:9000 -v "/var/run/docker.sock:/var/run/docker.sock" portainer/portainer`
7. Now point your web browser to port 9000 of the manager node to access Portainer (you may have to forward this port through SSH). 
8. Portainer will prompt you to create a password on your first login, and once you're in, you can now use the swarm for something more fun. 
9. If you're looking for something to use your swarm for, why not create your very own Mirai botnet? Look here for instructions: [docker-mirai](https://github.com/lejolly/docker-mirai)