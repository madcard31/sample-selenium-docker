pipeline {
    // master executor should be set to 0
    agent any
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
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    bat 'docker login --username $user --password $pass https://registry.hub.docker.com'
                    bat 'docker push madcard31/selenium-docker:latest'
                }
            }
        }
    } // stages
    post{
        always {
            bat 'docker logout'
        }
    }
} // pipeline