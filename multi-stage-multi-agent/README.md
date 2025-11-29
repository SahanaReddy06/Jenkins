# Multi Stage Multi Agent

Set up a multi stage jenkins pipeline where each stage is run on a unique agent. This is a very useful approach when you have multi language application
or application that has conflicting dependencies.

**⭐ Short Explanation**

1️⃣ Jenkins picks an agent (a worker machine).

2️⃣ On that agent, Jenkins starts a Docker container using:

node:16-alpine (this already has Node.js 16 installed)

3️⃣ Inside that Docker container, Jenkins runs:

node --version

4️⃣ The container prints Node.js version → job successful.

That’s it.
