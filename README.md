# Simple questions and exercices to learn about Docker!! ;)

### Questions

```
1- docker info  
2- docker run hello-world  
3- docker images  
4- docker ps -a  
5- docker logs -f c51f86c28340  
6- docker rm $(docker ps -qa)  
7- docker run alpine ls -l  
8- docker run -it alpine /bin/sh  
9- http://hub.docker.com/  
10- docker run --name static-site -e AUTHOR="Icaro Bichir" -d -p 8888:80 dockersamples/static-site  
```

### Concept
	Images:
	- Base images 	
	- Child images 
	- Official images
	- User images

### Analysing Logs
```
docker run -d alpine sh -c 'while true; do date; sleep 1; done'
```

### Love cats?
```
cd flask-app/
docker build -t local/flask-app .
docker run -d --name flask -p 8080:5000 local/flask-app
```

### Docker image with Jenkins 2.3, with docker inside.
```
git clone git@github.com:IcaroBichir/dind-plus-jenkins.git

docker-compose up --build

docker exec jenkins2.3 cat /var/jenkins_home/secrets/initialAdminPassword
```

### A visualizer for Docker Swarm Mode using the Docker Remote API, Node.JS, and D3
```
docker run -it -d -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock dockersamples/visualizer

docker service create \
  --name=test1 \
  --publish=8081:8080/tcp \
  --constraint=node.role==manager \
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
  dockersamples/visualizer

docker service create \
  --name=static-site \
  --publish=8082:80/tcp \
  --constraint=node.role==manager \
  --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock \
  dockersamples/static-site

docker service create \
  --name=jenkins-swarmed \
  --publish=8083:8080/tcp \
  --constraint=node.role==manager \
  dindplusjenkins_jenkins2.0

docker service create \
  --name=cat-gifs1 \
  --publish=8085:5000/tcp \
  --constraint=node.role==manager \
  --detach=false \
  local/flask-app

docker service ls
docker service scale
docker service logs
```

### Kill and remove images
```
docker ps
docker kill DOCKER_ID
docker rm DOCKER_ID
docker image
docker rmi IMAGE_ID
docker kill $(docker ps -qa)
docker rm $(docker ps -qa)
docker rm $(docker ps -a -f status=exited -q)
docker rmi $(docker images -a -q)
docker images | grep "pattern" | awk '{print $1}' | xargs docker rm
```


## Next Chapter ;)

```
git clone https://github.com/docker/example-voting-app.git
cd example-voting-app

docker swarm init
docker stack deploy --compose-file docker-stack.yml vote
docker stack services vote
http://localhost:5000
http://localhost:5001
docker stack ls
docker stack rm vote
```