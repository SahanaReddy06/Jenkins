🚀 Jenkins Setup Using Docker (Blue Ocean + Docker Pipeline)

This guide explains how to install and run Jenkins using Docker, build the Jenkins Docker image, set up networking, unlock Jenkins, and start/stop the Jenkins container.

## 📌 1. Clone the Repository
git clone https://github.com/SahanaReddy06/Jenkins


✅ Downloads your Jenkins project files from GitHub to your local system.

## 📌 2. Build the Jenkins Docker Image
docker build -t myjenkins-blueocean:2.528.2-1 .


✅ Builds a custom Docker image named myjenkins-blueocean:2.528.2-1 using the Dockerfile in the current folder.

## 📌 3. Create a Docker Network
docker network create jenkins


Creates an isolated Docker network for Jenkins to communicate with Docker-in-Docker safely.

✔️ Verify the network:
docker network ls

## 📌 4. Run Jenkins Container

Use this (PowerShell compatible) command:

docker run --name jenkins-blueocean --restart=on-failure --detach ^
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 ^
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 ^
  --volume jenkins-data:/var/jenkins_home ^
  --volume jenkins-docker-certs:/certs/client:ro ^
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.528.2-1

✔️ What this command does:

Creates a container named jenkins-blueocean

Automatically restarts on failure

Runs in background (detached)

Connects to the jenkins network

Sets Docker environment variables

Mounts volumes:

jenkins-data → Jenkins home folder

jenkins-docker-certs → Docker certificates

Exposes ports:

8080 → Jenkins UI

50000 → Jenkins agents

Uses image myjenkins-blueocean:2.528.2-1

## 📌 5. Open Jenkins in Browser

After the container starts, open:

👉 http://localhost:8080

You will see the Unlock Jenkins page.

## 📌 6. Get Jenkins Initial Admin Password

Run this:

docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword

✔️ What it does:

Prints the password stored inside the container to unlock Jenkins during the first setup.

Copy the password and paste it into Jenkins UI.

## 📌 7. Start/Stop Jenkins Later

You do NOT need to run the big docker run command again.

Once the container is created, use these:

▶️ Start Jenkins
docker start jenkins-blueocean

⏹ Stop Jenkins
docker stop jenkins-blueocean

🔄 Restart Jenkins
docker restart jenkins-blueocean

📦 Check running containers
docker ps

## 📌 8. IMPORTANT Notes

Jenkins configurations persist inside the jenkins-data volume.

If you restart your computer, simply run:

docker start jenkins-blueocean


No need to rebuild the image every time.

🎉 Jenkins is ready to use!

You can now:

Install plugins

Create pipelines

Build & deploy applications

Integrate GitHub/Webhooks

Use Docker inside Jenkins
