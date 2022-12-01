pipeline {
    // master executor should be set to 0
    agent any
    environment {
            DOCKER_CREDS = credentials('dockerhub')
    }
    stages {
        stage('Build Jar') {
            steps {
                //sh
                bat "mvn clean package -DskipTests"
            }
        }
        stage('Build Image') {
            steps {
                //sh
                bat "docker build -t=madcard31/selenium-docker ."
            }
        }
        stage('Push Image') {
            steps {
                    //sh
			        bat "docker login --username=$DOCKER_CREDS_USR --password-stdin=$DOCKER_CREDS_PWD"
			        bat "docker push madcard31/selenium-docker:latest"
			    }
            }
        }
    }
}