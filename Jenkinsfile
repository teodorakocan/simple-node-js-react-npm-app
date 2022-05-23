node {
    stage('Git Hub Checkout') {
        git credentialsId: 'GitHubCredentials', url: 'https://github.com/teodorakocan/simple-node-js-react-npm-app.git'  
    }

    stage('Build Docker Image') {
        sh 'docker build -t teodorakocan/demo:v1 .'
    }

    stage('Push Docker Image Into Docker Hub') {
        steps{
            withCredentials([string(credentialsId: 'Docker_Password', variable: 'Docker_Password')]) 
            {
                bat "docker login -u teodorakocan -p ${Docker_Password}"
            }
            bat 'docker push teodorakocan/demo:v1'
        }
    }
}
