pipeline {
    environment{
        branchName="dimitrijk/kiii-jenkins"
    }
    agent any

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        stage('Build image') {
            steps {
                script {
                    def app = docker.build("dimitrijk/kiii-jenkins")
                }
            }
        }
        stage('Push image') {
            steps {
                script {
                    // right parameter is jenkins credentials
                   docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {            
                       app.push("${env.BUILD_NUMBER}")            
                       app.push("latest")  
                }
            }
        }
    }
}
