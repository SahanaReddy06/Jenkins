🛠️ Jenkins Setup Using Docker (Blue Ocean + Docker Pipeline)
📁 Prerequisites
Docker installed

Git installed

Windows PowerShell or Linux Terminal

Internet connection

📥 Clone the Repository
Run the below command to download Jenkins project files from GitHub:

bash
git clone https://github.com/SahanaReddy06/Jenkins
🏗️ Build the Jenkins Docker Image
Build a custom Jenkins image:

bash
docker build -t myjenkins-blueocean:2.528.2-1 .
🌐 Create a Docker Network
Set up a network for Jenkins and Docker communication:

bash
docker network create jenkins
Verify Network:

bash
docker network ls
🚀 Run Jenkins Container
Use this command (compatible with Windows PowerShell):

bash
docker run --name jenkins-blueocean --restart=on-failure --detach ^
  --network jenkins ^
  --env DOCKER_HOST=tcp://docker:2376 ^
  --env DOCKER_CERT_PATH=/certs/client ^
  --env DOCKER_TLS_VERIFY=1 ^
  --volume jenkins-data:/var/jenkins_home ^
  --volume jenkins-docker-certs:/certs/client:ro ^
  --publish 8080:8080 ^
  --publish 50000:50000 ^
  myjenkins-blueocean:2.528.2-1
📌 What This Command Does
Creates container: jenkins-blueocean

Auto-restarts on failure

Runs in background

Connects to network: jenkins

Sets environment variables: Docker host + TLS

Mounts volumes:

jenkins-data → Jenkins configuration

jenkins-docker-certs → Docker certificates

Exposes ports:

8080 → Jenkins UI

50000 → Jenkins agents

Uses image: myjenkins-blueocean:2.528.2-1

🌍 Open Jenkins in Browser
Visit:

text
http://localhost:8080
You will see the Unlock Jenkins screen.

🔑 Get Jenkins Initial Admin Password
Find the initial password with:

bash
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
Then paste it into Jenkins to unlock.

🔧 Start / Stop Jenkins Later
Do not run the full docker run command again after the first setup.

To Start Jenkins:

bash
docker start jenkins-blueocean
To Stop Jenkins:

bash
docker stop jenkins-blueocean
To Restart Jenkins:

bash
docker restart jenkins-blueocean
View Running Containers:

bash
docker ps
📌 Important Notes
All Jenkins data is stored in the jenkins-data Docker volume (persistent).

After system reboot, simply run:

bash
docker start jenkins-blueocean
No need to rebuild the image or re-run full setup.

🎉 Jenkins Is Ready!
You can now:

Install plugins

Create CI/CD pipelines

Build & deploy applications

Connect GitHub webhooks

Use Docker inside Jenkins

If you want, I can also create:
A separate section for Pipeline setup

A Jenkinsfile example

A Docker-in-Docker setup section

Instructions for GitHub Webhook integration
