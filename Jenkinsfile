pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B install -DskipTests'
            }
        }
        stage('Package') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [],
                userRemoteConfigs: [[url: 'https://github.com/traccytian/Teedy_2024.git']])
                sh 'mvn -B -DskipTests clean package'
            }
        }
        // Building Docker images
        stage('Building image') {
            steps{
                //your command
                sh 'sudo docker build -t teedy2024_manual .'
                sh 'sudo su'
            }
        }
        // Uploading Docker images into Docker Hub
        stage('Upload image') {
            steps{
                //your command
                sh 'sudo docker tag teedy2024_manual 123456zjc/teedy_local:v1.0'
                sh 'sudo docker image push 123456zjc/teedy_local:v1.0'
            }
        }
        //Running Docker container
            stage('Run containers'){
            steps{
                //your command
                sh 'sudo docker pull 123456zjc/teedy_local:v1.0'
                sh 'sudo docker run -d -p 8084:8080 --name teedy_manual011 teedy2024_manual'
                sh 'sudo docker run -d -p 8082:8080 --name teedy_manual022 teedy2024_manual'
                sh 'sudo docker run -d -p 8083:8080 --name teedy_manual033 teedy2024_manual'
            }
        }

    }


}
