pipeline {
    agent any
    
    environment {
        SONARQUBE = 'SonarQube'
        DOCKER_IMAGE = 'helloworld-python:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/yourusername/helloworld-python.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'echo "Building the Python app"'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Dockerize') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/app.py', allowEmptyArchive: true
            junit '**/target/test-*.xml'
        }
    }
}
