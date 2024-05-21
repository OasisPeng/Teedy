pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('K8s') {
            steps {
                script {
                    def imageName = 'jasmine84444/teedy:latest'
                    sh "kubectl set image deployments/hello-node container-name=$imageName"
                }
            }
        }
}
