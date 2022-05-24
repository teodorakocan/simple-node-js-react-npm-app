pipeline {
    agent any

    tools {nodejs "node"}

    stages{
        stage('Git Hub Checkout') {
            environment{
                NEW_VERSION = "${sh(returnStdout: true, script: 'export GIT_SHA=$(git rev-parse HEAD)')}"
            }
            
            steps{
                sh 'npm install git'
                echo "${NEW_VERSION}"
                git credentialsId: 'GitHubCredentials', url: 'https://github.com/teodorakocan/simple-node-js-react-npm-app.git'  
            }
        }

        stage('Build Docker Image') {
            steps{
                sh "export GIT_SHA=\$(git rev-parse HEAD)"
                sh "docker build -t teodorakocan/demo:latest -t teodorakocan/demo:GIT_SHA ."
            }
        }

        stage('Push Docker Image Into Docker Hub') {
            steps{
                withCredentials([string(credentialsId: 'Docker_Password', variable: 'Docker_Password')]) 
                {
                    sh "docker login -u teodorakocan -p ${Docker_Password}"
                }
                sh 'docker push teodorakocan/demo:latest'
                sh "docker push teodorakocan/demo:${GIT_SHA}"
            }
        }
    }
}
