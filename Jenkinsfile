pipeline {
    agent any
    stages {
//         stage('Build') {
//             steps {
//                 bat 'mvn -B -DskipTests clean package'
//             }
//         }
//         stage('pmd') {
//             steps {
//                 bat 'mvn clean -DskipTests install'
//                 bat 'mvn pmd:pmd'
//             }
//         }

        stage('Doc') {
            steps {
                bat 'mvn javadoc:jar --fail-never'
            }
        }

        stage('Test report') {
            steps {
                bat 'mvn test'
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
