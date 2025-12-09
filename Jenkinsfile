pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven3'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t maysseem/demo-maven:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub',
                                                 usernameVariable: 'USERNAME',
                                                 passwordVariable: 'PASSWORD')]) {
                    bat """
                        echo Logging into Docker Hub...
                        docker login -u %USERNAME% -p %PASSWORD%
                        docker push maysseem/demo-maven:latest
                    """
                }
            }
        }
    }
}
