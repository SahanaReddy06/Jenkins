🚀 Jenkins Setup Using Docker (Blue Ocean + Docker Pipeline)

This guide explains how to install and run Jenkins using Docker, build the Jenkins image, configure networking, unlock Jenkins, and start/stop the container.

📌 1. Clone the Repository
git clone https://github.com/SahanaReddy06/Jenkins


Downloads the Jenkins project files from GitHub.

📌 2. Build the Jenkins Docker Image
docker build -t myjenkins-blueocean:2.528.2-1 .


Builds a custom Jenkins image using the Dockerfile in the current directory.

📌 3. Create a Docker Network
docker network create jenkins


Creates an isolated network for Jenkins + Docker to communicate safely.

Verify the network:

docker network ls

📌 4. Run Jenkins Container

Use this PowerShell-compatible command:

docker run --name jenkins-blueocean --restart=on-failure --detach ^
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 ^
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 ^
  --volume jenkins-data:/var/jenkins_home ^
  --volume jenkins-docker-certs:/certs/client:ro ^
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.528.2-1

✔️ What this command does:

Creates a container: jenkins-blueocean

Auto restarts on failure

Runs in background (detached)

Connects to the jenkins network

Sets Docker environment variables

Mounts volumes:

jenkins-data → Jenkins home

jenkins-docker-certs → Docker certificates

Exposes ports:

8080 → Jenkins UI

50000 → Jenkins agents

Uses image: myjenkins-blueocean:2.528.2-1

📌 5. Open Jenkins in Browser

Once the container starts, visit:

👉 http://localhost:8080

This will display the Unlock Jenkins page.

📌 6. Get Jenkins Initial Admin Password
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword


Displays the initial password stored inside the container.
Copy it and paste into Jenkins UI to unlock.

📌 7. Start/Stop Jenkins Later

After the first setup, do NOT run the full docker run command again.

Use these simple commands:

▶️ Start Jenkins
docker start jenkins-blueocean

⏹ Stop Jenkins
docker stop jenkins-blueocean

🔄 Restart Jenkins
docker restart jenkins-blueocean

📦 View running containers
docker ps

📌 8. Important Notes

Jenkins configuration is stored inside the jenkins-data volume.

After system restart, simply run:

docker start jenkins-blueocean


No need to rebuild the Docker image every time.

🎉 Jenkins is Ready!

You can now:

Install plugins

Create CI/CD pipelines

Build & deploy apps

Connect GitHub webhooks

Use Docker inside Jenkins
