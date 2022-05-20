node {
    stage('Build') { 
        sh 'npm install'
    }
    
    stage('Git Hub Checkout') {
        git credentialsId: 'GitHubCredentials', url: 'https://github.com/teodorakocan/simple-node-js-react-npm-app.git'  
    }

    stage('Build Docker Image') {
        bat 'docker build -t teodorakocan/demo:v1 .'
    }

    stage('Push Docker Image Into Docker Hub') {
        withCredentials([string(credentialsId: 'Docker_Password', variable: 'Docker_Password')]) 
        {
            bat "docker login -u teodorakocan -p ${Docker_Password}"
        }
        bat 'docker push teodorakocan/demo:v1'
    }
}
