pipeline {
    // master executor should be set to 0
    agent any
    stages {
        stage('Build Maven Jar') {
            steps {
                bat 'mvn clean install -DskipTests'
            }
        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t=madcard31/selenium-docker .'
            }
        }
        stage('Push Docker Image to Docker Hub') {
            steps {
			    withCredentials([string(credentialsId: 'dockerhub_pwd', variable: 'dockerhub_pwd')]) {
                    bat 'docker login -u madcard31 -p ${dockerhub_pwd}'
                }
			    bat 'docker push madcard31/selenium-docker:latest'
            }
        }
    }
}