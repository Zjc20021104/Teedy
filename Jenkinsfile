pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // 检出项目代码
                git 'https://github.com/Zjc20021104/Teedy.git'
            }
        }
        stage('Build') {
            steps {
                // 构建项目
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                // 运行测试
                sh 'mvn test'
                // 生成测试报告
                junit 'target/surefire-reports/**/*.xml'
            }
        }
        stage('Generate Javadoc') {
            steps {
                // 生成 Javadoc
                sh 'mvn javadoc:jar'
                // 将生成的 Javadoc 打包为 artifact
                archiveArtifacts artifacts: 'target/site/apidocs/**/*.jar', fingerprint: true
            }
        }
    }
}
