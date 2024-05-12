pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
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
                sh 'docker build -t teedy2024_manual .'
            }
        }
        // Uploading Docker images into Docker Hub
        stage('Upload image') {
            steps{
                //your command
                sh 'docker tag teedy2024_manual 123456zjc/teedy_local:v1.0
                    docker image push 123456zjc/teedy_local:v1.0'
            }
        }
        //Running Docker container
            stage('Run containers'){
            steps{
                //your command
                sh 'docker pull 123456zjc/teedy_local:v1.0
                    docker run -d -p 8084:8080 --name teedy_manual01 teedy2024_manual
                    docker run -d -p 8082:8080 --name teedy_manual02 teedy2024_manual
                    docker run -d -p 8083:8080 --name teedy_manual03 teedy2024_manual'
            }
        }

    }


}
