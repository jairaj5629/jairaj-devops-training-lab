pipeline {
    agent any

    environment {
        BUILD_VERSION = "3.0.${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout') {
            steps {
                echo "Checking out source code..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building artifact version ${BUILD_VERSION}"
                sh '''
                    mkdir -p build
                    echo "Artifact built by Jenkins build #${BUILD_NUMBER}" > build/app.txt
                    zip -r build/app-${BUILD_VERSION}.zip build/app.txt
                '''
            }
        }

        stage('Test') {
            steps {
                echo "Simulating tests..."
                sh 'echo "Tests passed successfully."'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'build/*.zip', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully."
        }
        failure {
            echo "Pipeline failed."
        }
    }
}
