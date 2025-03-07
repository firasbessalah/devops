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

        /* Uncomment if you need SonarQube analysis
        stage('MVN SONARQUBE') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.login=squ_b89f78b6e34a1e612085135b6784f32676ec1480 -Dsonar.skipTests=true'
            }
        }
        */

        stage('MVN Nexus') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }

            stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_VERSION} ."
                }
            }
        }

    }
}
