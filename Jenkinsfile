pipeline {
    agent {
        docker {
            image 'node:16' // or any other Node version you want
        }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // deploy steps go here
            }
        }
    }
}
