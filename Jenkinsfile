pipeline {
    agent {docker {
    image 'maven:3.8.4-openjdk-17-slim'
}}
    stages {
        stage('Build') {
            steps {
                sh 'mvn --version'
                echo "Build"
            }
        }
        stage('Test') {
            steps {
                echo "Test"
            }
        }
        stage('Integration Test') {
            steps {
                echo "Integration Test"
            }
        }
    }
    post {
       always {
            echo "This will always run"
        }
        success {
            echo "This will run only if the build succeeds"
        }
        failure {
            echo "This will run only if the build fails"
        }
    }
}