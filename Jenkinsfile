pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('pmd') {
            steps {
                bat 'mvn clean -DskipTests install'
                bat 'mvn pmd:pmd'
            }
        }
        stage('Test report') {
            steps {
                bat 'mvn -Dtest=GroupDaoTest test --fail-never'
            }
        }
        stage('Doc') {
            steps {
                bat ' mvn javadoc:javadoc --fail-never'
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
