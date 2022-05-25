pipeline {
    agent any

    enivironment{
        GIT_COMMIT_SHORT = sh(
                script: "printf \$(git rev-parse --short ${GIT_COMMIT})",
                returnStdout: true
        )
    }

    stages{
        stage('Git Hub Checkout') {
            steps{
                echo "${GIT_COMMIT_SHORT}"
                git credentialsId: 'GitHubCredentials', url: 'https://github.com/teodorakocan/simple-node-js-react-npm-app.git'  
            }
        }
        
        stage('Build Docker Image') {
            steps{
                sh "docker build -t teodorakocan/demo:${env.BUILD_NUMBER} ."
            }
        }

        stage('Push Docker Image Into Docker Hub') {
            steps{
                withCredentials([string(credentialsId: 'Docker_Password', variable: 'Docker_Password')]) 
                {
                    sh "docker login -u teodorakocan -p ${Docker_Password}"
                }
                sh "docker push teodorakocan/demo:${env.BUILD_NUMBER}"
            }
        }

        stage('Pull Image from Docker Hub') {
            steps{
                sh "docker pull teodorakocan/demo:${env.BUILD_NUMBER}"
            }
        }
    }
}
