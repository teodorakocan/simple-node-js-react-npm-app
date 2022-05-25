pipeline {
    agent any

    environment{
        registry = "teodorakocan/demo"
        registryCredential = 'Docker_Password'
        dockerImage = ''
        NEW_VERSION = sh(
                script: "printf \$(git rev-parse ${GIT_COMMIT})",
                returnStdout: true
        )
    }

    stages{
        stage('Build'){
            steps{
                echo " ${PATH}"
            }
        }
        stage('Build Docker Image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":${NEW_VERSION}"
                }
            }
        }

        stage('Push Docker Image Into Docker Hub') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Pull Image from Docker Hub') {
            steps{
                sh "docker pull teodorakocan/demo:${NEW_VERSION}"
            }
        }
    }
}
