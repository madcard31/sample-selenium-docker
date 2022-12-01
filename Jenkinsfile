pipeline {
    // master executor should be set to 0
    agent any
    stages {
        stage('Build Jar') {
            steps {
                //sh
                bat 'mvn clean package -DskipTests'
            }
        }
        stage('Build Image') {
            steps {
                //sh
                bat 'docker build -t=madcard31/selenium-docker .'
            }
        }
        stage('Push Image') {
            environment {
                DOCKER_CREDS = credentials('dockerhub')
            }
            steps {
                //sh
                bat 'echo $DOCKER_CREDS_PSW | docker login -u $DOCKER_CREDS_USR --password-stdin'
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