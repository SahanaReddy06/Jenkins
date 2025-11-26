🛠️ Jenkins Setup Using Docker (Blue Ocean + Docker Pipeline)

This guide explains how to install and run Jenkins inside Docker, build the Jenkins image, configure networking, unlock Jenkins, and manage the Jenkins container.

📁 Prerequisites

Docker installed

Git installed

Windows PowerShell / Linux Terminal

Internet connection

📥 1. Clone the Repository
git clone https://github.com/SahanaReddy06/Jenkins


Purpose: Downloads the Jenkins project files from GitHub.

🏗️ 2. Build the Jenkins Docker Image
docker build -t myjenkins-blueocean:2.528.2-1 .


Purpose: Builds a custom Jenkins image using the Dockerfile in the current directory.

🌐 3. Create a Docker Network
docker network create jenkins


Purpose: Creates an isolated network for Jenkins + Docker communication.

✔ Verify Network
docker network ls

🚀 4. Run Jenkins Container

Use this PowerShell-compatible command:

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

Connects to: jenkins Docker network

Environment variables set: Docker host + TLS

Volumes mounted:

jenkins-data → Stores Jenkins configuration

jenkins-docker-certs → Docker certificates

Ports exposed:

8080 → Jenkins UI

50000 → Jenkins agent communication

Uses image: myjenkins-blueocean:2.528.2-1

🌍 5. Open Jenkins in Browser

Visit:

http://localhost:8080


You will see the Unlock Jenkins screen.

🔑 6. Get Jenkins Initial Admin Password
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword


Copy and paste this password into the Jenkins UI.

🔧 7. Start / Stop Jenkins Later

⚠️ Do NOT run the full docker run command again after the first setup.

▶ Start Jenkins
docker start jenkins-blueocean

⏹ Stop Jenkins
docker stop jenkins-blueocean

🔄 Restart Jenkins
docker restart jenkins-blueocean

📦 Check Running Containers
docker ps

📌 8. Important Notes

All Jenkins data is stored inside the jenkins-data Docker volume.

After a system reboot, simply run:

docker start jenkins-blueocean


No need to rebuild the image again.

🎉 Jenkins Is Ready

You can now:

Install plugins

Create CI/CD pipelines

Build & deploy applications

Connect GitHub webhooks

Use Docker inside Jenkins
