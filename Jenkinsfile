pipeline {
    agent none
    stages {
        stage('Build Jar') {
            agent {
                docker {
                    image 'maven:3-alpine'
                    args '-v $HOME/.m2:/root/.m2'
                }
            }
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Build Image') {
            steps {
                script {
                	app = docker.build("madcard31/selenium-docker")
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
			        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
			        	app.push("${BUILD_NUMBER}")
			            app.push("latest")
			        }
                }
            }
        }
    }
}



// pipeline {
//     // master executor should be set to 0
//     agent any
//     environment {
//         DOCKER_CREDS = credentials('dockerhub')
//     }
//     stages {
//         stage('Build Jar') {
//             steps {
//                 bat 'mvn clean package -DskipTests'
//             }
//         }
//         stage('Build Image') {
//             steps {
//                 bat 'docker build -t=madcard31/selenium-docker .'
//             }
//         }
//         stage('Push Image') {
//             steps {
//                 bat 'docker login --username $DOCKER_CREDS_USR --password $DOCKER_CREDS_PSW https://registry.hub.docker.com'
//                 bat 'docker push madcard31/selenium-docker:latest'
//             }
//         }
//     } // stages
//     post{
//         always {
//             bat 'docker logout'
//         }
//     }
// } // pipeline