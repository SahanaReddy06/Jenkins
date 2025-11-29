# A simple jenkins pipeline to verify if the docker slave configuration is working as expected.
**⭐ Short Explanation**

1️⃣ Jenkins picks an agent (a worker machine).

2️⃣ On that agent, Jenkins starts a Docker container using:

node:16-alpine (this already has Node.js 16 installed)

3️⃣ Inside that Docker container, Jenkins runs:

node --version

4️⃣ The container prints Node.js version → job successful.

That’s it.
