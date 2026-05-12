pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Verify Tools') {
            steps {
                sh '''
                    echo "Checking Java version..."
                    java -version

                    echo "Checking Maven version..."
                    mvn -version
                '''
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Simple Maven build completed successfully.'
        }

        failure {
            echo 'Simple Maven build failed. Please check the console output.'
        }
    }
}
