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
//        stage('Integration Test') {
//            steps {
//                sh 'mvn failsafe:integration-test failsafe:verify'
//            }
//        }

        stage('Package') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }
        stage('Build Docker Image') {
             steps {
                //sh 'docker build -t abhinav27/currency-exchange-devops:$env.BUILD_TAG'
                script {
                    dockerImage = docker.build("abhinav27/currency-exchange-devops:${env.BUILD_TAG}")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub') {
                        dockerImage.push();
                        dockerImage.push('latest');
                    }
                }
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