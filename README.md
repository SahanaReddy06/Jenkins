Commands to unlock jenkins: 

git clone https://github.com/SahanaReddy06/Jenkins

docker build -t myjenkins-blueocean:2.528.2-1 .

docker network create jenkins

docker network ls

docker run --name jenkins-blueocean --restart=on-failure --detach ^
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 ^
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 ^
  --volume jenkins-data:/var/jenkins_home ^
  --volume jenkins-docker-certs:/certs/client:ro ^
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.528.2-1

Browse to http://localhost:8080 (or whichever port you configured for Jenkins when installing it) and wait until the Unlock Jenkins page appears.

docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
(above command gives a password)
