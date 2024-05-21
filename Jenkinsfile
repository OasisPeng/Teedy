pipeline {
    agent any
    environment {
        KUBECONFIG = credentials('/var/lib/jenkins/.kube/config') 
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
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
}
