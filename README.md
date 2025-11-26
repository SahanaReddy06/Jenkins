🚀 Jenkins Setup Using Docker (Blue Ocean + Docker Pipeline)

This guide explains how to install and run Jenkins using Docker, build the Jenkins image, configure networking, unlock Jenkins, and manage the Jenkins container.

📌 1. Clone the Repository
git clone https://github.com/SahanaReddy06/Jenkins


Downloads Jenkins project files from GitHub.

📌 2. Build the Jenkins Docker Image
docker build -t myjenkins-blueocean:2.528.2-1 .


Builds a custom Jenkins image using the Dockerfile in the current directory.

📌 3. Create a Docker Network
docker network create jenkins


Creates an isolated Docker network for Jenkins + Docker communication.

✔️ Verify network
docker network ls

📌 4. Run Jenkins Container

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

✔️ What this command does

Creates container: jenkins-blueocean

Restarts automatically on failure

Runs in background (--detach)

Connects to jenkins Docker network

Sets required Docker environment variables

Mounts volumes:

jenkins-data → Jenkins home directory

jenkins-docker-certs → Docker certificates

Exposes ports:

8080 → Jenkins UI

50000 → Jenkins agent communication

Uses image: myjenkins-blueocean:2.528.2-1

📌 5. Open Jenkins in Browser

Visit:

👉 http://localhost:8080

You will see the Unlock Jenkins page.

📌 6. Get Jenkins Initial Admin Password
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword


Shows the initial admin password.

Copy/paste into Jenkins UI.

📌 7. Start / Stop Jenkins Later

Do NOT run the full docker run command again.

▶️ Start Jenkins
docker start jenkins-blueocean

⏹ Stop Jenkins
docker stop jenkins-blueocean

🔄 Restart Jenkins
docker restart jenkins-blueocean

📦 Check running containers
docker ps

📌 8. Important Notes

Jenkins data is stored in jenkins-data volume (persistent).

After system reboot, just run:

docker start jenkins-blueocean


No need to rebuild or rerun the full command.

🎉 Jenkins is Ready!

You can now:

Install plugins

Create CI/CD pipelines

Build & deploy applications

Configure GitHub webhooks

Use Docker inside Jenkins
