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
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        app.push("dimitrijk/kiii-jenkins$BUILD_NUMBER")
                        app.push("$branchName-latest")
                        // signal the orchestrator that there is a new version
                    }
                }
            }
        }
    }
}
