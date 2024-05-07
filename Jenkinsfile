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
                bat 'mvn -Dtest=GroupDaoTest test --fail-never'
                bat 'mvn surefire-report:report'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            archiveArtifacts artifacts: 'target/site/surefire-report/*', fingerprint: true
            junit '**/target/site/surefire-reports/**/*.xml'
        }
    }
}
