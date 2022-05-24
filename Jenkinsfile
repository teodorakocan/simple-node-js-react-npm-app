pipeline {
    agent any

    stages{
        

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
    }
}
