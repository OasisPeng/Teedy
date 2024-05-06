pipeline {
    agent any
    stages {
        stage('Print Maven Version') {
            steps {
                powershell 'mvn --version'
            }
        }
        stage('Print Java Version') {
            steps {
                powershell 'java --version'
            }
        }
        stage('Build') {
            steps {
                powershell 'mvn -B -DskipTests clean package'
            }
        }
        stage('pmd') {
            steps {
                powershell 'mvn pmd:pmd'
            }
        }
        stage('Test') {
            steps {
                powershell 'mvn test'
            }
        }
        stage('Doc') {
            steps {
                powershell 'mvn javadoc:jar'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            junit '**/target/surefire-reports/**/*.xml'
        }
    }
}
