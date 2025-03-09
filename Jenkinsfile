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
stage('Git Checkout') {
    steps {
        git branch: 'main', url: 'https://github.com/firasbessalah/devops.git'
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
              withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'

                    }
                }
            }
        }
      stage('Push Docker Image') {
            steps {
                script {
                    sh 'docker push ${IMAGE_NAME}:${IMAGE_VERSION}'
                }
            }
        }
        stage('Verify docker-compose.yml') {
    steps {
        script {
            sh 'ls -la'  // This will list all files in the workspace to check if docker-compose.yml is present
        }
    }
}

             stage('Run Docker Compose') {
            steps {
                script {
                    // Run Docker Compose in detached mode
                    sh 'docker compose -f docker-compose.yml up -d'
                }
            }
        }


    }
}
