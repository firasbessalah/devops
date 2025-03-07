pipeline {
    agent any

    environment {
        IMAGE_NAME = "firasbessalah/test"
        IMAGE_VERSION = "1.0.1"
    }

    stages {
        stage('GIT') {
            steps {
                git branch: 'master', url: 'https://github.com/firasbessalah/devops.git'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('MVN Nexus') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'sudo docker build -t ${IMAGE_NAME}:${IMAGE_VERSION} .'
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'firasbessalah', passwordVariable: '25175009@fifa')]) {
                        sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    }
                }
            }
        }


    }
}
