pipeline {
    agent any

    environment{
        NEW_VERSION = sh(
                script: "printf \$(git rev-parse ${GIT_COMMIT})",
                returnStdout: true
        )
    }

    stages{
        stage('Git Hub Checkout') {
            steps{
                git branch: 'master', credentialsId: 'GitHubCredentials', url: 'https://github.com/teodorakocan/simple-node-js-react-npm-app.git'
            }
        }

        stage('Build Docker Image') {
            steps{
                sh "docker build -t teodorakocan/demo:${NEW_VERSION} ."
            }
        }

        stage('Push Docker Image Into Docker Hub') {
            steps{
                withCredentials([string(credentialsId: 'Docker_Password', variable: 'Docker_Password')]) 
                {
                    sh "docker login -u teodorakocan -p ${Docker_Password}"
                }
                sh "docker push teodorakocan/demo:${NEW_VERSION}"
            }
        }
        
        stage('Pull Image from Docker Hub') {
            steps{
                sh "docker pull teodorakocan/demo:${NEW_VERSION}"
            }
        }
    }
}
