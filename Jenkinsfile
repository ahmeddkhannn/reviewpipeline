pipeline {
    agent any

    environment {
        GIT_CREDENTIALS_ID = 'github-credentials'
        SONARQUBE_SERVER = 'SonarQube'
        SONARQUBE_TOKEN = credentials('sonarqube-token')
        DOCKER_IMAGE = 'helloworld-python:latest'
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    echo 'Cloning repository...'
                    git branch: 'main', url: 'https://github.com/ahmeddkhannn/reviewpipeline.git', credentialsId: env.GIT_CREDENTIALS_ID
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Building...'
                    // Use 'sh' for Unix-based agents
                    bat 'echo "Building the Python app"'
                }
            }
        }

        stage('Dockerize') {
            steps {
                script {
                    echo 'Dockerizing...'
                    // Use 'sh' for Unix-based agents
                    bat 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    echo 'Running SonarQube analysis...'
                    withSonarQubeEnv(env.SONARQUBE_SERVER) {
                        // Use 'sh' for Unix-based agents
                        sh 'sonar-scanner -Dsonar.projectKey=my-project-key -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.login=${SONARQUBE_TOKEN}'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Deployment stage. Add deployment steps here if needed.'
                    // This stage can be customized for your deployment needs
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}
