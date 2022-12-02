#!/usr/bin/env groovy
pipeline {
    // master executor should be set to 0
    agent any
    options {
        skipStagesAfterUnstable()
    }
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
                withCredentials([string(credentialsId: 'dockerhub_pwd', variable: 'DOCKER_PWD')]) {
                    bat 'docker login -u madcard31 -p %DOCKER_PWD%'
                }
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