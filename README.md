### 🛠️ Jenkins Setup Using Docker (Blue Ocean + Docker Pipeline)

---

### 📁 Prerequisites

- Docker installed
- Git installed
- Windows PowerShell or Linux Terminal
- Internet connection

---

### 📥 Clone the Repository

Run the below command to download Jenkins project files from GitHub:

`git clone https://github.com/SahanaReddy06/Jenkins`


---

### 🏗️ Build the Jenkins Docker Image

Build a custom Jenkins image:

`docker build -t myjenkins-blueocean:2.528.2-1 .`


---

### 🌐 Create a Docker Network

Set up a network for Jenkins and Docker communication:

`docker network create jenkins`


Verify the network:
`docker network ls`


---

### 🚀 Run Jenkins Container

Use this command (PowerShell compatible):

`docker run --name jenkins-blueocean --restart=on-failure --detach ^
--network jenkins ^
--env DOCKER_HOST=tcp://docker:2376 ^
--env DOCKER_CERT_PATH=/certs/client ^
--env DOCKER_TLS_VERIFY=1 ^
--volume jenkins-data:/var/jenkins_home ^
--volume jenkins-docker-certs:/certs/client:ro ^
--publish 8080:8080 ^
--publish 50000:50000 ^
myjenkins-blueocean:2.528.2-1`


---

### 📌 What This Command Does

- Creates container: `jenkins-blueocean`
- Auto-restarts on failure
- Runs in background
- Connects to network: `jenkins`
- Sets environment variables for Docker + TLS
- Mounts persistent volumes for Jenkins config and Docker certs
- Exposes ports `8080` (Jenkins UI), `50000` (agents)
- Uses image: `myjenkins-blueocean:2.528.2-1`

---

### 🌍 Open Jenkins in Browser

Visit:
http://localhost:8080

You will see the Unlock Jenkins screen.

---

### 🔑 Get Jenkins Initial Admin Password

Retrieve the password for Jenkins unlock:

`docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword`

Paste this password into the Jenkins UI.

---

### 🔧 Start / Stop Jenkins

**Start Jenkins:**
`docker start jenkins-blueocean`

**Stop Jenkins:**
`docker stop jenkins-blueocean`

**Restart Jenkins:**
`docker restart jenkins-blueocean`

**View running containers:**
`docker ps`

---

### 📌 Important Notes

- Jenkins data is stored in the `jenkins-data` Docker volume, so it persists.
- After reboot, simply use:
`docker start jenkins-blueocean`


- No need to rebuild or re-run full setup.

---

### 🎉 Jenkins Is Ready!

You can now:

- Install plugins
- Create CI/CD pipelines
- Build and deploy apps
- Connect GitHub webhooks
- Use Docker inside Jenkins

