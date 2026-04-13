pipeline {
//    agent {docker {
//    image 'maven:3.8.4-openjdk-17-slim'
//}}
    agent any

    environment {
        dockerHome = tool 'myDocker'
        mavenHome = tool 'myMaven'
        PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn --version'
                sh 'docker version'
                echo "Build"
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Integration Test') {
            steps {
                sh 'mvn failsafe:integration-test failsafe:verify'
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