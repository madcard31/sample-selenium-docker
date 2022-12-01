pipeline {
    // master executor should be set to 0
    agent any
    environment {
        DOCKER_CREDS = credentials('dockerhub')
    }
    stages {
        stage('Build Jar') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }
        stage('Build Image') {
            steps {
                bat 'docker build -t=madcard31/selenium-docker .'
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker login -u $DOCKER_CREDS_USR -p $DOCKER_CREDS_PSW'
                bat 'docker push madcard31/selenium-docker:latest'
            }
        }
    } // stages
    post{
        always {
            bat 'docker logout'
        }
    }
} // pipeline