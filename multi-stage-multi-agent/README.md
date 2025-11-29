# Multi Stage Multi Agent

Set up a multi stage jenkins pipeline where each stage is run on a unique agent. This is a very useful approach when you have multi language application
or application that has conflicting dependencies.


### Short Explanation

Your pipeline has 2 stages:

## Back-end Stage

Uses a Docker container with Maven + Java 11

Runs the command:

mvn --version


This checks if Maven is working.

## Front-end Stage

Uses a different Docker container with Node.js 16

Runs the command:

node --version


This checks if Node.js is working.

🎯 Main Idea

➡️ agent none
Jenkins should not use a default agent.

➡️ Each stage uses its OWN agent with its OWN Docker container.

So:

Backend stage → Maven container

Frontend stage → Node.js container

Both run separately and cleanly.
