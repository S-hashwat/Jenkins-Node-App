# Jenkins + Node.js CI/CD Pipeline

This project sets up a Continuous Integration/Continuous Deployment (CI/CD) pipeline using **Jenkins** for a sample **Node.js application** hosted on **GitHub**.

---

## 🚀 Project Structure

Jenkins-Node-App/ ├── Jenkinsfile ├── package.json ├── index.js └── ...

yaml
Copy
Edit

---

## 🛠️ Prerequisites

- Docker installed on your system
- GitHub account with the repository: [https://github.com/S-hashwat/Jenkins-Node-App](https://github.com/S-hashwat/Jenkins-Node-App)
- VS Code or terminal access
- Internet access to pull Jenkins image and install plugins

---

## 🐳 Run Jenkins in Docker

```bash
docker run -d -p 8080:8080 -p 50000:50000 \
  --name jenkins \
  --user root \
  -v jenkins_home:/var/jenkins_home \
  jenkins/jenkins:lts
We used --user root to allow installation of Node.js inside the Jenkins container.

🔑 Unlock Jenkins
Open browser: http://localhost:8080

Get the initial admin password:

bash
Copy
Edit
docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword
Paste the password, continue, and install Suggested Plugins

🔌 Install Node.js Plugin
Navigate to Manage Jenkins → Plugin Manager

Search for and install: NodeJS Plugin

⚙️ Configure Node.js Tool
Go to Manage Jenkins → Global Tool Configuration

Under NodeJS, click Add NodeJS

Name: Node 16, check Install automatically, and select version 16.x

🧪 Jenkins Pipeline Setup
Jenkinsfile
groovy
Copy
Edit
pipeline {
    agent any

    tools {
        nodejs "Node 16"
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                sh 'npm test || echo "Tests failed, but continuing..."'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
            }
        }
    }
}
🔗 Create a Pipeline Job in Jenkins
Go to Jenkins Dashboard → New Item

Name: NodeAppPipeline

Select Pipeline, then click OK

In the Pipeline section:

Definition: Pipeline script from SCM

SCM: Git

Repo URL: https://github.com/S-hashwat/Jenkins-Node-App.git

Branch: */main

Save and click Build Now

✅ Output
Jenkins clones the repo

Installs dependencies using npm install

Runs tests (or echoes warning)

Displays deploy stage message

🧯 Common Errors Faced & Solutions
Error	Fix
docker: not found	Run Jenkins container with --user root
Invalid agent type "docker"	Use agent any instead
npm: not found	Install NodeJS via Jenkins plugin
couldn't find remote ref master	Use main branch instead of master
Permission denied while apt-get update	Use root user in container
