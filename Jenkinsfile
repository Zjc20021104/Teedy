pipeline {
agent any
stages {
stage('Build') {
steps {
sh 'mvn -B -DskipTests clean package'
}
}
stage('K8s') {
steps {
sh 'kubectl set image deployments/hello-node gcr.io/k8s-minikube/kicbase:v0.0.44=ac520a1862a7'
}
}
}
}
