pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World....!'
            }
        }
        stage('checkout') {
            steps {
                echo 'Hello World....checkout!'
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ktallapakam/devops-automation.git']])
                sh "mvn clean install"
            }
        }
        stage('docker-build') {
            steps {
                echo 'Hello World....docker-build!'
                script {
                    sh "docker build -t tallapakam/mypublicdocker:devops-automation ."
                }
            }
        }
        stage('docker-push') {
            steps {
                echo 'Hello World....docker-push!'
                script {
                    withCredentials([string(credentialsId: 'DocHubCred', variable: 'DockerHubCred')]) {
                        sh "docker login -u tallapakam -p ${DockerHubCred}"
                    }
                    sh "docker push tallapakam/mypublicdocker:devops-automation"

                }
            }
        }
    }
}
