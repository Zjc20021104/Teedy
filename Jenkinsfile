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
sh 'kubectl delete deployment  hello-node'
  sh 'kubectl create deployment hello-node --image=123456zjc/teedy_local:v1.0'
  //sh 'kubectl expose deployment hello-node --type=LoadBalancer --port=8080'
  sh 'minikube service hello-node'
}
}
}
}
